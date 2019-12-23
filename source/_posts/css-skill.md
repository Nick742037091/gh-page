---
title: css技巧
date: 2019-12-22 16:03:55
categories:
  - 前端
tags:
  - css
  - 技巧
---


本文列举列一下css常用技巧。

<!-- more -->


## 水平垂直居中


```css
.parent {
  position: relative;
  .son {
    position: absolute;
    top: 0;
    left: 0;
    transform: translate(-50%, -50%);
  }
}
```

```css
.parent {
  position: relative;
  .son {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    /* 宽高是必须的，否则会扩散到容器尺寸 */
    width: 100px;
    height: 100px;
  }
}
```

```css
/* 相对视窗水平垂直居中 */
.son {
  position: fixed;
  margin: 50vh 50vw;
  transform: translate(-50%, -50%);
}
```


