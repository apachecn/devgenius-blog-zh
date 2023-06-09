# 关于 JS 中的 localStorage

> 原文：<https://blog.devgenius.io/all-about-localstorage-in-js-4760dbff0b0d?source=collection_archive---------3----------------------->

![](img/ce0dfe275e2b2bc1e175baff25cee5b4.png)

Maksym Kaharlytskyi 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 本地存储在内存中

LocalStorage 是一个 web 存储对象，用于将来自网站的数据存储到用户的本地计算机上，这意味着存储的数据跨浏览器会话保存。数据可以以键-值对的形式无限期存储，没有截止日期。因此，即使您关闭了浏览器，当您的浏览器需要再次访问数据时，您的数据仍然存在。这与 sessionStorage 属性不同，session storage 属性只存储一个会话的数据，一旦关闭浏览器选项卡，数据就会立即丢失。

在基于 Chromium(Chrome)的浏览器中，数据保存在 SQLite 文件中，该文件位于/AppData/Local/Google/Chrome/user data/Default/Local Storage 的子文件夹中。由于它存储在您的个人电脑存储器中，这意味着您无法在所有设备上使用它，因此如果您将笔记本电脑留在家中，您将无法在另一台电脑上访问该本地存储器。

值得注意的是，所有主流浏览器(Internet Explorer 和 Chrome)的本地存储空间都被限制在 5MB 以内，而 Firefox 等特定浏览器的本地存储空间被限制在 10MB 以内。理想情况下，localStorage 不应该用于存储敏感信息，如果您要存储敏感信息，请确保您对加密敏感数据进行了研究。我个人最喜欢的是 Ruby on Rails 上的宝石“bcrypt”。尽管 localStorage 是一个伪数据库，但它不能替代基于服务器的数据库，因为这些数据只存储在用户的浏览器和个人计算机上。

localStorage 属性是只读属性，大多数浏览器只能在内存中存储字符串。这造成了一个有趣的问题，当你试图存储一个布尔值，如'真'，它会存储为字符串！因此，如果您需要检索该值，并尝试将该值与另一个值进行比较，您将会遇到一些问题。对此的解决方案是使用 JSON.parse()将字符串解析为布尔值。

## 使用本地存储

LocalStorage 有五种不同的方法。

1.  setItem("key "，" value "):将键和值添加到 localStorage

```
//to store datalocalStorage.setItem('Name', 'Teodoro');
```

2.getItem("key "):从 localStorage 获取项目

```
//retrieve datalocalStorage.getItem('Name');
```

3.removeItem("key "):从 localStorage 中移除项目

```
//clear a specific itemlocalStorage.removeItem('Name');
```

4.clear():完全清除本地存储

```
//clear the whole data stored in localStoragelocalStorage.clear();
```

5.key(index):检索传递的索引的键

```
//retrieve the key from localStoragelocalStorage.key(0);
```