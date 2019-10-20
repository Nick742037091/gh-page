---
title: 迷宫问题
date: 2019-10-20 19:45:46
categories:
  - 算法
tags:
  - js
  - 回溯算法
---

本文描述的是找出走出迷宫的问题，迷宫是 NxN 的矩阵，入口为左上角，出口为右下角。

## 基本思路

假设迷宫矩阵中每个位置为一个方块，每个方块可以是空闲的(值为 1)或者是被阻挡的(值为 0)。

1.  创建一个二级数组 solution 用于存储结果。将 solution 的初始位置置 1， 从矩形的初始位置(左上角)开始查找。
2.  判断当前位置是否位于右下角，如果是的话，将 solution 对应的位置值 1，直接返回。判断当前位置是否为 1，若是的话就 solution 对应的位置值 1，执行下一步，否则直接返回。
3.  向右(x+1)查找，如果该位置为 0，返回上一级执行步骤 4；如果该位置为 1，将 solution 的对应的位置位置置 1，则执行再向右查找，执行步骤 2，依次类推。
4.  向下(y+1)查找，如果该位置为 0，返回上一级执执行步骤 5；如果该位置为 1，将 solution 的对应的位置位置置 1，执行步骤 3，依次类推。
5.  将 solution 的对应的位置位置置 0，结束该位置的查找，返回上一级。
6.  最终 solution 的置为 1 的位置表示了走出迷宫的路径。

![](/medias/maze/1.png)

## 示例代码（js）

```js
const rateInMaze = maze => {
  let solution = []
  const { length } = maze
  for (let i = 0; i < maze; i++) {
    solution[i] = []
    for (let j = 0; j < length; j++) {
      solution[i][j] = 0
    }
  }
  if (findPath(maze, 0, 0, solution)) {
    return solution
  }
  return false
}

const findPath = (maze, x, y, solution) => {
  const { length } = maze
  if (x === length - 1 && y === length - 1) {
    solution[x][y] = 1
    return true
  }
  if (isSafe(maze, x, y)) {
    solution[x][y] = 1
    if (
      findPath(maze, x + 1, y, solution) ||
      findPath(maze, x, y + 1, solution)
    ) {
      return true
    }
    solution[x][y] = 0
  }
  return false
}

const isSafe = (maze, x, y) => {
  const { length } = maze
  if (x >= 0 && y >= 0 && x < length && y < length && maze[x][y] !== 0) {
    return true
  }
  return false
}
```
