---
title: dva-roadhog with babel problem
date: 2019-08-20 22:46:36
tags:
---
  之前公司在開始專案之前並沒有考慮到跨瀏覽器問題，先是在 Safari 上遇到 CSS 不相容問題，現在又遇到要在 Android 4.0 的系統上運行網頁。同樣的也是如同 CSS 不相容時的狀況，開啟網頁後一片全白的狀況。
<!--more-->

## 框架介紹
  [dva](https://github.com/dvajs/dva)
  [roadhog](https://github.com/sorrycc/roadhog)

## 解決
   首先排除掉 CSS 不相容後，遇到個困難是要如何印出 error message。最後是在 index.ejs 最上面使用 window.onerror 來印出 error message。 

   最後印出 ```Uncaught ReferenceError: Set is not defined```，通常是在無法識別 ES6 的語法時才會出現，而這可以使用 [babel-polyfill](https://babeljs.io/docs/en/next/babel-polyfill.html) 解決。但是我已經在 index.js 最上面 ```import @babel/polyfill```，也因此我嘗試在其他地方引入 babel-polyfill。

   最後是在 .webpack.rc.js 的 entry 中配置 babel-polyfill，詳細情況如該 [issue](https://github.com/dvajs/dva/issues/1692#issuecomment-390560686)。

## 心得
   目前是還在尋找為什麼 ```import @babel/polyfill``` 沒有發揮作用，不過專案最後還是成功運行在 Android 4.0 上。