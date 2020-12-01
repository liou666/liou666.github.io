---
layout: post
title: 行内块元素之间出现空白间隙的原因及解决办法
subtitle:
date: 2020-08-24
author: liou
header-img:
catalog: true
tags:
  - HTML
typora-root-url: ..
---

### 行内块元素之间产生空白间隙的原因

元素被当成行内元素排版的时候，元素之间的空白符（空格、回车换行等）都会被浏览器处理，根据 `white-space` 的处理方式（默认是 `normal`，合并多余空白），原来 `HTML` 代码中的回车换行被转成一个空白符，所以元素之间就出现了空隙。这些元素之间的间距会随着字体的大小而变化，当行内元素 `font-size:16px` 时，间距为 `8px`。

### 去除空白间隙的方法

###### 去除元素间的空白

通过将上一个元素的闭合标签与下一个元素的开始标签写在同一行，可以去除元素间的空白，或者将两个`inline-block` 元素间加上空白注释，或者不写元素的闭合标签等，例如这么写：

```html
<ul>
  <li>one</li>
  <li>two</li>
  <li>three</li>
</ul>
<!-- or -->
<ul>
  <li>one</li>
  <!--
    -->
  <li>two</li>
  <!--
    -->
  <li>three</li>
</ul>
```

###### 父元素设置 font-size 为 0，子元素单独再设置字体大小

```css
.father {
  font-size: 0;
}
.son {
  font-size: 16px;
}
```

###### 设置 margin-right 为负值

用 `margin` 负值来抵掉元素间的空白，不过 `margin` 负值的大小与上下文的字体和文字大小相关，并且**同一大小的字体，元素之间的间距在不同浏览器下是不一样的**，如：`font-size:16px` 时，Chrome 下元素之间的间距为 `8px`,而 Firefox 下元素之间的间距为 `4px`。所以这个方法并不通用，也相对比较麻烦，因此**不太推荐使用**。

###### 给 inline-block 元素加 float 或者 flex

让行内块元素浮动起来，或者给父盒子加上 display: flex; 都可以解决空白间隙的问题
