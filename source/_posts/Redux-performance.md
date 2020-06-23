---
title: Redux-performance
date: 2020-06-20 10:40:00
tags: ReactJS
---
  記錄個之前都沒遇過的問題，關於 Redux 的效率問題。
<!--more-->

## 問題
  昨天發現在 Redux 裡面塞太多資料時，會導致頁面切換速度緩慢。原因是因為 Redux 在 shouldComponentUpdate 會進行 shallow compare，而我傳入的資料是大量的 array 導致 shallow compare 花的時間過多。

## 解決
  可以考慮在切換到其他頁面時清空資料，但是這樣會導致再切回去時要重新載入資料，或是改用 object 存取資料。

## 補充
  今天發現是因為我在另一個頁面產生的多個 canvas，在切換頁面之後還暫存著，導致頁面因此載入緩慢，而不是我在 Redux 存的資料太多的問題。不過上述 Redux 的效率問題依舊還是需要考慮。

