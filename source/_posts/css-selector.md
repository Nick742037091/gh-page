---
title: css选择器
date: 2019-10-24 21:41:27
categories:
  - 前端
tags:
  - css
  - 选择器
---

本文列出各种常用的css选择器。

>  以下为三种最基础的选择器。 
#### 元素选择器
```css
p{
  color: blue;
}
```
#### 类选择器
```css
.name{
  color: blue;
}
```

#### ID选择器
```css
#name{
  color: blue;
}
```

>  以下的选择器中元素、类和ID选择器可以互相替换。 

#### 后代选择器
```css
p a{
  color: blue;
}
```

#### 子选择器
* 只选择元素的直接后代

```css
#nav > a{
  color: blue;
}
```

#### 相邻同辈选择器
* 只选择元素的第一个相邻同辈元素

```css
#nav + a{
  color: blue;
}
```

#### 同辈选择器
* 选择元素的之后的所有同辈元素

```css
#nav ~ a{
  color: blue;
}
```


#### 通用选择器
* 用于初始化所有选择器(不过一般不这么做，而是通过元素选择器分别设置)。

```css
* {
  padding: 0;
  margin: 0;
}
```

* 与其他选择器组合，表示选择某个元素的所有子元素

```css
.title-block > * {
  color: red;
}
```

### 属性选择器

```css
/* 匹配属性是否存在 */
input[type]{
  color: red;
}
/* 匹配属性全等 */
input[type="submit"]{
  color: red;
}
/* 匹配开头 */
a[href^="http"]{
  color: red;
}
/* 匹配结尾 */
img[src$=".jpg"]{
  color: red;
}
/* 匹配某些字符 */
a[href*="about"]{
  color: red;
}
```

### 伪元素
* 可减少元素数量

```css
/* 选择首字符 */
.text::first-letter{
    color: red;
}
/* 选择首行 */
.text::first-line{
    color: red;
}
/* 开头插入内容 */
.text::before{
    content: "insert ";
    color: red;
}
/* 结尾插入内容 */
.text::after{
    content: " insert";
    color:red;
}
```

### 伪类

```css
/* 对于以下的a标签，下面的状态会覆盖上面的状态 */
/* 未访问过的链接 */
a:link{
  color:blue
}
/* 访问过的链接 */
a:visited{
  color:blue
}
/* 鼠标悬停和状态 */
a:hover,
a:focus{
  color:blue
}
/* 鼠标点击或者键盘回车选择状态 */
a:active{
  color:blue
}
/* 通过urll#号后面的内容找到对应id的元素，会显示的状态 */
.comment:target{
  color:red;
}
/* 反选 */
.text:not(first-letter){
  color: black;
}
```

### 结构化伪类

```css
/* 以下都是指选择子元素 */
/* 选择奇数序列 */
tr:nth-child(odd){
  background-color: green;
}
/* 选择偶数序列 */
tr:nth-child(even){
  background-color: green;
}
/* 选择第三个 */
tr:nth-child(3){
  background-color: green;
}
/* 选择倒数第三个 */
tr:nth-last-child(3){
  background-color: green;
}
/* 选择第1个，等同于nth-child(1) */
tr:first-child{
  background-color: green;
}
/* 选择最后1个，等同于nth-last-child(1) */
tr:last-child{
  background-color: green;
}
/* 通过计算公式选择，这里匹配4、7、10、13... */
tr:nth-child(3n+4){
  background-color: green;
}
/* 选择前3个 */
tr:nth-child(n-3){
  background-color: green;
}
```


### 表单伪类
```css
/* 选择没有required的input标签 */
input:optional{
  color: grey;
}
/* 选择输入有效电子邮件地址的input标签 */
input[type="email"]:valid{
  color: grey;
}
/* 选择输入无效电子邮件地址的input标签 */
input[type="email"]:invalid{
  color: red;
}
```

#### 层叠优先级
> important > 行内样式 > ID选择器 > 类、伪类和属性选择器 > 元素选择器和微元素选择器
