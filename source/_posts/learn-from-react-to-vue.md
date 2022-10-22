---
title: learn-from-react-to-vue
date: 2022-10-22 08:54:08
tags: Vue
---

我在今年初的時候從電商網站離職，目前公司是使用 Vue 開發內容管理系統(CMS)。
雖然之前都聽過別人說學 React 後再學 Vue 很簡單，而且 Vue3 也蠻像 React 的。
但是親身學習過後才知道，真的蠻簡單的(？)。
<!--more-->

## 心得

* 事件綁定寫法不同，例如 Vue 使用 `v-bind:click`，而 React 使用 `onClick`。
* 組件傳值的寫法蠻容易搞混的，個人會覺得 React 傳值時用 `{}`，比 Vue 傳值用 `:` 清楚。
* 不能用陣列 `map` 的方式去產生組件，而要改用 `v-for`。Vue 就是要讓使用者始終在操作 HTML 元素，但是我一開始會困惑為什麼兩邊都可以渲染變數，而我想使用 `map` 渲染變數卻不行。
* 好用又危險的 `v-model` ，與蠻多人討論過我們該在哪時候使用 `v-model`，目前聽過最極端案例是完全禁止使用 `v-model`，而我跟另一名友人的想法是認為可以適當應用。而關於怎樣才叫做適當應用，這我覺得就是軟體開發的最難以掌控的點了，所以也是能夠理解完全禁止的考量了。
* `function` 傳遞時該使用 `emit` 還是 `props` ，React 可以把 `function` 四處傳，而 Vue 提供了兩種傳遞途徑，我與友人討論過是覺得 `function` 應該只用 `emit` 傳遞。

## 總結

我目前這間公司剛進去，隔天就用 Vue3 開發元件了，然後一個禮拜內就正式進行開發文章編輯器。
所以我被迫快速掌握 Vue3，但也因此我能夠確切體認到，兩者的轉換真的不用花太多時間。
當然，一開始寫的程式蠻多都沒利用到 Vue 的優點，更多只是當 React 寫。