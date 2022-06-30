---
title: windowOS-automation
date: 2022-06-25 08:07:07
tags: window
categories:
- window
---

大家有用過自動安裝window 系統嗎？正常我們都用 ISO光碟片，USB和網路方法安裝OS。可這些方法我們可能要一直按下一步等等。今天我想分享如何用自動化安裝，不需要寫程式，只要把`unattend.xml`放進我們window ISO 或是USB的根目錄就可以。

這個自動化工具叫做unattend 如果有興趣可以在網路找相關內容。

我會教大家如何建立`unattend.xml`檔案，他可以幫我們自動建立帳號，切磁區等等。在這分享我沒有教如何分切磁區。


- 為什麼要做這個？
如果你長期在安裝`windowOS`我建議可以學會這個，非長方便。

## Part 1 : 建立`autounattend.xml` 檔案。 Create a automation `autounattend.xml`
#### 1.	去windowsafg網站
請到 [window-afg](https://www.windowsafg.com/)網站建立`autounattend.xml`檔案
Access to [windows answer file generator](https://www.windowsafg.com/) webpage to create `autounattend.xml` file
![windowsafg](https://i.imgur.com/ikhlwPq.png)

#### 2.	用預設的設定 You can use the default setting, or use the same setting I set.
我只設定，時間，鍵盤語言，和帳號
I only changed `time tone`, `keyboard to US`, and `account to administrator` 
![account admin](https://i.imgur.com/WDtM0RU.png)

#### 3.	Download `autounattend.xml` file. 下載`autounattend.xml`檔案
![downloadfile](https://i.imgur.com/8PYvDsZ.png)

## Part 2 : 把`autounattend.xml`檔案放進WindowOS的根目錄 add the`autounattend.xml` into window image file. 
- There are many way you can do, you just have to put your e`autounattend.xml`file into windowOS root directory. 
- 有很多方法可以做，這藥就是把e`autounattend.xml`放進windowOS根目錄。

#### 1.	請下載`anyburn`這個工具再安裝他。 Ｄownload `anyburn` tool and install it 
#### 2.	啟動`anyburn`再選`edit image file` Open the tool and click on edit image file
![editimage](https://i.imgur.com/kisbiAK.png)
  
#### 3.	Select your window iso file 選取你的ISO檔案
 ![select-iso-file](https://i.imgur.com/gcnbsp7.png)
 
#### 4.	Select your file e`autounattend.xml` file 選取你的e`autounattend.xml`檔案
 ![xml](https://i.imgur.com/XZe9UCh.png)
 
#### 5.	Ｓave your iso name (recommend change different name) 存取新個ISO檔名(建議曲新的名字)
 ![change-iso-name](https://i.imgur.com/CEKajae.png)


#### 6.	建立windowOS USB開機 
- Your new iso image is created, right now you create a bootable usb disk using the iso file. 
- Create USB bootable file for window OS, use tool RUFUS, and select your disk 
我們已建好window ISO 檔案，現在準備製作window USB 開機碟，我們用RUFUS這套軟體。
![RUFUS-burniso](https://i.imgur.com/hOXuKYP.png)

#### 8.	You can install OS already. 現在可以安裝ＯＳ
- After install OS you have to select which window you can to install, after that all will be automatic. 
- 安裝ＯＳ請輸選你要安裝那個window版本OS，選完就會自動幫你安裝成功，什麼都不用設。等他綁你安裝完成。


## Part 3 bypass the os edition selection page 
- As you can see above setting, will still need to select which OS you need to install. To automatic not occur, there are some way you can do, edit the autounattend.xml. 
- 剛剛上面步驟你有發現我們還要選我們要安裝的OS。在這我們也可以自動化，不需要選，自動綁我們選我們要哪一個版本。

#### 1.	編輯我們的`autounattend.xml`檔案 Modify `autounattend.xml`, usb disk just go to edit the file

#### 2.	Check window edition vlaue 檢查我們window 11 pro的直
我們可以查看我們所有版本的直是什麼。我們可以用這個語法去查。
Ｗe can check value of all edition is, 
 ![](https://i.imgur.com/VbzK5WA.png)
#### 3.	Add this below will not pop the edition selection page 把下面語法加進去就可以
以我為例我的WIN11Pro是第5個選項，所以我會放5在`value`請看下面語法。As my example win 11 pro is the fifth one, so i will add 5 to my `value` as below 
```
<InstallFrom>
<MetaData wcm:action="add">
<Key>/image/index</Key>
<Value>5</Value>
</MetaData>
</InstallFrom>
```
![](https://i.imgur.com/W6vgWjo.png)
