---
title: 内插搜索法
date: 2019-10-09 23:45:41
categories:
  - 算法
tags:
  - js
  - 搜索算法
---

内插搜索法是改良版的二分搜索法，适用于搜索已排序的数组，时间复杂度为 O(n)，在数组分布均匀时性能最好。

<!-- more -->

## 基本思路

利用数组最大值和最小值，计算出查找值的大概索引 index，若查找值小于 index 对应的值，则将 index-1 作为最大值，重新计算索引进行对比；若查找值大于 index 对应的值，则将 index+1 作为最小值，重新计算索引进行对比。以此类推，直到找到对应的值或者查找区域只有一个元素(没有对应的值)。

## 示例代码（js）

```js
/**
 * 内插搜索法
 * @param {数组} arry
 * @param {搜索的值} value
 */
const interpolationSearch = (arry, value) => {
  const { length } = arry
  let low = 0
  let high = length - 1
  let position = -1
  let delta = -1
  while (low < high && value >= arry[low] && value <= arry[high]) {
    delta = (value - arry[low]) / (arry[high] - arry[low])
    position = low + Math.floor((high - low) * delta)
    if (arry[position] === value) {
      return position
    } else if (arry[position] < value) {
      low = position + 1
    } else if (arry[position] > value) {
      high = position - 1
    }
  }
  return -1
}
```
