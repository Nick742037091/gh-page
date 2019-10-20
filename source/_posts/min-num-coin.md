---
title: 最少硬币找零问题
date: 2019-10-14 22:35:11
categories:
  - 算法
tags:
  - js
  - 动态规划算法
---

动态规划是一种将复杂问题分解为更小的子问题来解决的优化技术。本文描述的是从给定零钱数组中，找出组合成指定金额数量最少的搭配。

## 基本思路

1. 迭代数组，用指定金额减迭代项，得到余数。
2. 若余数大于 0，用余数代替指定金额，重复 1 步骤，递归至余数为 0。余数为 0 时，返回空数组。
3. 在步骤 1 的每次迭代中可得到组成余数的零钱数组，和迭代项合并成数组 C。返回所有迭代之中长度最小的数组 C。
4. 将指定金额和对应的最少数组 C 缓存起来，避免重复查询。
5. 将所有 1 步骤得到的最少数组合并起来得到最终的最少数组。

## 示例代码（js）

```js
const minCoinChange = (coins, amount) => {
  // 缓存各个值对应的最少零钱数组
  const cache = []
  // 缓存最少零钱数组长度,初始化为无效大
  let minNum = Number.MAX_VALUE
  // 最终得到的最少零钱数组
  let res = []
  const makceChange = value => {
    if (!value) {
      return []
    }
    if (cache[value]) return cache[value]
    let min = []

    coins.forEach(item => {
      newAmount = value - item
      // 余数小于0不处理
      if (newAmount < 0) return
      let newMin = makceChange(newAmount)
      // 对比得到组成value的最少零钱数组
      // 存在余数大于零且无法由零钱组合成(newMin.length === 0)的情况，此时不做处理
      if (
        (min.length === 0 || newMin.length + 1 < min.length) &&
        (newMin.length > 0 || newAmount === 0)
      ) {
        min = [item, ...newMin]
        // 对比得到组成指定金额amount的最少零钱数组
        if (value === amount && min.length < minNum) {
          minNum = min.length
          res = min
        }
      }
    })
    return (cache[value] = min)
  }
  makceChange(amount)
  return res
}
```
