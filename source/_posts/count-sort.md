---
title: 计数排序
date: 2019-10-06 22:33:36
categories:
  - 算法
tags:
  - js
  - 排序算法
---

计数排序是一种分布式排序算法，分布式排序使用已组织好的辅助数据结构（称为桶）,然后进行合并，得到排好序的数组。
计数排序是用来排序正整数的优秀算法，时间复杂度为 O(n+k),k 为临时计数数组的大小。计数排序需要更多的内存来存放临时数组。

<!-- more -->

## 基本思路

使用一个用来存储每个元素在原始数组（0 至最大值）中出现次数的临时数组，迭代临时数组，并根据元素出现次数，依次添加到结果数组中。

## 示例代码（js）

```js
/**
 * arry 数组
 * asc 是否升序排序
 **/
const countSort = (arry, asc = true) => {
  if (arry.length < 2) {
    return arry
  }
  const max = findMaxValue(arry)
  const counts = new Array(max + 1)
  arry.forEach(item => {
    if (!counts[item]) {
      counts[item] = 0
    }
    counts[item]++
  })
  const res = []
  counts.forEach((count, index) => {
    while (count > 0) {
      if (asc) {
        res.push(index)
      } else {
        res.unshift(index)
      }
      count--
    }
  })
  return res
}

const findMaxValue = arry => {
  let max = arry[0]
  for (let i = 1; i < arry.length; i++) {
    if (arry[i] > max) {
      max = arry[i]
    }
  }
  return max
}
```
