---
title: css flex布局
date: 2019-12-17 23:16:39
categories:
  - 前端
tags:
  - css
  - flex布局
---

本文主要介绍 css 的flex布局。
<!-- more -->
> 注：IE9及更早版本的IE不支持flex布局。

## 声明flex布局
```css
  display:flex
```

## 指定主轴方向（与主轴方向垂直的为辅轴方向）
```css
  /*支持row（水平方向,默认值）、column（垂直方向）、row-reverse（水平反向）、
  column-reverse（垂直反向）  */
  flex-direction: row;
```

## 主轴方向的排布
```css
  /* 默认值。若主轴为水平方向，表示排布在左侧；若主轴为垂直方向，表示排布在顶部。 */
  justify-cotent: flex-start;
  /* 若主轴为水平方向，表示排布在右侧；若主轴为垂直方向，表示排布在底部。 */
  justify-cotent: flex-end;
  /* 表示排布在主轴方向上的中间 */
  justify-cotent: center;
  /* 表示将多余的空间等分后分配到项与项之间 */
  justify-cotent: space-between;
  /* 表示将多余的空间等分分配到项与项两侧 */
  justify-cotent: space-around;
  /* 利用auto特性，使某一个右侧的空白拉伸至最大值，可实现左右排列，中间留空的效果。
  其他margin属性类似。 */
  margin-right:auto;
```

## 辅轴方向的对齐
```css
  /* 默认值。表示辅轴方向的尺寸拉伸至最大值。align-items为其他值时，
  会取消拉伸效果至可包含内部元素。 */
  align-items: stretch;
  /* 若主轴为水平方向，表示位于顶部对齐；若主轴为垂直方向，表示对齐位于左侧对齐。 */
  align-items: flex-start;
  /* 若主轴为水平方向，表示位于底部对齐；若主轴为垂直方向，表示对齐位于右侧对齐。 */
  align-items: flex-end;
  /* 若主轴为水平方向，表示相对于垂直方向中间对齐；
    若主轴为垂直方向，表示相对于水平方向中间对齐。 */
  align-items: center;
  /* 若主轴为水平方向，表示相对于行内文本基线对齐； 
    若主轴为垂直方向，和flex-start效果相同。*/
  align-items: baseline;
  /* 只适用于设置子项，支持flex-start/flex-start/center，
    效果与align-items类似，但只作用于单独子项。 */
  align-self: flex-start;
```

