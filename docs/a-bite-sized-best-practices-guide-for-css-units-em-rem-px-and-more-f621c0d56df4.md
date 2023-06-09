# CSS 单元的最佳实践指南:Em、Rem、Px 等等

> 原文：<https://blog.devgenius.io/a-bite-sized-best-practices-guide-for-css-units-em-rem-px-and-more-f621c0d56df4?source=collection_archive---------7----------------------->

## 在你的响应式网页设计中使用 CSS 单元如 em，rem，px 等的初学者指南。

![](img/789c8146a72555d68ad0abd4865a2503.png)

## 绝对单位

绝对单位主要分为两类:像素(px)和其余(cm、mm、in)。绝对单位有利于布局精确的屏幕尺寸，但它们不会随视口缩放，所以它们对于在平板电脑和手机上创建响应式设计来说不太好。

你可能会在日常生活中认出厘米、毫米和英寸等单位。这些单元，就像它们在现实生活中的对应物一样，应该只在设计印刷品(物理设计)时使用。一般来说，避免使用非像素绝对单位，除非您对它们有特殊的用途。

*   **像素**(像素)
*   还有 pt，cm，mm，in

⭐ **最佳实践**:虽然我建议你**如果有更好的选择**就少用 px 单元，但它们有时在**指定特定的宽度、高度和字体大小**时会很有用。

## 百分比

百分比主要用于**宽度**。它们使得计算子元素应该占父对象空间的百分比变得非常容易。例如，检查下面的 HTML，其中“parent”是两个子容器的父容器:

```
<div class=”parent”>
   <div class=”child-one”></div>
   <div class=”child-two”></div>
</div>
```

默认情况下，我的父 div(下面的红色块)的宽度是 100%。通过声明 child-one 的宽度为 60%，child-two 的宽度为 40%，结果将是:

![](img/f61e4f948204aa0119d88fd202bc258b.png)

## 相对单位

这些单元通常用于实现响应式设计，因为它们随页面的不同元素而缩放。这意味着它们在显示器、平板电脑和手机上会很好看！作为一名反应灵敏的网页设计师，em 和 rem 单元应该是你最好的朋友。

*   相对于字体大小的单位。比如 **em** 、 **rem** 、ch、ex。
*   相对于视口的单位，如 **vh** 、 **vw** 、vmin 和 vmax。

# 关于 Em 和 Rem 要知道的事情

## Em 单元:

*   当用于**字体大小**属性时，em 是相对于父字体大小的**。**
*   1em 不会改变任何事情。意思是复制父母的字体大小。
*   所以 120% em 相当于父字体大小的 120%。
*   ⚠️ **一个问题** : **如果** **你改变了父元素的字体大小，你会影响到那个父元素的所有子元素**的所有后续字体大小。因此，通过将 em 单位应用于层次结构中的子元素，如果您更改根字体大小，可能会产生一些天文数字的缩放效果。
*   ⭐ **最佳实践** : **Em 非常适合设置填充、边距和宽度**。这是因为**当你把 em 用于除了字体大小之外的任何东西时，它与父元素无关。**是相对于自己的字号。
*   👍**因此，如果在 width 属性上使用 em 单位，宽度将随该元素的字体大小**缩放，而不是随父元素的字体大小缩放。

## Rem 单位:

*   **rem 单元不是相对于父对象，而是相对于根对象**:HTML 元素。
*   您可以**更改 HTML 元素的字体大小**来更改所有使用 rem 单位的对象的字体大小。
*   ⚠️ **一个问题**:在 HTML 元素中设置字体大小**是不需要的**。它偶尔会造成问题，所以要谨慎使用。
*   ⭐ **最佳实践** : Rem 单元避免了 em 单元的缩放问题，因此在为响应式网页设计设置字体大小时，它们是一个很好的选择。