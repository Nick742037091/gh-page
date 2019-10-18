---
title: 二分搜索法
date: 2019-10-09 23:36:26
categories:
  - 算法
tags:
  - js
  - 搜索算法
---

二分搜索法是适用于已排序数组的搜索算法，时间复杂度为 O(log(n))。

## 基本思路

取数组中间数进行对比，若小于中间数，则取最小值和中间值之间的中间数进行对比；
若大于中间数，则取中间数和最大值之间的中间数进行对比。以此类推，直到找到对应的值或者查找区域只有一个元素(没有对应的值)。

## 示例代码（js）

### 迭代法

```js
/**
 * 数组二分搜索
 * @param {搜索的数组}} arry
 * @param {搜索的值} value
 */
const binarySearch = (sortArry, value) => {
  let low = 0
  let high = sortArry.length - 1
  while (low <= high) {
    const mid = Math.floor((low + high) / 2)
    if (value < sortArry[mid]) {
      high = mid - 1
    } else if (value > sortArry[mid]) {
      low = mid + 1
    } else {
      return mid
    }
  }
  return -1
}
```

### 递归法

```js
**
 * 数组二分搜索
 * @param {排序的数组} sortArray
 * @param {搜索的值} value
 */
const binSearch = (sortArray, value) => {
  const low = 0
  const high = sortArray.length - 1
  return binSearchRecursive(sortArray, low, high, value)
}

const binSearchRecursive = (sortArray, low, high, value) => {
  if (low === high) {
    return sortArray[low] === value ? low : -1
  }
  const midIndex = Math.floor((low + high) / 2)
  const mid = sortArray[midIndex]
  if (value > mid) {
    return binSearchRecursive(sortArray, midIndex + 1, high, value)
  } else if (value < mid) {
    return binSearchRecursive(sortArray, low, mid - 1, value)
  } else {
    return midIndex
  }
}
```
