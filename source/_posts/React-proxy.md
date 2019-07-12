---
title: React_proxy
date: 2019-07-11 22:28:59
tags: ReactJS
---
  我在做一個練手的展示頁面，使用的是 [create-react-app](https://github.com/facebook/create-react-app)。但是在嘗試想要爬取其他網站資料時，遇到 CORS 問題。

在這之前，我就有使用其他方式成功爬取網站過，但是反而在使用 create-react-app 時遇到 CORS 而無法爬取，所以我首先懷疑是否是 create-react-app 的設定問題，
最後才發現是 proxy 沒設定的問題。而我在公司時的專案由於已經都設定好 proxy 了，所以沒有遇到該問題，故這對我來說是新鮮的挑戰。

## 解決
```javascript
const proxy = require('http-proxy-middleware')
module.exports = function (app) {
  app.use(proxy('http://localhost:3000/search', { target: 'https://www.suruga-ya.jp', changeOrigin: true }))
  app.use(proxy('http://localhost:3000/product/detail/', { target: 'https://www.suruga-ya.jp/', changeOrigin: true }))
  app.use(proxy('http://localhost:3000/database/pics/game/', { target: 'https://www.suruga-ya.jp/', changeOrigin: true }))
}
```
