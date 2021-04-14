---
title: How-to-deploy
date: 2021-01-12 22:06:54
tags: git
---

目前公司的開發流程有點類似於 GitFlow，使用 Jenkins 部屬，且主要是由我來部屬上版，也因此我花了不少時間在研究以及了解部屬流程。

<!--more-->

## 介紹

我目前公司的開發流程相較於 GitFlow 少了 release 階段。有 Alpha 測試，Beta 測試，Gamma 測試，三個測試跑完之後才會部屬上 Demo 和 Production。

- Alpha 測試使用 feature 分支，供前後端內部測試使用。測試完 merge 進去 develop。
- Beta 測試使用 develop 分支，供 QA 和 PM 測試。測試完後 merge 進去 master。
- Gamma 測試使用 hotfix 分支，供 QA 和 PM 測試。測試完後 merge 進去 develop 和 master。
- Demo 和 Production 使用 master 分支，供正式使用。

## 心得

目前公司的 Jenkins 部屬一次大概要花七至十分鐘。其中 Gamma 測試最麻煩，因為需要更新到兩個分支，而且還要確保正式環境不會有問題。

另外我們平常開發時通常使用 git pull --rebase，而在 merge 回其他分支時使用 git merge。rebase 的好處在於能夠消除不必要的合併提交，但是在像是 feature 分支 merge 進去 develop 時就不適合使用 rebase，因為會產生許多 conflict。
