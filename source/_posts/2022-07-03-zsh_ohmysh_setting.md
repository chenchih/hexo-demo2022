---
title: UBUNTU-Zsh + Oh My Zsh + Powerlevel10k
date: 2022-07-03 09:00:18
tags:
- zsh
categories:
- devtool
---

#　前言
今天天想分享如何在terminal或終端機變成更有效率或是更美化。我們需要用到`zsh` 和 `ohmysh`。

本篇文章會安裝以下套件：
- ubuntu 安裝和設定 
    - 基本套件: `zsh` `git` `wget` `curl`
    - `ohymysh`套件
    - shell 設定
    - `Oh My Zsh` 安裝，主題設定
    - 安裝`Powerlevel10k` 主題，不然會怪怪
    
## 更新 ubuntu 套件
`$ sudo apt-get update`

## 安裝 zsh

### 檢查我們目前支援的shells
> 目前支援的shells 
> `$cat /etc/shells`

![zsh-after](https://i.imgur.com/SGzosrt.png)

>目前用的shells 
>> `$ echo $shells`

### 安裝必要的套件
```
# 安裝 git 套件
$sudo apt-get install git -y

#install zsh 套件
$sudo apt-get install zsh -y
```

## 檢查我們目前支援的shells
>目前支援的shells 
>> `$cat /etc/shells`

![zsh-after](https://i.imgur.com/shjh3uG.png)
 
>目前用的shells 
>> `$ echo $shells`

![shell](https://i.imgur.com/1OtykFv.png)


## 安裝　oh-my-zsh
Ubuntu 已經有安裝`wget`，你可以選擇用`wget`或`curl`方式來安裝`oh-my-zsh`。
如果你電腦沒安裝可以用下面指令，會把兩套下載工具的套件安裝。

- curl 和wget 
> `$ sudo apt install wget git curl vim -y`

- 下面是安裝oh-my-zsh方法：

### - curl　
```
# via curl
$sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
or
### - wget
```
#via wget
$sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```
![ohmyzsh](https://i.imgur.com/aSImOnn.png)

##　oh-my-zsh 配置修改
### 修改SHELL預設default設定
- 方法 1: 
> `$chsh -s /bin/zsh`
- 方法 2: 
> `chsh -s $(which zsh)`


### 登出或是重開機
然後把電腦登出再登入或是重開機，再次開啟 Terminal 就可以看到自動進入 oh-my-zsh 了，此時開啟會如下圖：

### 主題下載
- 我們可以到[官方](https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes)提供的主題 中挑選喜歡的主題。
- 以這個例子我選下載　[`Bullet train`](https://github.com/caiogondim/bullet-train.zsh)

#### 下載 bullet-train
- 有兩方法可以下載：
    - git clone 方法 
    > `git clone https://github.com/caiogondim/bullet-train.zsh.git`
    - 網頁下載 方法
 
- 下載完會有出現`bullet-train.zsh-theme`，把他方進 `~/.oh-my-zsh/themes`資料夾


```
cd ~
cd downloads
#download bullet-train theme
git clone https://github.com/caiogondim/bullet-train.zsh.git
# cd to directory
cd bullet-train.zsh
# move the file to ohmyzsh theme folder
mv bullet-train.zsh .~/.oh-my-zsh/themes
```
![clone-bullet](https://i.imgur.com/VUwf4MU.png)

### 主題修改
### 檢查themes
![checktheme](https://i.imgur.com/yIxezj6.png)
#### 修改 `~/.zshrc`
`$sudo nano  ~/.zshrc`
or
`$sudo gedit  ~/.zshrc`

> ZSH_THEME="bullet-train"
![changetheme](https://i.imgur.com/hF7mZqB.png)

#### 重啟 therminal 
- 重啟 therminal 
你會發現格式怪怪的，亂碼。我們需要下載 powerline
- 下載 powerline
> `$ sudo apt-get install powerline`
> `$ sudo apt-get install fonts-powerline`
- 重啟 therminal 
![bulletetheme](https://i.imgur.com/ZmWOCGk.png)

## reference
- https://medium.com/@wifferlin0505/%E5%9C%A8-ubuntu-16-04-lts-%E4%B8%AD%E5%AE%89%E8%A3%9D%E4%BD%BF%E7%94%A8-oh-my-zsh-cf92203ca8a2
- https://joechang0113.github.io/2020/03/23/ubuntu-install-oh-my-zsh.html
- https://www.kwchang0831.dev/dev-env/ubuntu/oh-my-zsh