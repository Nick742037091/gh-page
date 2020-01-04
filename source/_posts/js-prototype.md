---
title: js原型与继承
date: 2020-01-04 22:53:22
categories:
  - 前端
tags:
  - js
  - 原型
  - 继承
---

本文主要介绍 js 的原型与继承。

<!-- more -->

# 原型

每个函数都有一个 prototype(原型)属性，这个属性是一个指针，指向一个对象，这个对象的包含特定类型实例的共享属性和方法。prototype 包含了 constructor 属性，指向该函数（即构造函数）。该函数通过 new 操作创建的实例，包含内置的`[[Prototype]]`属性（一些浏览器中存在相同含义的`__proto__`属性），指向原型。

实例中查找属性时，先从实例自身查找，查找不到时，再从原型中查找。

```js
function Person(name) {
  // 覆盖原型的name属性
  if (name) {
    this.name = name
  }
}
Person.prototype.name = 'nick'
Person.prototype.sex = 0
Person.prototype.age = 29
Person.prototype.showName = function() {
  console.log(this.name)
}
var nick = new Person()
var jack = new Person('jack')
nick.showName() // nick
jack.showName() // jack
```

</br>

![](/medias/js-prototype/1.png)

# 继承
