---
title: 背包问题
date: 2019-10-19 18:15:53
categories:
  - 算法
tags:
  - js
  - 动态规划算法
---

本文描述的是在一组不同重量和价值的背包中，给定最大重量，找出两两组合最大价值的背包。

## 基本思路

1. 优先排除超重背包和相等重量价值较低的背包。
2. 遍历所有背包，对于每个背包，按照当前背包重量+1至最大重量作为总重量进行遍历，获取可与当前背包组合的背包，得到组合后的价值。
3. 对比所有的组合的价值，得出最大的总价值和。


## 示例代码（js）

```js
const bagQuestion = (bagList, capacity) => {
  const wMap = {}
  let maxRes = {
    w1: 0,
    w2: 0
  }

  bagList.forEach(bag => {
    const { weight, value } = bag
    // 排除超重的背包
    if (weight >= capacity) return
    // 重量一样，价格较低优先的被排除
    if (
      wMap[weight] === undefined ||
      (wMap[weight] && wMap[weight].value < value)
    ) {
      wMap[weight] = bag
    }
  })

  for (let wKey in wMap) {
    const w1 = +wKey
    for (let total = w1 + 1; total <= capacity; total++) {
      const w2 = wMap[total - w1] ? wMap[total - w1].weight : 0
      // 没有可与当前背包组合的背包
      if (!w2) continue
      let curVal = 0
      let maxVal = 0
      const noMax = maxRes.w1 === 0 && maxRes.w2 === 0
      if (!noMax) {
        curVal = wMap[w1].value + wMap[w2].value
        maxVal = wMap[maxRes.w1].value + wMap[maxRes.w2].value
      }
      // 判断每个组合价值得到最大价值的组合
      if (noMax || curVal > maxVal) {
        maxRes = {
          w1,
          w2
        }
      }
    }
  }
  return [wMap[maxRes.w1], wMap[maxRes.w2]]
}
```