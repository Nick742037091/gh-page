---
title: 基数排序
date: 2019-10-09 23:09:28
categories:
  - 算法
tags:
  - js
  - 排序算法
---

基数排序是一种分布式排序算法，是根据数字的基数(如十进制数基数为 10)将整数分布到桶中。

<!-- more -->

## 基本思路

以十进制数为例，先根据个位数字，利用桶排序法(10 个桶)进行排序，生成新数组。再对十位数字进行排序，生成新数组。以此类推，最高位排序之后即为结果数组。

## 示例代码（js）

```js
/**
 * 基数排序
 * @param {数组} arry
 * @param {基数} base
 * @param {是否升序排序} asc
 */
const baseSort = (arry, base = 10, asc = true) => {
  // 利用字符串长度获取最大数字长度
  let maxLength = 0
  arry.forEach(item => {
    const { length } = String(item)
    if (length > maxLength) {
      maxLength = length
    }
  })
  for (let i = 0; i < maxLength; i++) {
    arry = baseBucketSort(arry, i, base, asc)
  }
  return arry
}

const baseBucketSort = (arry, index, base, asc) => {
  const res = []
  const temp = []
  //创建桶
  for (let i = 0; i < base; i++) {
    temp[i] = []
  }
  //根据对应位数字分布到各个桶
  arry.forEach(item => {
    const bucketIndex = Math.floor(item / Math.pow(base, index)) % base
    if (asc) {
      temp[bucketIndex].push(item)
    } else {
      temp[base - 1 - bucketIndex].push(item)
    }
  })
  //通过桶生成排序后的数组
  temp.forEach(list => {
    list.forEach(item => {
      res.push(item)
    })
  })
  return res
}
```
