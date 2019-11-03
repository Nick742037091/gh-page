---
title: 快速排序
date: 2019-10-02 21:20:43
categories:
  - 算法
tags:
  - js
  - 排序算法
---

快速排序是比较常用的一种排序算法，复杂度为 O(nlog(n))，使用的是分而治之的方法。

<!-- more -->

## 目标

> 实现数组升序排序

## 基本思路

1. 以数组中间值作为参考，将数组拆分为小数区域(小于等于中间值的元素)和大数区域(大于中间值的元素)。
2. 对小数区域和大数区域分布进行 1 操作，递归直至拆分后的区域只有一个元素。

## 示例代码（js）

```js
const quickSort = arry => {
  quick(arry, 0, arry.length - 1)
}

// 元素长度大于1，才进行排序。
// 将元素拆分为左右大小区域，然后分别对左右区域进行拆分。
const quick = (arry, left, right) => {
  const { length } = arry
  if (length > 1) {
    const index = partition(arry, left, right)
    if (left < index - 1) {
      quick(arry, left, index - 1)
    }
    if (right > index) {
      quick(arry, index, right)
    }
  }
}
// 从数组两侧往中间遍历，以中间元素作为参考值。左侧向中间查找大于或等于参考值的元素，右侧向中间查找小于或等于参考值的元素。将查找到的左右两侧的元素进行替换，继续往中间查找。当左侧索引大于右侧索引，停止查找。最终左侧的元素都小于右侧的元素。
const partition = (arry, left, right, asc = true) => {
  const pivot = arry[Math.floor((left + right) / 2)]
  let i = left
  let j = right
  while (i <= j) {
    // {3}
    while (arry[i] < pivot) {
      i++
    }
    while (arry[j] > pivot) {
      j--
    }
    if (i <= j) {
      // {4}
      swapInList(arry, i, j)
      i++
      j--
    }
  }
  return i
}

const swapInList = (list, a, b) => {
  temp = list[a]
  list[a] = list[b]
  list[b] = temp
}
```

假设中间参考值为 m。
对行 3 取 i === j 时，存在以下几种情况:

1. `arry[i] === arry[j] === m`，则 `i++,j--`，函数返回 i。对应于行 4 ，i === j 的情况。
   > ![](/medias/quick-sort/1.png)
2. `arry[i] === arry[j] < m`，则 `i++`，j 不变，函数返回 i。
   > ![](/medias/quick-sort/2.png)
   > 或者
   > ![](/medias/quick-sort/3.png)
3. `arry[i] === arry[j] > m`，则 i 不变,`j--`，函数返回 i。

   > ![](/medias/quick-sort/4.png)
   > 或者
   > ![](/medias/quick-sort/5.png)

   因此数组中索引 0~i-1 为小数区域，>=i 为大数区域，left <= i <= right。
