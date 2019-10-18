---
title: 桶排序
date: 2019-10-08 22:06:12
categories:
  - 算法
tags:
  - js
  - 排序算法
---

桶排序是一种分布式排序算法，时间复杂度为 O(n+k)。

## 基本思路

它根据元素大小将数组分为不同的桶(较小的数组),再使用一个简单的排序算法，例如插入排序(适合小数组的排序)，来对每个桶进行排序，最后将所有的桶合并为结果数组。

## 示例代码（js）

```js
/**
 * arry 数组
 * asc 是否升序排序
 **/
/**
 * 桶排序法
 * @param {数组} arry
 * @param {是否升序排序} asc
 * @param {桶容量} bucketSize
 */
const bucketSort = (arry, asc = true, bucketSize = 5) => {
  if (arry.length < 2) {
    return arry
  }
  const buckets = createBucket(arry, asc, bucketSize)
  return sortBuckets(buckets, asc)
}

const createBucket = (arry, asc = true, bucketSize) => {
  let min = arry[0]
  let max = arry[0]
  for (i = 1; i < arry.length; i++) {
    const cur = arry[i]
    if (cur < min) {
      min = cur
    }
    if (cur > max) {
      max = cur
    }
  }

  const bucketCnt = Math.floor((max - min) / bucketSize) + 1
  const buckets = []
  for (let i = 0; i < bucketCnt; i++) {
    buckets[i] = []
  }
  for (let i = 0; i < arry.length; i++) {
    const cur = arry[i]
    if (asc) {
      const bucketIndex = Math.floor((cur - min) / bucketSize)
      buckets[bucketIndex].push(cur)
    } else {
      const bucketIndex = bucketCnt - 1 - Math.floor((max - cur) / bucketSize)
      buckets[bucketIndex].unshift(cur)
    }
  }
  return buckets
}

const sortBuckets = (buckets, asc) => {
  const res = []

  buckets.forEach(bucket => {
    insertSort(bucket, asc)
    if (asc) {
      res.push(...bucket)
    } else {
      res.unshift(...bucket)
    }
  })
  return res
}
```
