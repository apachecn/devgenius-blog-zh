# 重构时我们可能会遇到的问题

> 原文：<https://blog.devgenius.io/problems-that-we-may-run-into-when-refactoring-96ba081cabe?source=collection_archive---------18----------------------->

![](img/2f9333421e6920f7b9f0844b2aebeaf0.png)

Jorge Franganillo 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

重构是我们在开发软件时经常要做的事情。因此，我们必须了解它。

在本文中，我们将看看重构时可能会遇到的问题。

# 更改界面

当我们改变一个接口时，这意味着任何实现该接口的东西和任何调用实现该接口的东西的东西都必须改变。

拥有接口的全部意义在于，我们不必担心某些东西的底层实现。

我们可以为重构做一些改变。更改方法名是可以的，因为它们可以一次自动更改。

然而，如果我们改变一个已经发布的接口，那么我们必须保持接口的新旧版本，以避免破坏任何现有的代码。

如果我们改变了函数的签名，那么我们要么调用旧的函数，要么调用新的函数，这取决于使用了哪个接口。

我们应该尝试引用这两个接口，看看代码是否仍然可以在新旧接口上工作。

我们可以弃用旧界面，这样我们就不会引入突破性的变化，但让旧界面的用户知道旧界面将被弃用，并在未来被删除。

# 难以重构的设计变更

有些设计变更很难重构。

这可能意味着我们必须从头开始设计那部分程序，并编写干净的代码来清理代码。

# 什么时候不应该重构？

有些时候我们不应该重构。如果代码太乱，无法重构，我们可能不得不从头开始编写代码。

那样的话，从头开始可能更容易些。

我们应该重写的一个明显迹象是当当前代码不能按预期工作时。我们可能会发现它充满了无法稳定的错误。

如果我们想要重构，代码必须大部分正确工作。

我们也可以考虑将一大段代码重构为具有强封装的组件。

这样，我们可以一次重构或重建一段代码。由于这种松散耦合，修改代码要比保留现有代码容易得多。

如果我们接近最后期限，那么我们不应该重构。重构总是有机会破坏代码。

未完成的重构是技术债。大多数公司需要债务才能正常运转。

然而，我们不能让它失控，否则公司会破产的。

在软件开发的情况下，我们通过重构代码来管理债务。

一旦我们交付了代码，我们就可以重构了。

# 重构和设计

一起重构和设计。我们应该从一开始就很好地设计我们的代码，这样我们就不必进行太多的重构。

在我们糟糕地设计了代码之后进行重构并不是最有效地利用我们的时间。

我们都遇到过糟糕代码的问题，在我们完成糟糕的设计之后。

然后我们要么不得不做大量的重构，要么不得不从头重写糟糕的部分。

此外，我们不应该将我们的软件构建得过于灵活。灵活的解决方案比不灵活的更难维护。

如果我们不需要灵活性，那么我们就不应该把它放进去。

灵活性花费我们更多的时间来构建，因为它增加了我们代码的复杂性。

这让大家都很沮丧。

即使我们现在没有实现灵活的解决方案，如果需要，我们仍然可以在以后的代码中增加灵活性。

重构可以在不牺牲灵活性的情况下带来简单的设计。

设计过程可以更容易，压力也更小，因为我们不必为现在不需要的所有灵活性而设计。

我们总是可以重构我们的代码来增加我们需要的灵活性。

因此，我们应该设计易于重构的代码。

![](img/a98236e22824bf8798bbe1dfff8b0cfb.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由[alony Haust](https://unsplash.com/@aiony?utm_source=medium&utm_medium=referral)拍摄的照片

# 结论

我们遇到的问题包括改变界面和增加灵活性。

更改接口意味着更改实现接口和使用接口的任何东西的实现。

因此，我们必须保留新旧接口，摒弃旧接口，以避免破坏人们代码的变化。

此外，我们必须设计代码，使它们易于重构，以便我们可以在以后对它们进行更改。