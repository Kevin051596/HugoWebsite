---
title: "Command Lists and Problems"
date: 2022-09-26T23:12:28+08:00
description: some useful commands and problems during using git 
draft: false
menu:
  sidebar:
    name: commands & problems
    identifier: git-management-commands-&-problems
    parent: git-management
    weight: 10
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

### 首次使用必要指令
---
{{< split 4 8>}}
1. 設定使用者名稱

2. 設定使用者電子信箱

3. 列出使用者資訊
---
`git config --global user.name "your_username"`  

`git config --global user.email "your_email_address@example.com"`  

`git config --global --list`  
{{< /split >}}
### 常見上傳流水線指令
---
{{< split 4 8>}}
1. 初始化本地儲存庫

2. 將檔案加入 git 暫存區

3. 將檔案提交至本地儲存庫

4. 將檔案連結遠端儲存庫

5. 將檔案上傳至遠端儲存庫
---
`git init`

`git add .`

`git commit -m "commit message" ` 

`git remote add origin [repo_url]`  

`git push -u origin main`  

{{< /split >}}

### 分支指令、傳輸指令
---
{{< split 5 7>}}
1. 查看分支列表（只有本地）

2. 查看分支列表（本地和遠端）

3. 創建新分支

4. 刪除本地分支

5. 刪除本地分支（強制執行）

6. 刪除遠端分支

7. 創建新分支並切換於此

8. 下載遠端分支並切換於此

9. 更名分支

10. 切換分支

11. 切換回上個分支

12. 捨棄該檔案的更動

13. 刪除該檔案

14. 合併分支（合併於當前分支）

15. 合併分支（來源分支合併於目標分支）

16. 預覽分支合併後的更動

17. 上傳至遠端分支

18. 上傳至遠端分支並且記憶該分支

19. 上傳至遠端分支並且記憶該分支

20. 拉取遠端儲存庫更動

21. 拉取遠端儲存庫更動

22. 增加遠端儲存庫  
  
23. 設置儲存庫的起點為 SSH

24. 下載遠端儲存庫

25. 下載遠端私人儲存庫
---

`git branch`

`git branch -a`

`git branch [branch name]`

`git branch -d [branch name]`

`git branch -D [branch name]`

`git push origin --delete [branch name]`

`git checkout -b [branch name]`

`git checkout -b [branch name] origin/[branch name]`

`git branch -m [old branch name] [new branch name]`

`git checkout [branch name]`

`git checkout -`

`git checkout -- [file-name.txt]`

`git rm -r [file-name.txt]`

`git merge [branch name]`

`git merge [source branch] [target branch]`

`git diff [source branch] [target branch]`

`git push origin [branch name]`

`git push -u origin [branch name]`

`git push`

`git pull`

`git pull origin [branch name]`

`git remote add origin [repo_url]`

`git remote set-url origin [repo_url]`

`git clone repo_url`

`git clone [repo_url]`
{{< /split >}}

### 其他指令
---
{{< split 4 8>}}
1. 查看當前狀態

2. 將當前工作區加入暫存

3. 將暫存區清空

4. 列出歷史紀錄

5. 列出詳細歷史紀錄

6. 列出簡要的歷史紀錄

7. 還原提交更改
---
`git status`

`git stash`

`git stash clear`

`git log`

`git log --summary`

`git log --oneline`

`git revert commitid`

{{< /split >}}
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
[35+ Git Commands List Every Programmer Should Know](https://www.loginradius.com/blog/engineering/git-commands/)