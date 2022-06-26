---
title: 無密碼-遠端桌面連線和分享網路磁碟
date: 2022-06-25 08:06:54
tags: window
categories:
- window
---
## 遠端桌面連線
我想分享如何設定**無密碼**，也可以做遠端桌面連線。正常都是我們電腦帳號如果設定無密碼但又想做遠端，需要作揖些設定。


### Step1: 請在鍵盤輸入`window + r`
### Step2: 請輸入`gpedit.msc`
### Step3: disable Limit account use of blank password, to enable blank password　
![blank password](https://i.imgur.com/TSEfiQi.png)

## 網路磁碟分享
我想分享如何設定**無密碼**，也可以做網路磁碟分享，這樣可以共享資料夾。

### Step1: 建立一個資料夾
### Step2: 把資料夾設定權限
### Step３: 設定無密碼設定
請到:`控制台\所有控制台項目\網路和共用中心\進階共用設定`設下面設定
![enable blank password](https://i.imgur.com/TSEfiQi.png)