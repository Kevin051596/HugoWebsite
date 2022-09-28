---
title: "無法推上遠端儲存庫"
date: 2022-09-28T09:54:28+08:00
description: record problems during using git
draft: false
menu:
  sidebar:
    name: problems recording 1
    identifier: git-management-problems-recording-1
    parent: git-management
    weight: 10
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

### 錯誤紀錄
***
{{< alert type="info" >}}
`error: src refspec main does not match any`  
`error: failed to push some refs to [repo_url]`
{{< /alert >}}
> **可能原因**   
> 遠端儲存庫沒有對應的分支 
> ***
> **解決方法**  
> 將本地儲存庫待上傳的分支更名  
> `git branch -m [old branch] [new branch]`  

{{< vs 3>}}
{{< alert type="info" >}} 
` ! [rejected]        main -> main (non-fast-forward)`  
`error: failed to push some refs to [repo_url]`
{{< /alert >}}
> **可能原因**  
> 部分內容未被合併，該版本不是遠端儲存庫最新版本
> ***
> **解決方法**  
> `git fetch origin main`  
> `git merge --allow-unrelated-histories origin/main`  
> `git add .`  
> `git commit`  

### 參考資料
***
[fatal: refusing to merge unrelated histories](https://developer.aliyun.com/article/614459)  
[rejected problem](https://blog.csdn.net/qq_27249535/article/details/121906285)  