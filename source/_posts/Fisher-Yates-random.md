---
title: Fisher-Yates随机算法
date: 2019-10-10 23:50:33
categories:
  - 算法
tags:
  - js
  - 随机算法
---

一种适用于对数组进行随机排序的算法。

<!-- more -->

## 基本思路

迭代数组，从最后一位开始将当前位置和一个随机位置进行交互，这个随机位置比当前位置小。这样，这个算法可以保证随机过的位置不会再被随机一次。

## 示例代码（js）

```js
const swapInList = (list, a, b) => {
  temp = list[a]
  list[a] = list[b]
  list[b] = temp
}

const shuffle = arry => {
  for (let i = arry.length - 1; i > 0; i--) {
    const randomIndex = Math.floor(Math.random() * (i + 1))
    swapInList(arry, i, randomIndex)
  }
  return arry
}
```
