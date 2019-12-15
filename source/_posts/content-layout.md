---
title: css内容布局
date: 2019-12-15 22:16:41
categories:
  - 前端
tags:
  - css
  - 内容布局
---

本文主要介绍 css 的内容布局。

<!-- more -->

z-index

1. 非静态定位的元素会根据它们在代码树中的深度以此叠放，可以通过 z-index 设置叠放次序。
2. z-index 默认值为 auto，叠放顺序相当于元素 z-index:0，z-index 非 auto 时，会在元素上产生堆叠上下文。在一个堆叠上下文内部，z-index 的大小不会影响其他堆叠上下文的元素。

非行内布局实现水平布

1. 浮动布局实现
2. 行内块元素实现

```html
<template>
  <div>
    <img
      src="https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_92x30dp.png"
    />
    <div class="info">
      <div>标题</div>
      <div>描述</div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .info {
    display: inline-block;
  }
</style>
```

3. 表格属性实现

```html
<template>
  <div class="parent">
    <div class="title">标题1</div>
    <div class="title">标题2</div>
    <div class="title">标题3</div>
    <div class="title">标题4</div>
  </div>
</template>

<style lang="scss" scoped>
  .parent {
    width: 100%;
    display: table;
    /*  默认等比分配宽度。fixed设置按照第一行宽度分配表格宽度 */
    /* table-layout: fixed; */
    background-color: red;
    .title {
      display: table-cell;
    }
  }
</style>
```

4. flex 布局

行内块元素的居中

1. 行内块元素的水平垂直居中

> 通过 vertical-align 可设置图片和行内块元素相对于行内元素的对齐方式

```html
<template>
  <div class="parent">
    <img
      class="avatar"
      src="https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_92x30dp.png"
    />
    <div class="info">
      <div>标题</div>
      <div>描述</div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .parent {
    background-color: red;
    /* 使行内元素水平居中 */
    text-align: center;
    .avatar {
      /* 行内图片垂直居中 */
      vertical-align: middle;
    }
    .info {
      display: inline-block;
      /* 行内元素垂直居中 */
      vertical-align: middle;
    }
  }
</style>
```

2. 在容器元素中水平垂直居中

> 当容器高度不等于行内元素高度时，通过添加一个高度等于容器高度的行内伪元素，使其相对于行内元素垂直居中，从而实现整体的垂直居中。

```html
<template>
  <div class="parent">
    <img
      class="avatar"
      src="https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_92x30dp.png"
    />
    <div class="info">
      <div>标题</div>
      <div>描述</div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .parent {
    /* 指定容器高度 */
    height: 100px;
    background-color: red;
    /* 使行内元素水平居中 */
    text-align: center;
    /* 添加高度为100%伪元素，使其他行内元素基于该元素居中。 */
    &::before {
      content: '';
      display: inline-block;
      vertical-align: middle;
      height: 100%;
    }
    .avatar {
      vertical-align: middle;
    }
    .info {
      display: inline-block;
      vertical-align: middle;
    }
  }
</style>
```
