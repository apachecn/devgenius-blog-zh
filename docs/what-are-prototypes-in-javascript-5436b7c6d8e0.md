# JavaScript 中的原型是什么？

> 原文：<https://blog.devgenius.io/what-are-prototypes-in-javascript-5436b7c6d8e0?source=collection_archive---------11----------------------->

不要和 JavaScript 原型库混淆，这篇文章是关于原型本身的。

![](img/fd7e8ec79e0d57bcbf6bb180ea7394d3.png)

[斯坦利戴](https://unsplash.com/@stanleydai?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/prototype?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

原型是一种对象属性，它允许对象之间继承共同的功能。所有 JavaScript 对象都有从`Object.prototype`继承属性和方法的能力。甚至原型本身也有继承更多属性的能力，又名另一个原型，简称`prototype chaining`。

下面是一个正在使用的原型示例:

原型是编程中非常有用和强大的工具。它们使您能够一次在特定对象的所有实例上添加属性和定义方法。当以这种方式完成时，它占用更少的内存，因为它只在原型上存储一次，同时仍然允许每个实例访问它。如果您决定不使用原型，而是将方法添加到构造函数中，那么每次创建一个新的对象实例时，它在创建之前都不知道这些属性。第二，会创建重复的函数，从而占用更多的内存，最终降低程序速度。随着应用程序的增长，创建的实例数量也会增加，因此使用原型是降低成本的理想选择。

原型对象已经可以使用许多不同的方法，这些方法是可以实现的有用工具。这些方法中的一些是`.toString()`。`valueOf()`、`.isPrototypeOf()`等。

## Object.create()

`Object.create()`通常用于创建可以明确定义的原型。如果你用关键字`new`创建一个新对象，你就不能控制这个对象的属性。`Object.create()`函数接受两个参数:第一个参数是原型对象，第二个参数是具有您希望新创建的对象继承的特定属性的对象。这是比使用`new`关键字更好的创建对象的方式，因为不需要调用或声明构造函数。这也有助于使您的程序更加动态，因为您将基于所提供的参数创建具有不同原型的对象。

在 JavaScript 编程中，原型可能是一个很难理解的概念，但是一旦你开始使用它们，你将能够产生更快更有效的应用程序。