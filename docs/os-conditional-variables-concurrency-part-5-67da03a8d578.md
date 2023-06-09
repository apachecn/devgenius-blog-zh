# [OS]条件变量—并发性第 5 部分

> 原文：<https://blog.devgenius.io/os-conditional-variables-concurrency-part-5-67da03a8d578?source=collection_archive---------14----------------------->

我们上次讨论了互斥体，但是我们还有一件事要讨论:条件变量。互斥为我们提供了一种保护共享状态的方法，并允许我们一次只为一个对应的共享状态运行一个线程。

![](img/912c8a22cfc240de4de9b5da8f91d963.png)

micha Parzuchowski 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 条件变量

如果我们使用互斥，我们等待一个拥有者线程来释放锁。然而，如果我们想等待一个特定的事件呢？例如，我们有一个共享状态 x = 10，我们想等到 x == 20。我们如何做到这一点？“条件变量”来了。顾名思义，这就像 if 语句中的一个条件，但是有一些额外的特性。

先说上面的例子。我们有 int x = 10，我们想等到 x == 20。我们不能每次都简单地读取 x 的值，因为 x 是一个共享状态，可能存在竞争条件。因此，我们必须为 x 获取一个相应互斥体的锁。假设我们获取了 x 的锁，现在做什么？我们读取 x 的值，如果不是 20，那么释放锁。

```
#include <thread>

int x = 10;
std::mutex x_m;

void InitXWhenXisTwenty(){
  x_m.lock(); // lock mutex for x to read the value of x
  while(x != 20){ // if x is not equal to 20
     x_m.unlock(); // unlock the mutex to let other threads to make x to 20
     x_m.lock(); // lock the mutex again to read the value of x and check the 
                 // while condition
  } 
  cout << "Finally x == 20, initialize it to 0" << endl;
  // Initialize x to 0
  x = 0; 
  x_m.unlock();
} 
```

如你所见，这是非常低效的。我们有一个繁忙的 while 循环，即使 x 不等于 20，它每次都会试图消耗 CPU。而不是等待线程每次都检查变量，我们应该把这个改成**另一个“使 x == 20”的线程应该告诉等待线程 x 现在是 20，这样你就可以开始工作了。这种事件驱动的架构正是 CV 允许我们做的。CV 给了我们三种方法:等待，信号，广播。**

## 等待

等待基本上就是等待那个条件变量，也就是等待某件事情发生。CV 的 wait()的好处是我们可以避免忙碌的等待。当我们调用 wait()时，它将等待线程放到条件变量的等待队列中。然后，稍后如果另一个线程调用 signal 或 broadcast 来唤醒等待的线程，那么这个线程就可以脱离等待队列，开始做一个工作(消耗 CPU)。当线程在 CV 的等待队列中时，它不会试图消耗 CPU。正如我们在上一篇文章中看到的，如果线程进入 CV 的等待队列，线程的状态就会变成“等待”。由于它没有处于就绪状态，调度程序不能直接将该线程置于“运行”状态，直到该线程变为“就绪”

那么当我们调用 wait 时会发生什么呢？当我们呼叫等待时，

1.  它首先**释放互斥锁**以允许另一个线程工作。
2.  调用者线程进入等待队列。
3.  稍后，一些其他线程唤醒这个线程，那么这个线程将变成“就绪”状态。
4.  如果调用者线程开始运行，它将试图**重新获取我们在步骤 1 中释放的互斥锁**。

这与我们对前面的 InitXWhenXisTwenty()函数所做的非常相似。我们只是释放锁，等到有人通知我们事件，然后重新获取锁来完成工作。需要注意的一点是， **CV 的等待是和互斥**相关联的！

让我们看看如何使用它。

```
#include <thread>

int x = 10;
std::mutex x_m;
cv twenty_cv;

void InitXWhenXisTwenty(){
  x_m.lock(); // lock mutex for x to read the value of x
  if(x != 20){ // if x is not twenty
    // remember we should have the lock of x_m, at the beginning of wait()
    // we release the lock of x_m 
    twenty_cv.wait(x_m); // Drop the lock and go to sleep.
  }
  // remember at this point, we acquired the lock of x_m
  // everytime we returns from wait(), we have the lock of that mutex
  cout << "Finally x == 20, initialize it to 0" << endl;
  // Initialize x to 0
  x = 0; 
  x_m.unlock();
}
```

看起来不错吧？实际上这并不完全正确。如果在调用者线程重新获得锁之前，某个其他线程先获得了锁，并将 x 修改为其他值，该怎么办？例如，假设另一个线程使 x == 20，并唤醒调用者线程。现在，调用方线程从“等待”状态中醒来，并试图重新获取锁。在这个调用方线程重新获得锁之前，其他一些线程先获得锁，并使 x == 21。现在，调用者线程获得锁并打印“最终 x == 20”，这是不正确的，因为 x == 21。**因此，我们应该将 if 改为“while”来再次检查条件。**

除此之外，我们还有另一个使用“while”的理由我们必须从 wait()中注意到的一点是，即使没有人唤醒调用者线程，它也会“虚假地唤醒”。

> `wait`使当前线程阻塞，直到条件变量被通知或虚假唤醒发生——cppreference.com

 [## 标准::条件 _ 变量::等待

### wait 导致当前线程阻塞，直到通知条件变量或发生虚假唤醒…

en.cppreference.com](https://en.cppreference.com/w/cpp/thread/condition_variable/wait) 

现在，看看代码。

```
void InitXWhenXisTwenty(){
  x_m.lock(); 
  while(x != 20){ 
    twenty_cv.wait(x_m); // Drop the lock and go to sleep.
    // it acquires the lock again, and check the while condition!
    // if x != 20, then it will go into loop again.
  }
  // now at this point we can guarantee that x == 20\. 
  cout << "Finally x == 20, initialize it to 0" << endl;
  x = 0; 
  x_m.unlock();
}
```

## 信号和广播

信号是唤醒等待线程的一种机制。它只会从所有等待 CV 的线程中唤醒一个线程。另一方面，广播将唤醒所有等待 CV 的线程。因此，我们应该在什么时候使用哪一个呢？

当我们知道所有等待的线程都可以取得进展时，我们应该使用 signal，因为只唤醒一个线程就足以取得进展。但是，如果我们不能确定所有等待的线程都能取得进展，我们应该使用广播。有可能我们使用了信号，而一个被唤醒的线程无法取得进展。

我们来看信号的例子。

```
void setXtoTwenty(){
  x_m.lock();
  x = 20; // makes x to twenty
  twenty_cv.signal(); // wakes only one thread that is waiting for this.
  x_m.unlock();
}
```

我们可以在这里使用 signal，因为我们知道所有等待“twenty_cv”的线程都可以做相应的工作。简而言之，所有等待“twenty_cv”的线程都是在等待 x 变成 20。

让我们看看这个例子。

```
void InitXWhenXisThirty(){
  x_m.lock(); 
  while(x != 30){ 
    twenty_cv.wait(x_m); // uses same cv as InitXWhenXisTwenty
  }
  cout << "Finally x == 30, initialize it to 0" << endl;
  x = 0; 
  x_m.unlock();
}
```

我们有一个线程正在等待 x == 30，但是它使用了与 InitXWhenXisTwenty()相同的 cv。现在，如果我们发出 signal()，那么它可能会唤醒这个线程，它正在等待 x == 30，我们无法取得我们想要的进展。在这种情况下，我们应该使用广播而不是信号。

让我们看另一个例子。假设我们有三个函数，depositDogeEther()、deposit 比特币()和 depositDoge()。此外，我们有一个解析事务的函数。每个存款功能都在等待相应密码的交易。如果我们使用广播，那么我们可以有一个单一的 CV，并让所有三个函数等待同一个 CV。然而，如果我们使用一个信号，我们应该有三个 CV，每个存款功能将等待特定的 CV。此外，通知函数将调用相应 cv 的信号。

让我们看看广播案例的简单代码。

```
mutex transaction_m;
cv transaction_cv;  // we have single mutex and single cv

void depositEther(){
  transaction_m.lock();
  while(number_of_new_transaction_for_ether <= 0){
    transaction_cv.wait(transaction_m);
  }
  ehter_account_balance += new_transaction_amount;
  transaction_m.unlock();
}

void depositBitcoin(){
  transaction_m.lock();
  while(number_of_new_transaction_for_bitcoin <= 0){
    transaction_cv.wait(transaction_m);
  }
  bitcoin_account_balance += new_transaction_amount;
  transaction_m.unlock();
}

void depositDoge(){
  transaction_m.lock();
  while(number_of_new_transaction_for_doge <= 0){
    transaction_cv.wait(transaction_m);
  }
  doge_account_balance += new_transaction_amount;
  transaction_m.unlock();
}
// all three functions are waiting for transaction_cv. 

void parseNewTransaction(transaction tx){
  transaction_m.lock();

  /* parse tx */

  new_transaction_amount = tx.amount; // update the tx amount

  if(tx_is_for_ether) number_of_new_transaction_for_ether++;
  else if(tx_is_for_bitcoin) number_of_new_transaction_for_bitcoin++;
  else if(tx_is_for_doge) number_of_new_transaction_for_doge++;

  // wake all threads up. Among all three, only one can make a progress
  transaction_cv.broadcast();
  transaction_m.unlock();
}
```

这有点低效，因为我们知道只有一个存放函数可以完成工作，但是我们唤醒所有的存放线程，这是不必要的。因此，最好使用 signal 并拥有多个 cv。

```
mutex transaction_m;
cv ether_tx_cv;  // we have three cv
cv bitcoin_tx_cv;
cv doge_tx_cv;

void depositEther(){
  transaction_m.lock();
  while(number_of_new_transaction_for_ether <= 0){
    ether_tx_cv.wait(transaction_m); // wait for the specific cv!
  }
  ehter_account_balance += new_transaction_amount;
  transaction_m.unlock();
}

void depositBitcoin(){
  transaction_m.lock();
  while(number_of_new_transaction_for_bitcoin <= 0){
    bitcoin_tx_cv.wait(transaction_m);
  }
  bitcoin_account_balance += new_transaction_amount;
  transaction_m.unlock();
}

void depositDoge(){
  transaction_m.lock();
  while(number_of_new_transaction_for_doge <= 0){
    doge_tx_cv.wait(transaction_m);
  }
  doge_account_balance += new_transaction_amount;
  transaction_m.unlock();
}
// all three functions are waiting for transaction_cv. 

void parseNewTransaction(transaction tx){
  transaction_m.lock();

  /* parse tx */

  new_transaction_amount = tx.amount; // update the tx amount

  if(tx_is_for_ether){ 
    number_of_new_transaction_for_ether++; 
    ether_tx_cv.signal(); // now, we wakes up that specific cv, and we know that
    // all threads waiting for this cv are waiting for ether tx and make a progress
  }
  else if(tx_is_for_bitcoin){
    number_of_new_transaction_for_bitcoin++;  
    bitcoin_tx_cv.signal();
  }
  else if(tx_is_for_doge){
    number_of_new_transaction_for_doge++;
    doge_tx_cv.signal();
  }
  transaction_m.unlock();
}
```