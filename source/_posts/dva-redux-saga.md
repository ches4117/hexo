---
title: dva-redux-saga
date: 2020-02-26 22:13:07
tags: ReactJS
---

如果使用者在短時間內連續點擊頁面，使 Redux 連續取得資料並更新 props，導致頁面快速刷新。
為了改善該問題，我去看幾間網站的做法，大部分都是將除了最後一個點擊之外的連線需求取消。
<!--more-->

## 解決
1. [dva issue](https://github.com/dvajs/dva/issues/1749)
2. [Redux Saga cancel](https://redux-saga.js.org/docs/advanced/TaskCancellation.html)

從 1 中，我知道 dispatch type clear 可以取消當前 model 所有未完成的 effect，但是最後講到的 race 方法無法解決我的問題。

從 2 中，我找到了 cancel，於是我將 task fork 之後，記錄該 task。
也因此，我能夠在每次 dispach 時，檢查之前是否有 task，如果有，則將該 task cancel。

## 心得
目前還在檢查該作法是否有其他隱患。