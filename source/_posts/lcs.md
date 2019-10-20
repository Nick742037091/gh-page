---
title: 最长公共子序列
date: 2019-10-20 11:16:48
categories:
  - 算法
tags:
  - js
  - 动态规划算法
---

本文描述的是找出两个字符中以相同顺序出现，但不要求连续（非字符串子串）的最长子字符串。

## 基本思路

迭代字符串 X，假设当前字符为 a,从第一个字符开始迭代字符串 Y，直到找到相同字符所在的位置 index。
往后迭代字符串 X，在下一次迭代字符串 Y 的时候从 index+1 开始迭代。以此类推，将所有找到的相同字符串组合成最长公共子序列。

## 示例代码（js）

```js
const lcs = (strX, strY) => {
  let res = ''
  let startY = 0
  for (let x = 0; x < strX.length; x++) {
    const wX = strX[x]
    for (let y = startY; y < strY.length; y++) {
      const wY = strY[y]
      if (wX === wY) {
        res += wX
        startY = y + 1
        break
      }
    }
  }
  return res
}
```
