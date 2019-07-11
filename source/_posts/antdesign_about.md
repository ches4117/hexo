---
title: Ant Design初學心得    
date: 2019-06-05 22:08:54
tags: ReactJS
---
  工作一年多了，工作一開始對 Javascript 還不太熟悉，就直接開始使用 Reactjs。理所當然的，基本知識面的不足加上 React 生態系的複雜，使我撞到過無數次牆。

不過就算是現在，我也不敢說自己已經熟悉 React 了，程度頂多就是剛入門。標題的 [Ant Design](https://ant.design/docs/react/introduce-cn) 是 React 的 UI 框架之一，不過其實並不太建議初學者直接從框架開始，因為會有一堆東西塞在框架裡面，而你卻不知道他們的功能是什麼，出問題時如果身旁沒有有經驗的人指導的話，很容易陷入誤區，挫折感會很大。

## 開始
[在 create-react-app 中使用](https://ant.design/docs/react/use-with-create-react-app-cn)是 Ant Design 的教學頁面，如字面上的意思，就是使用 [create-react-app](https://facebook.github.io/create-react-app/) 初始化 Ant Design。create-react-app 是 React 官方支持，創建基本 SPA（Single Page Application）的工具。簡單的流程結束之後，只要輸入```npm start```，就可以看到最基本的頁面了。

## 進階
因為 Ant Design 是一個龐大的框架，而我們通常不會運用到全部的組件，因此就需要使用到按需加載。有兩種方法可以實現按需加載，第一種是引入組件時寫成 ```import { XXX } from antd/lib/XXX```，而第二種則是使用 Ant design 自行開發的 babel 插件 [babel-plugin-import](https://github.com/ant-design/babel-plugin-import)，設定完成之後，該插件能夠將原本的 ```import { XXX } from 'antd'``` 轉換成```import { XXX } from antd/lib/XXX```。

## 心得
Ant Design 我較熟悉的是圖表組件，而他們的圖表組件是使用 [Bizchart](https://bizcharts.net/products/bizCharts) 完成的，所以如果對圖表組件有什麼想要新增或是疑問時，建議是直接去 Bizchart 官方網站找尋解答。而我在使用圖表組件時偶爾會遇到一些 responsive bug，部分圖表在縮放時表現的並不如預期。而且有些圖表組件的寬高設置也不是很彈性，需要動態獲取外層元件的寬高才能設定內層圖表組件的寬高。除此之外，Ant Design 我目前用起來都沒有遇到太大問題。