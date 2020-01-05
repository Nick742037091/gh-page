---
title: css盒模型
date: 2019-10-26 22:28:44
categories:
  - 前端
tags:
  - css
  - 盒模型
---

本文主要介绍 css 盒模型的一些相关属性。

<!-- more -->

### width 和 height

- 默认情况下，元素盒子的 width 和 heigh 指的是内容盒子，也就是可渲染区域的宽度和高度。此时添加边框和内边距不会影响内容盒子的大小，但是会导致整个元素盒子扩大，要注意此时若想元素盒子的宽高和添加边框和内边距之前一致，要通过 width 和 height 的值来实现。

### padding 和 margin

- padding 为内边距，margin 为外边距。
- 可用 px、em、rem 和百分比设置。宽度、高度百分比都是相对于包含块。
- 可用 padding-bottom + absolute 布局实现元素盒子的固定宽高比。

### box-sizing

- 默认值为 content-box，即 width 和 height 设置的是内容盒子的宽高。
  <br/>![](/medias/css-box/1.png)

* 设置为 border-box，width 和 height 就包括了内边距和边框的宽度。
  <br/>![](/medias/css-box/2.png)

### 块级盒子

- div、p、h1、article、section 等属于块级元素，显示为块级盒子的形式。
- 沿垂直方堆叠，垂直方向上的间距由它们的垂直内边距、边框和外边距决定。

### 行内盒子

- strong、span 等属于块级元素，显示为行内盒子的形式。
- 无法设置 width 和 height，通过设置 line-height 能间接设置行内盒子的高度。
- 沿文本水平排列，会随文本的换行而换行。它们之间的水平间距由水平内边距、边框和外边距决定。垂直方向上的内边距、边框和外边距不影响高度(可能会看到渲染的内容不代表实际的高度)。

### display

- 块级盒子为 display: block。
- 行内盒子为 display: inline。
- display: inline-block 可以实现行内布局，同时可以像块级盒子一样设置宽度、高度和垂直方向上的内边距、边框和外边距。
- display: none 表示为不生成盒子，因此也就不会显示出来，不占用文档中的空间。
- display: flex 可以设置为 flex 布局。
- display: grid 可以设置为网格布局。

### 外边距折叠

- 是常规块盒子的的一种机制，行内盒子、浮动盒子和绝对定位盒子不会发生外边距折叠。
- 相同层级的块盒子互相接触的外边距发生折叠，折叠后的边距高度等于两则中较大的边距。
  <br/>![](/medias/css-box/3.png)
- 父子层级的块盒子互相接触的外边距发生折叠，折叠后的边距高度等于两则中较大的边距。
  <br/>![](/medias/css-box/4.png)
- 空元素的上下边距会发生折叠，折叠后的边距高度等于两则中较大的边距。
- 外边距折叠是为了解决多个文本段落最顶部和最低部的外边距只有中间段落边距一半的问题。

### 静态定位

- position:static，默认定位方式，安按照文档流进行排布。
- 包含块是最近的父元素

### 相对定位

- position:relative，可以通过设置 top、right、bottom 和 left 属性实现位置的偏移，但是仍然会在文档流中占有原来的空间。
- 包含块是最近的父元素

### 绝对定位

- position:absolute，可以通过设置 top、right、bottom 和 left 属性实现位置的偏移，脱离了文档流，不再占有原来的空间。
- 可以通过 z-index 设置盒子层叠的顺序，z-index 值大的会覆盖为值小的上面。
- 包含块是相对于距离它最近的非静态布局父元素，根据包含块进行定位，因此会随着滚动轴的滚动而滚动。

### 固定定位

- position:fixed，可以设置 top、right、bottom、left 和 z-index 属性，和绝对定位类型类似
- 包含块是视口（viewport），根据视口进行定位，因此不会随着滚动轴的滚动而滚动。

### 浮动定位

- 通过设置 float 属性实现的定位(left、right 等，默认为 none)，会脱离文档流。
- 包含块是直接父元素，可布局区域是父布局的内容块。
- 存在多个浮动元素时，会根据浮动方向(left 或者 right)，按照顺序排列布局。例如，代码中元素出现的顺序是 box1、box2、box3，float 为 left 时实际布局为 box1、box2、box3；float 为 right 时实际布局为 box3、box2、box1。
  ![](/medias/css-box/5.png)
- 当 float: right 之前出现文档内的非 float 元素时，会导致换行。
- 浮动元素几乎不占据文档流空间，但是在遇到文本的时候，文本不会布局在浮动元素之下，而是避开浮动元素，为其流出空间，从而形成文字环绕在浮动元素四周的效果。
  <br/>![](/medias/css-box/6.png)
- 要阻止文本环绕在浮动元素四周，需要给包括文本的盒子设置 clear 属性，其值可为 left、right、both 和 none，用于指定盒子的那一侧不该紧挨着浮动元素。浏览器会根据浮动元素的高度，给盒子添加足够的 margin-top，将文本推到浮动元素之下。由于浮动元素脱离了文档流，若父元素只包含浮动元素，浮动元素无法将父元素撑开，导致父元素的高度为零。利用 clear 属性，可额外添加一个设置了 clear 属性的空元素，实现将父元素高度设置为浮动元素高度的效果。一般通过为::after 伪元素添加 clear 属性来实现。

  ```css
  .p-block::after {
    content: '';
    display: block;
    clear: both;
  }
  ```

### 块级格式化上下文(BFC)

- 设置为块级格式化作用域的方式
  1. 设置 display 为 inline-block、flex 相关、table 相关和 grid 相关的类型
  2. 设置 float 不为 none
  3. 设置 position 为 absolute 或者 fixed
  4. 设置 overflow 不为 visible
- 浮动不会影响其他 BFC 中的布局，因此元素设置为 BFC,会有以下效果：
  1. 必须自动包含浮动元素，可以使浮动子元素自动撑开父元素。
  2. 不会延伸到相邻的浮动元素底部。
- 清除浮动只能清除同一 BFC 在它前面的元素的浮动。
- 外边距折叠只会发生在同一 BFC 的块级元素之间。

```html
<template>
  <div id="app">
    <div class="top-block">
      <div class="float-block"></div>
      <div class="text-block">xxxxx xxxxx xxxxx xxxxx</div>
    </div>

    <div class="bottom-block"></div>
  </div>
</template>

<style>
  #app {
    width: 400px;
  }
  .top-block {
    overflow: auto;
  }
  .float-block {
    float: left;
    width: 300px;
    height: 50px;
    background-color: red;
  }
  .text-block {
    overflow: auto;
  }

  .bottom-block {
    width: 300px;
    height: 100px;
    background-color: green;
  }
</style>
```
