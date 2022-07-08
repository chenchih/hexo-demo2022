---
title: windowOS-製作動畫.xml
date: 2022-06-25 08:07:07
tags: window
categories:
- window
---

大家有用過自動安裝window 系統嗎？正常我們都用 ISO光碟片，USB和網路方法安裝OS。可這些方法我們可能要一直按下一步等等。今天我想分享如何用自動化安裝，不需要寫程式，只要把`unattend.xml`放進我們window ISO 或是USB的根目錄就可以。
這個自動化工具叫做unattend 如果有興趣可以在網路找相關內容。 
我會教大家如何建立`unattend.xml`檔案，他可以幫我們自動建立帳號，切磁區等等。在這分享我沒有教如何分切磁區。

為什麼要做這個？
如果你長期在安裝`windowOS`我建議可以學會這個，非長方便。

## Part 1 : 建立`autounattend.xml` 檔案。

### 1.	去windowsafg 網站 
- 請到 [window-afg](https://www.windowsafg.com/)網站製作`autounattend.xml`檔案
- Access to [windows answer file generator](https://www.windowsafg.com/) site and create `autounattend.xml` file
![windowsafg](https://i.imgur.com/ikhlwPq.png)

### 2.	window 相關設定
用預設的設定即可。You can use the default setting, or use the same setting I set.
- 我只設定，時間，鍵盤語言，和帳號
- I only changed `time tone`, `keyboard to US`, and `account to administrator` 
![account admin](https://i.imgur.com/WDtM0RU.png)

### 3.下載`autounattend.xml`檔案
Download `autounattend.xml` file. 下載`autounattend.xml`檔案
![downloadfile](https://i.imgur.com/8PYvDsZ.png)

## Part 2 :`autounattend.xml` 放進windowOS目錄（ISO檔案或是USBdisk)。
把`autounattend.xml`檔案放進WindowOS的根目錄。add the`autounattend.xml` into window image file. 
- There are many way you can do, you just have to put your e`autounattend.xml`file into windowOS root directory. 
- 我們有多方法可以把`autounattend.xml`放進windowOS根目錄。
### 方法一：放進window ISO樣案
我們可以把剛剛下載的.xml放進window ISO檔案，以下是如何編輯我們ISO File
#### 1.	請下載`anyburn`這個工具再安裝他。 Ｄownload `anyburn` tool and install it 
#### 2.	啟動`anyburn`再選`edit image file` Open the tool and click on edit image file
![editimage](https://i.imgur.com/kisbiAK.png)
  
#### 3.	選取你的ISO檔案 Select your window iso file 
 ![select-iso-file](https://i.imgur.com/gcnbsp7.png)
 
#### 4.	Select your file `autounattend.xml` file 選取你的e`autounattend.xml`檔案
 ![xml](https://i.imgur.com/XZe9UCh.png)
 
#### 5.	Ｓave your iso name (recommend change different name) 存取新個ISO檔名(建議曲新的名字)
 ![change-iso-name](https://i.imgur.com/CEKajae.png)

#### 6.	建立windowOS USB開機 
- Your new iso image is created, right now you create a bootable usb disk using the iso file. 
- Create USB bootable file for window OS, use tool RUFUS, and select your disk 
我們已建好window ISO 檔案，現在準備製作window USB 開機碟，我們用RUFUS這套軟體。
![RUFUS-burniso](https://i.imgur.com/hOXuKYP.png)

#### 7.	You can install OS already. 現在可以安裝ＯＳ
- After install OS you have to select which window you can to install, after that all will be automatic. 
- 安裝ＯＳ請輸選你要安裝那個window版本OS，選完就會自動幫你安裝成功，什麼都不用設。等他綁你安裝完成。
### 方法2 ：放進window USB碟
- 這個是我們一般製作window ＯＳ 的開機碟，如果不知道可以參考上面的第6步。
- 我們再把我們的`autounattend.xml` 放進USB-Disk的根目錄。

## Part 3 bypass the os edition selection page 
- As you can see above setting, will still need to select which OS you need to install. To automatic not occur, there are some way you can do, edit the autounattend.xml. 
- 剛剛上面步驟你會發現我們要自己選我們要安裝那一個OS版本。在這我教大家如何自動幫我們選，重投安裝到完。

### 1.	編輯我們的`autounattend.xml`檔案 

### 2.	Check window edition vlaue 檢查我們window 11 pro的直
我們需要先知道我們要安裝的window的直是哪的，這裡有一個指令可以查看看：
> 指令: `Dism /Get-ImageInfo /ImageFile:<your_path>`
>> EXample: `Dism /Get-ImageInfo /ImageFile:F:\sources\install.wim`

**Note:** `F:` 我的Ｗindow位置。 
 ![](https://i.imgur.com/VbzK5WA.png)

以上圖你可以看的如果我們要安裝window 11 PRO，他是第5個選項，因此我們在下面步驟要把5加進去

### 3.	加window安裝OS選項進`autounattend.xml`
剛剛上面我們用指令可以查看`window 11 Pro` 是第幾個選項，他是第5個選項，我們先去編輯`autounattend.xml` ，然後把下面語法加進去。
**Ｎote:** `<Value>5</Value>`記得要填你的window的選單得直。

```
<InstallFrom>
<MetaData wcm:action="add">
<Key>/image/index</Key>
<Value>5</Value>
</MetaData>
</InstallFrom>
```
![](https://i.imgur.com/W6vgWjo.png)
