---
title: html语义化
date: 2019-10-24 20:05:26
categories:
  - 前端
tags:
  - html5
  - 语义化
---
  html5中加入了一些语义化标签，来更清晰的表达文档结构。使用这些为了能够让开发者或是爬虫读懂各个模块的语义化内容。语义化标签使用没有严格的要求，本文只是阐述一些语义化标签的常用用法。
  * [掘金](https://juejin.im/)前端页面就大量使用了语义化标签。
  * [Element组件](https://element.eleme.cn/#/zh-CN/component/container)也封装了一些语义化的组件。

### 示例图
  ![](/medias/html-semantic/1.jpg)
### HTML5新增的语义化标签

`<header>`
* 用于页面body底部，可包含标题、导航栏和搜索栏等。
* 用于表示模块的头部，可用于section、article之中。


`<nav>`
* 用于定义导航，链接等。

`<main>`
* 用于表示页面的主体部分。

`<aside>`
* 用于作为侧边栏。
* 用于作为嵌入内容（在article内），用于展示一些附加信息。

`<footer>`
* 用于作为页脚。
* 用于展示article或者section的底部信息。

`<article>`
* 用于表示页面中的一段独立的内容，通常情况下包括标题、正文和脚注。article可以嵌套使用，但是必须是整体与部分的关系，比如文章中的评论部分。

`<section>`
* 用于对页面进行分块。
* 用于文章等进行分段。


### 附：一些常用结构化标签。

##### HTML5之前的

`<p>` : 用于表示段落。

`<li>`: 用于表示列表。

##### HTML5新增的

`<em>`: 代替`<i>`，表示强调，显示为斜体。
  
`<strong>`: 代替`<b>`，表示强调，显示为粗体。











