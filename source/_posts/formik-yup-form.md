---
title: formik-yup-form
date: 2020-12-12 21:19:01
tags: ReactJS
---

最近換公司，新公司需要實作許多表單供使用者填寫。React 表單的套件繁多，各有優缺，而我目前只有用過 Formik，故不做比較，只分享我目前的心得。

<!--more-->

## 介紹

[Formik](https://formik.org/) 提供了兩種建立表單的方式，第一種是組件的方式，像是 `<Field>`，預設是`<input>`元件，又或是透過 `<Field as="select">` 則是`<select>`元件。而如果想要使用自己的組件則需要使用`<Field component>`。

不過因為我新公司已經有一套自己的組件使用了。所以是使用另一種透過 hook 以及 context 的方式，將 Formik 所需的方法以及變數拿來使用。Formik 提供了 `useFormikContext()` 的方式，取得我們所設定好的表單初始值和初始狀態，以及 Formik 原本就有的方法。

最後，錯誤驗證則是結合了 [Yup](https://github.com/jquense/yup) ，Yup 的錯誤規則蠻簡單上手的，而且還有支援正則。

## 問題

隨著單頁的 `input` 的數量增加，輸入的速度也會有所延遲。這是因為每個輸入都會觸發 `onChange` 進行驗證，最後的解決方法是在 `onBlur` 時才觸發驗證。
