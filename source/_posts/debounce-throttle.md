---
title: 防抖与节流
date: 2019-12-23 13:24:21
categories:
  - 算法
tags:
  - js
  - 防抖
  - 节流
---

## 防抖

```js
/**
 * 防抖，每次触发重新计时
 * @param {function} fn 处理函数
 * @param {number} wait 延迟时间时间
 * @param {boolean} immediate 是否立即触发
 */
export const debounce = (fn, wait, immediate = false) => {
  let timer = null
  const debounced = function(...args) {
    let result = null
    const callNow = !timer
    if (timer) clearTimeout(timer)
    timer = setTimeout(() => {
      fn.call(this, args)
    }, wait)
    if (immediate) {
      if (callNow) result = fn.call(this, args)
    }
    return result
  }

  debounced.cancel = function() {
    clearTimeout(timer)
    timer = null
  }
  return debounced
}
```

## 节流

```js
/**
 *  节流函数，每隔一段时间可触发一次。可控制首次和末次是否触发。
 * @param {function} fn 处理函数
 * @param {number} wait 时间间隔
 * @param {object} options leading: 首次是否触发；trailing末次是否触发。leading和trailing不能同时为false
 */
export const throttle = (
  fn,
  wait,
  options = { leading: true, trailing: false }
) => {
  let timer = null
  let preTime = 0
  const throttled = function(...args) {
    const curTime = new Date().getTime()
    // a.判断是否首次直接触发
    if (preTime === 0 && !options.leading) preTime = curTime
    const remainTime = wait - (curTime - preTime)
    if (remainTime <= 0) {
      // 在超过或等于固定时间间触发
      // 1.若定时器已启动，取消定时器，确保不会额外触发一次。
      // 2.直接触发事件。
      if (timer) {
        // 刚好remaining === 0
        clearTimeout(timer)
        timer = null
      }
      fn.call(this, args)
      preTime = curTime
    } else if (!timer && options.trailing) {
      // 在固定时间间隔内触发，若定时器没启动，启动定时器，在remaining时间之后再触发一次。
      timer = setTimeout(() => {
        fn.call(this, args)
        // 若首次不直接触发，需要将preTime值为零作为a处的判断条件
        preTime = options.leading ? new Date().getTime() : 0
        timer = null
      }, remainTime)
    }
  }

  throttled.cancel = function() {
    clearTimeout(timer)
    preTime = 0
    timer = null
  }
  return throttled
}
```
