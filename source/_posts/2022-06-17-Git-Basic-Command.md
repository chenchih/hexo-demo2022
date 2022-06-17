---
title: Git Basic Command
date: 2022-06-17
tags: 
- github
categories: 
- github
---

今天我想在這文章中介紹最常用到的git指令。我會介紹我最常用到的指令有：
- git init
- git add .
- git commit -m "message"
- git push
以上是我最常用到的。我還想介紹一些關於git remote 等指令。

## 基本指令

### 1. git init 初始化 git
Step1: 建立一個資料夾如：`$mkdir test`
Step2: 進去目錄 `cd test`
Step3: 執行 `git init`就會初始化 git。如果你下 `ls-al`就可以看所有資料，會有一個 `.git` 隱藏檔

### 2. git add 把檔案進索引index
Step1: 建立檔案 `touch hello.py`
Step2: 編輯檔案
- (linux) vim hello.py
- (window) notepad hello.py
就加 `print('hello world`)`
Step3: 把檔案加進索引 `git add .` 
Step4: 看git status  `git status`
他會顯示stage 

### 3. git commit
我們準備要把他推到我們本地local repository，請下以下指令：
> `git commit -m "add hello.py " `
`-m`: message，後面是你要推的信息


### 4. git log 
我們可以用這個指令`git log --oneline` 來看我們有commit 成功嘛。這個指令很常用。我們可以看到我們的commit hash，這可以讓我們環原我們檔案等等。
有幾個參數可以用：
- git log ：顯示相細訊息
- git log --oneline: 只顯示基本信息
- git log --oneline --graph : 可以顯示你的分支相關圖
- git log --oneline HEAD -N : HEAD 0 就是最新個commit，N可以顯示最新幾筆

### 5. git push
我們需要去giuthub建立我們自己的repository(專案)。建立完他會給我們一些提示，我們需要把本地跟遠端連再一起。

- local跟remote 連結
```
$git remote add origin https://github.com/username/<repoistory>.git
$git branch -M main #add local main branch
$git push -u origin main #add main remote branch
```
Note: 上面的`-u`：他會記錄你的repository名字，你下次要push上去，就可以直接下`git push`就不用下 `git push -u origin`

- 正常push command 
上面指令只需要在第一次用，下次你要push上說，只要下`git push`就好。

## 基本remote 相關指令
- 如果你相要改你個remote reposioty名字，或你加錯，我們都可以改。
    - 檢查我們的repository連結 check remote repository url：
    > `git remote -v`
    - 移除我們remote repository: 
    > `git remote rename <oldname> <newname>`
    - 改名remote repository: 
    > `git remote remove <name>`

## Branching 
### 1. 建立本地分支（只建立分支）
> `$git branch <branchname>` # create branchname
> `$git checkout <branchname>` # check branchname

### 2. 建立和切換分支Create a branch and switch 
> `$git checkout -b <branchname>` # create branch and switch
> `git switch -c <branchname>` # create branch and switch

### 3. check branch 檢查分支
> `$git branch` or `$git branch -l` # 本端分支，預設list local branch
> `$git branch -r` # list remote branch 遠端分支
> `$git branch -a` #全部分支 list all branch local and remote

### 4. 刪除分支 Delete branch 
- 刪除本地分支local branch
    > `$git branch -d <branchname>` # delete local branch
        `-d`: merge
        `-D` : no merge
- 刪除遠端分支remote branch
    > `$git push <remote name> --delete <remote branch name>` #delete remote branch

## remote branch (進階) 
### 1. 建立遠端分支第一次(建完git init)
> `git push --set-upstream <remote repository> <branch-name>`
>> Example: 
>> `git push --set-upstream origin newbranch1`

### 2. 刪除遠端分支
> `git push origin --delete newbranch1`
>>  or 也可以用這個
>> `git push <remote> :<branch>`

### 3. 本地切換遠端分支switch remote branch 
我們如果clone repository，只會有master被clone下來，分支不會下載。因此我們需要切換到remote branch。以下是切換方法:
> #假如我有 main和test
> `git branch -a` #list all remote local branch ，local沒看到test分支
> `git checkout origin/test` #test是遠端分支
> `git switch -` #切到master或main
> `git switch test `

這時就會有test分支

### 4. fetch --prune 把遠端分支在本地同步
我們在server 刪除 remote branch 可是在本地 branch -r 還是有看到，此時我們就要用這指令
> `git branch -r`
> `git fetch --prune`


## 結論
以上是最基本指令，我後續我再放一些高階的指令上去。