---
title: 🎯Web 接口 InterSectionObserver API
date: 
updated:
tags: [JavaScript, Tips]
categories: [JavaScript]
keywords:
description:
top_img: https://yh-blog.oss-cn-beijing.aliyuncs.com/mailchimp-lsdA8QpWN_A-unsplash.jpg
comments:
cover: https://yh-blog.oss-cn-beijing.aliyuncs.com/mailchimp-lsdA8QpWN_A-unsplash.jpg
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:

---

> 不需要通过监听滚动条去判断当前视口与dom的相对位置，就能轻易的判断出当前元素是否在可视范围内

前端可以使用 Intersection Observer API 来判断一个元素是否在视口范围内。
Intersection Observer API 可以观察指定元素与其祖先元素或浏览器视口的交叉状态，并提供回调函数来处理这些交叉状态。
要使用 Intersection Observer API，首先需要创建一个 IntersectionObserver 对象。该对象接受一个回调函数作为参数，每当被观察元素的可见性发生变化时就会被调用。回调函数接受一个参数 entries，它是一个数组，包含所有被观察元素的交叉状态信息。
具体来说，要判断一个元素是否在视口范围内，可以通过以下步骤：

1. 创建一个 IntersectionObserver 对象，并传入回调函数。
2. 使用该对象的 observe 方法观察目标元素。
3. 在回调函数中处理交叉状态信息，判断目标元素是否与视口发生交叉。

例如，下面是一个使用 Intersection Observer API 判断元素是否在视口范围内的示例代码：
```javascript
const element = document.querySelector('#target');

const options = {
  root: null,
  rootMargin: '0px',
  threshold: 1.0
};

const observer = new IntersectionObserver((entries) => {
  if (entries[0].isIntersecting) {
    console.log('Element is in viewport');
  } else {
    console.log('Element is not in viewport');
  }
}, options);

observer.observe(element);

```
> 其中，options 中的 root 属性指定了根元素，默认为浏览器视口；rootMargin 属性指定了根元素的外边距；threshold 属性指定了目标元素与根元素交叉的比例，取值范围为 0.0 到 1.0。在这个示例中，我们将 threshold 设置为 1.0，表示目标元素完全出现在视口范围内时才算交叉。

