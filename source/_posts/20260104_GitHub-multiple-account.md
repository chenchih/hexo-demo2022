---
title: GitHub_multiple_account
date: 2026-01-04 08:29:34
tags:
  - ssh
  - github
categories:
  - Linux
---

# Setup Multiply Github account via SSH

## 1. Generate separate SSH keys
```
# personal account
ssh-keygen -t ed25519 -C "email@personal_mail.com" -f ~/.ssh/id_personal

#work account
ssh-keygen -t ed25519 -C  "email@work_mail.com"  -f  ~/.ssh/id_rsa_work_user1
```
it will generate file private and public:
```
~/.ssh/id_personal
~/.ssh/id_personal.pub
~/.ssh/id_rsa_work_user1
~/.ssh/id_rsa_work_user1.pub
```
## 2. Add public keys to GitHub
1. GitHub → Settings
2. SSH and GPG keys
3. New SSH key
4. Paste the `.pub` file content

## 3. Registering the new SSH Keys with the ssh-agent

```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_personal
ssh-add ~/.ssh/id_rsa_work_user1
```

- List key: `ssh-add -l`
- 刪除則使用: `ssh add -d ~/.ssh/id_personal`
- 刪除全部: `ssh-add -D`

## 4. confgiure ssh by create SSH config File

- create ssh config
Edit config file
```
nano ~/.ssh/config
```
or manually create it
```
cd ~/.ssh/
touch config           // Creates the file if not exists
code config            // Opens the file in VS code, use any editor
```
- change permission: `chmod 600 ~/.ssh/config`

- Edit config
```

# Personal account, - the default config
Host github-personal
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_personal
   IdentitiesOnly yes
# Work account-1
Host github-work  
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa_work_user1
   IdentitiesOnly yes
```

Note:
IdentitiesOnly yes: Use only this key, no guessing. prevents SSH from trying the wrong keys

## 5. test ssh work
```
ssh -T git@github-work  
ssh -T git@github-personal 
```
## 6.  clone use correct ssh host

When git clone you need to change it's hostname from `git@github` to setting you se in `.ssh/config` this distinguish multiply account.  

If i was to git clone my repo like below picture which github gave URL `git@github.com:jakccl/helloTest.git` need to change to `git@github-personal`. If you only have one account then you can use what github gave `git@github.com`

{% asset_img git_url.png %}


```
#work
git clone git@github-work:username/repo.git 
#personal
git clone git@github-personal:username/repo.git
```

{% asset_img git_clone.png %}

## 7. Git identity per repo(optional)
- global
```
[user]
  name = Jak Lee
  email = personal@gmail.com
```
- Personal
```
cd project
git config user.name "Jak Lee"
git config user.email "personal@gmail.com"
```

- work
```
cd project2
git config user.name "Jak Lee"
git config user.email "work@company.com"
```
Note:
These settings are stored in  `project1/.git/config` and `project2/.git/config`
They override global `~/.gitconfig` for that repo

- check: `git config --get user.email`

A better way might be seperate folder for work and personal.

# Create Seperate Directory for github 

```
~/Code/
├── personal/    # 個人專案
└── work/        # 工作專案
```


## 1. configure git global config
```

[user]
    name = Your Default Name
    email = default@example.com

# 個人專案
[includeIf "gitdir/i:~/Code/personal/"]
    path = ~/Code/personal/.gitconfig

# 工作專案  
[includeIf "gitdir/i:~/Code/work/"]
    path = ~/Code/work/.gitconfig
```

## 2. Personal `~Code/personal/.gitconfig`
~Code/personal/.gitconfig
```
[user]
  name = CC
  email = personal@gmail.com

```
## 3. work `~Code/work/.gitconfig`
```
[user]
  name = CC
  email = work@company.com
```

## 4. Check and verify 
- check config
```
git config --show-origin --get user.email
git config --show-origin --get user.name
```

- other git command
```
# 修正 remote URL 為 SSH
git remote set-url origin git@<你剛才設定的 SSH Host 名稱>:<Github 用戶名稱>/<Repo 名稱>.git

# 確認配置自動套用
git config user.name
git config user.email

# 檢查目前專案設定
git config --local --list

# 確認 remote URL  
git remote -v

# 測試 SSH 連線
ssh -T github.com-personal
ssh -T github.com-work
```


# reference
- https://www.youtube.com/watch?v=cm68GCEcBXU&t=34s
- https://www.freecodecamp.org/news/manage-multiple-github-accounts-the-ssh-way-2dadc30ccaca/
- https://zsl0621.cc/ripgit/pro/git-github-multi-account