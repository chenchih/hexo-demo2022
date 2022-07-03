---
title: Hexo + GitHub Pages 架設個人網誌-簡易版-2
date: 2022-06-30 20:34:18
tags:
- Hexo
categories:
- Hexo
---

在這篇教學，我想要分享HEXO簡易版本。我在之前有寫ㄧ篇是關於Hexo完整篇，文章太長。如果你不想看那一篇可以看這一篇。在這一篇，我只會分享一些基本指令。

## 安裝 git
可以到官網下載[git](https://git-scm.com/):，或是你是Linux/MAC，可以輸入命令方式來安裝如下：

- Linux (Ubuntu, Debian)：
> `$ sudo apt-get install git-core`

- Linux (Fedora, Red Hat, CentOS)
> `sudo yum install git-core`

- mac 安裝:
> `brew install git`   


## 安裝 Hexo
### 先安裝 node.js 
可以到官網下載[Node.js](https://nodejs.org/en/)，或是你是Linux/MAC，可以輸入命令方式來安裝如下：
- MAC: 
> `$ brew update`
> `$ brew install node`
- Linux(ubuntu)
> `$ sudo apt-get install -y nodejs`


### 再安裝 Hexo
`$ npm install -g hexo-cli     # -g 全域安裝`

## 初始化 Hexo 資料夾
### 方法一：初始化專案或資料夾
```
$ hexo init <資料夾名稱>
$ cd  <資料夾名稱>
$ npm install
```

### 方法二：手動自己建立專案或資料夾
```
$ mkdir hexo_blogName
$ cd hexo_blogName
$ hexo init
$ npm install
```

## 修改 _config.yml 
我們可以改很多東西，但是一版人會把主題給換下，我會寫另一個文章關於改theme。以目前我們可以先改一下blog名字等等。
以我列字如下：
```
title: Chen-Chih Blog #博客blog名字
subtitle: 'Tech Note' 
description: ''
keywords:
author: chenchih  ＃作者名字
language: en  #zh-TW ＃顯示語言
timezone: Asia/Taipei ＃時區
```

## 本地端測試，啟動server

```
# 開啟新的 post
$ hexo new "post_title"

# 產生靜態網頁
$ hexo generate

# 先安裝 hexo-server
$ npm install hexo-server --save

# 接著就可以在local端預覽了
$ hexo server    # 預設在 http://localhost:4000
```

如果你的port 400被用掉，可以手動改其他port: `$ npm -s -p:xxx ` #xxx是你要的port

## 把檔案發布到 GitHub，修改`_config.yml`
請先去你的github建立你的專案和github page等等。
請打開`_config.yml`檔案，我們要改修我們github page 的連結
### 修改github page`url`設定
把我們github page網域填上去`url` 和 `root` 參數如下：
```
 # URL
 ## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
  url: https://<username>.github.io
  root: /
  permalink: :year/:month/:day/:title/
  permalink_defaults:
```

> `https://<username>.github.io`
>> root: /

或

> `https://<username>.github.io/repository-name`
>> root: repository-nam


### 修改 deploy 相關設定
去找deploy 相關參數如下，把我們的repository 加進去：
```
deploy:
  type: git          
  repo: https://github.com/<username>/<username>.github.io.git  
  branch: master
```
以面的例子是如果我們只有master or main 分支。如果你不是，請改`branch`即可

 ## deploy 我們網誌推上 Github
 ### 安裝deploy-git
 為了讓我們更方便deploy誌推上到github，請先安裝`deploy-git`套件，如下面指令：
`npm install hexo-deployer-git --save`
 ### deploy 我們網誌推上
 > `hexo deploy`

 或是

 > `hexo d`

 ## 完了
 有很多git相爨設定我沒放進來，請看第一篇文章，有更詳細教學。
