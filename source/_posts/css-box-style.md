---
title: css盒样式
date: 2019-11-02 15:25:28
categories:
  - 前端
tags:
  - css
  - 盒样式
---

本文主要介绍 css 盒子的一些常用样式。

<!-- more -->

### 背景颜色

```css
.box {
  /*  */
  background-color: #336699;
  /* 十六进制表示法缩写，要求每组的两个数字相同 */
  background-color: #369;
  /* rgb表示法，三个参数分别表示r/g/b的十进制数 */
  background-color: rgb(51, 102, 153);
  /* rgba表示法，比rgb表示法多了最后一个表示颜色透明度的参数(0~1) */
  background-color: rgb(51, 102, 153, 0.5);
}
```

### 不透明度

```css
.box {
  /* 0为全透明，1为完全不透明 */
  opacity: 0.5;
}
```

### 背景图片

- background-image

  ```css
  .box {
    /* 背景图片默认会覆盖在背景颜色上面，显示尺寸为原始图片尺寸，
    若盒子尺寸超过图片尺寸，背景图会在水平和垂直方向上平铺(不能
    刚好容纳图片时会对图片剪切)。*/
    background-color: red;
    background-image: url('./assets/logo.png');
    /* url可以为相对地址、绝对地址和base64值，
    相对地址若以/开头,表示相对于网址根地址。 */
    background-image: url('/assets/logo.png');
    background-image: url('data:image/jpeg;base64,xxxxxxxx');
    /* 支持的图片类型有jpeg、png、gif、svg和webp。 */
    background-image: url('/assets/logo.svg');
  }
  ```

- background-repeat

  ```css
  .box {
    /* 背景图平铺属性，可为repeat(水平和垂直方向进行平铺)、
    repeat-x(水平方向进行平铺)、repeat-y(垂直方向进行平铺)
    和no-repeat(不平铺)。 */
    background-repeat: repeat;
  }
  ```

- background-position

  ```css
  .box {
    /* 背景图位置，可以用像素、em/rem、百分比和关键字。*/

    /* 像素和em/rem是相对于左侧和顶部的距离。 */
    /* 相对于左侧20px，顶部30px，见图1。 */
    background-position: 20px 30px;

    /* 百分比指的是距离图片左侧x%和顶部y%的电和距离盒子左侧x%和顶部y%的点重合。 */
    /* 见图2 */
    background-position: 20% 30%;
    /* 设置图片位于盒子中间。 */
    background-position: 50% 50%;

    /* 关键字水平方向可选值为left/center/right,垂直方向可选值为top/center/bottom。 */
    /* 设置图片位于盒子左上侧。 */
    background-position: left top;
    /* 可在关键字之后额外添加相对距离(像素/em/rem/百分比)。 */
    /* 设置图片位于盒子距离右侧20px, 距离底部30%的高度。 */
    background-position: right 20px bottom 30%;

    background-repeat: no-repeat;
  }
  ```

  图 1
  ![](/medias/css-box-style/1.png)
  图 2
  ![](/medias/css-box-style/2.png)

- background-clip
  ```css
  .box {
    /* 背景颜色和背景图的渲染区域，可选值为border-box（默认值，渲染到边框）、
    padding-box(渲染到内边距)和content-box（渲染到内容区域）。 */
    background-clip: padding-box;
  }
  ```
- background-origin
  ```css
  .box {
    /* 背景图的渲染起始点，可选值为padding-box(默认值，内边距区域的左上角) 、
    border-box（边框区域的左上角）、和content-box（内容区域左上角）。
    背景颜色默认渲染起点是border-box，不可修改。 */
    background-origin: content-box;
  }
  ```
- background-attachment
  ```css
  .box {
    /* 背景图附着模式，可选择为scroll（默认）、fixed和local。 
    scroll指随着盒子父元素的滚动而滚动；fixed指随着盒子父元素的规则，
    背景图相对于视窗的位置不移动，原来位于盒子下面的元素会覆盖在背景图之上；
    local指当盒子本身是可滚动区域时，背景图会随局部区域滚动(默认是不移动的)。 */
    background-attachment: fixed;
  }
  ```  

- background-size
  ```css
  .box {
    /* 指定背景图的大小，可设置为像素、百分比、auto和关键字。
    像素是固定大小，大于盒子尺寸会被裁剪。百分比是指相对于盒子的长宽，
    一般情况下是一边设置为百分比，一边设置为auto， 以保持原始长宽比。
    关键字有contain和cover，contain是指在保持宽高比的同时，尽可能
    显示整张图片，相当于短边设置100%，长边设置auto; contain是指在
    保持宽高比的同时，尽可能铺满盒子，相当于长边设置100%，短边设置auto; */
    background-size: 200px 300px;
    /* 保持宽高比，宽度占盒子80%。 */
    background-size: 80% auto;
  }
  ```  

### 未完待续...
