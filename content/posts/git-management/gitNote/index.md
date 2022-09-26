---
title: "Commom Git Operation with Github"
date: 2022-09-26T23:12:28+08:00
description: how to push responsity to github, load down, some problems during the operating as well. 
draft: false
menu:
  sidebar:
    name: commom git with github
    identifier: git-management-problems-git-github
    parent: git-management
    weight: 10
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

### 上傳前指令
---
1. 將檔案加入 git 暫存區
    > git add .

2. 將檔案提交至本地儲存庫
    > git commit . -m "提交訊息"

### 上傳用指令
---
1. 將檔案連結遠端儲存庫
    > git remote add origin [url]

2. 將檔案上傳至遠端儲存庫
    > git push -u origin main

### 常見問題
---
##### `fatal: refusing to merge unrelated histories`
{{< vs 1>}}
  - 可能原因：合併的分支名字衝突
  - 解法：
    - 更改目前分支名稱
    - `git merge --allow-unrelated-histories origin main`
{{< vs 2>}}
##### `[rejected] main -＞ main (non-fast-forward)`
{{< vs 1>}}
  - 可能原因： 該分支不是遠端儲存庫的最新版本 

### 參考資料

[fatal: refusing to merge unrelated histories](https://developer.aliyun.com/article/614459)  
[rejected problem](https://blog.csdn.net/qq_27249535/article/details/121906285)