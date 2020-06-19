---
title: react-virtualized-tree
date: 2019-08-01 23:44:29
tags: ReactJS
---
  由於需要使用 tree 展示大量數據，而 [Ant Design](https://ant.design/docs/react/introduce-cn) 的 tree 在展示大量數據時，會導致畫面延遲，詳細重現以及解決方法可參考[該篇](https://blog.logrocket.com/rendering-large-lists-with-react-virtualized-82741907a6b3/)。
<!--more-->
## 解決
  我一開始是想使用 Tree 的節點，將一定數量的節點摺疊起來，需要時再展開。雖然這樣可以暫時解決問題，但是並不美觀，而且在大量展開節點時依舊會十分緩慢。因此我試了以下幾種套件。
  1. [react-lazy-paginated-tree](https://github.com/venasolutions/react-lazy-paginated-tree)
  2. [react-virtualized-tree](https://github.com/diogofcunha/react-virtualized-tree)

## react-lazy-paginated-tree
  這個套件有點類似我一開始的作法，不過他有做 Lazy load 和 Pagination，而 Pagination 需要自己參考範例寫 Pagination function。
  
  最後考量到在同時展開多個節點的情境下，應該還是會造成網頁緩慢，故最後沒有選擇使用該套件。
  
  (P.S: 雖然我覺得可以透過限制使用者展開節點數量來避免這種狀況發生。)

## react-virtualized-tree
  該套件主要依賴於 [react-virtualized](https://github.com/bvaughn/react-virtualized)，virtualized 的原理可以參考[該篇](https://github.com/dwqs/blog/issues/70)，在我的理解就是只渲染固定區域的元素，然後在該區域滾動時刷新該區域當前所顯示之元素。而我在 Antd 中引用該套件時，無法正常顯示 icon。
  
  後來我把 [material-icons](https://www.npmjs.com/package/material-icons) 的字型檔加入後即可正常顯示。而在這之前，我嘗試將該套件 Icon 的事件，繼承到 Antd Icon 上面使用，但是一直無法成功，也因此只能使用該套件的預設的 Icon。

## 心得
  最後成功將原本 Antd tree 的組件替換為 react-virtualized-tree，不過相比起 Antd tree，react-virtualized-tree 有許多小細節需要修改。