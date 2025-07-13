---
title: Python to exe
date: 2025-06-25 18:35:53
tags:
  - python
categories:
  - python
---

今天想分享如何用 python 轉 exe，也就是說如果你把你的 python 檔案轉成 exe 放在其他電腦就可以執行。這個好處就是你不用在其他電腦安裝 python 或其他 library，就可以用。

## Install Pyinstaller

這有很多方法和套件可以用，但我都用 `pyinstaller`

> 安裝 pyinstaller: `pip install pyinstaller`

## pyinstaller 用法

- 基本用法

```
#simple convert
pyinstaller your_script.py
```

- Adding Icons:

可以在下面連結下載 ico 也可以用，下載會是 `.png`檔案，需要轉成 `.ico`

```
pyinstaller --onefile --icon=myicon.ico your_script.py
```

> - [Icon URL](https://www.flaticon.com)
> - [png to ico](https://convertio.co/zh)

- 其他

```
#Single File:
pyinstaller --onefile your_script.py

#Adding Icons:
pyinstaller --onefile --icon=myicon.ico your_script.py

#no console window:
pyinstaller --onefile --windowed your_script.py

#Adding Data Files:
pyinstaller --onefile --add-data "data_file.txt;." your_script.py
```

## Linux 環境也可以用

如果你要在 linux 上面做一個執行當也可以:

```
#build to executable file
pyinstaller --onefile script.py

#run executable file
./dist/executfile
```
