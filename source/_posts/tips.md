---
title: "🎊Q&A 一些零碎的知识点🤖"
date:
updated:
tags: 前端
categories: 经验
keywords:
description:
top_img: https://images.unsplash.com/photo-1693825383079-32a0b83a442b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2573&q=80
comments:
cover: https://images.unsplash.com/photo-1693825383079-32a0b83a442b?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2573&q=80
toc:
toc_number:
toc_style_simple:
copyright: false
copyright_author:
copyright_author_href: false
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:

---

### 1：div或者a标签的高度总是比里面的img高度多了6px问题
`a元素` 或者 `div元素`下有一个匿名文本，这个文本外有一个匿名行级盒子，它有的默认`vertical-align`是 `baseline`的，而且往往因为上文`line-height`的影响，使它有个`line-height`，从而使其有了高度，因为`baseline`对齐的原因，这个匿名盒子就会下沉，往下撑开一些距离，所以把a撑高了。

解决办法一是消除掉匿名盒子的高度，也就是给`a设置line-height:0`或`font-size:0`;

解决办法二是给两者`vertical-align:top`，让其`top`对齐，而不是`baseline`对齐

解决办法三是给`img`以`display:block`，让它和匿名行级盒子不在一个布局上下文中，也就不存在行级盒。

`img`是行内元素，默认`display: inline`; 它与文本的默认行为类似，下边缘是与基线对齐，而不是紧贴容器下边缘。将`display`设置为`block`即可消除上面说的几个像素的差别。

### 2：隐藏滚动条滚动
```css
.div {
    overflow-x: hidden;
    overflow-y: auto;
}
  
.div::-webkit-scrollbar {
    display: none;
}
```