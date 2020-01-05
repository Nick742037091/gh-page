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

每个函数都有一个 prototype(原型)属性，这个属性是一个指针，指向一个对象，这个对象的包含特定类型实例的共享属性和方法。prototype 包含了 constructor 属性，指向该函数（即构造函数）。该函数通过 new 操作创建的实例，包含内置的`[[Prototype]]`属性（一些浏览器中存在相同含义的`__proto__`属性），指向原型。所有函数的默认原型是 Object.prototype，Object.prototype 的原型是 null。

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

// 判断原型的两种方法
console.log(Person.prototype.isPrototypeOf(nick)) //true
console.log(Object.getPrototypeOf(nick) === Person.prototype) //true

// 判断是否在实例和原型中
console.log('age' in nick) //true
// 判断是否在实例中
console.log(nick.hasOwnProperty('age')) //false

// 获取实例中的属性
console.log(Object.keys(nick)) // []
// 获取原型中的属性
console.log(Object.keys(Person.prototype)) //  ["name", "sex", "age", "showName"]
// 遍历实例和原型中的属性
for (let key in jack) {
  console.log(key)
}
```

</br>

![](/medias/js-prototype/1.png)

## 最佳实践

```js
function Person(name, sex, age) {
  // 实例属性
  this.name = name
  this.sex = sex
  this.age = age
}

Person.prototype = {
  constructor: Person,
  // 原型属性
  showName: function() {
    console.log(this.name)
  }
}
```

# 继承

原型链：查找实例属性时，若实例本身不存在该属性，会从原型中查找，若原型中找不到，则从上一级原型中查找，直到原型为 null 为止，原型之间的这种关系成为原型链。js 通过原型链实现继承。

## 最佳实践

```js
function SuperType(name) {
  this.name = name
  this.colors = ['red', 'green']
}

SuperType.prototype.showName = function() {
  console.log(this.name)
}

function SubType(name, age) {
  // 使用父类实例作为原型，会导致属性创建在父类实例中，存在数据共享问题。
  // 因此调用父类的构造函数，创建子类的属性。
  SuperType.call(this, name)
  // 初始化子类自身的属性
  this.age = age
}

function inheritPrototype(SubType, SuperType) {
  // 增加一层原型，避免调用父类构造函数导致多余的父类属性，同时也能继承父类原型中的属性
  function F() {}
  F.prototype = SuperType.prototype
  var obj = new F()
  // 设置子类原型的构造器
  obj.constructor = SubType
  SubType.prototype = obj
}

// 继承父类原型属性
inheritPrototype(SubType, SuperType)

SubType.prototype.showAge = function() {
  console.log(this.age)
}
var sup = new SuperType('sup')
var sub = new SubType('sub')
```
