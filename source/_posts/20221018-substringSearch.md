---
title: 20221018_substringSearch
date: 2022-10-18 17:44:27
tags: python
categories:
- python
---

今天分享如何搜尋字串裡面的substring或如果有檔案(log)想找相關字來做分析。

## spit 方式
我的string是: 
> `st="[20221013.162853.788442][info]:[[40;32m>>> DL- ingress traffic: 0.010799(Mbps), egress traffic: 0.087016(Mbps), ReTx: 0.000220(Mbps)[0m]"`

我想抓出時間和TPUT的直，如:
`[20221013.162853.788442]` 和 `0.010799(Mbps)` 同時要把 `[]` 和`(Mbps)`移除，可以用下面方式:


- Step1: 宣告我的string
```
st="[20221013.162853.788442][info]:[[40;32m>>> DL- ingress traffic: 0.010799(Mbps), egress traffic: 0.087016(Mbps), ReTx: 0.000220(Mbps)[0m]"
```

- Step2 抓取時間直
```
dateStr = st.split('[', 1)[1].split(']')[0]
print(dateStr) #20221013.162853.788442
```
> output:
>> 20221013.162853.788442

- Step3 抓取TPUT直
```
#一次把所有東西spit切掉 
Tput = st.split(" DL- ingress traffic:", 1)[1].split(',')[0].split('(')[0]
#如果不喜歡可以用下面一個一切
#subString = st.split(" DL- ingress traffic:", 1)[1]
#TPUT=subString.split(',')[0]
#TPUT=TPUT.split('(')[0]
print(Tput) # 0.010799
```
> output:
>> 0.010799

## Regular expression
Regular Expression 也好用，下面只教如何抓取時間。
- 數字only
```
import re
s = "alpha.Customer[20221013.162853.788442]"
m = re.search(r"\[([0-9.]+)\]", s)
print(m.group(1) ) #20221013.162853.788442
```
> output:
>> 20221013.162853.788442

- 如果有文字可以這樣用，我在 stackoverflow看到
```
s = "alpha.Customer[cus_Y4o9qMEZAugtnW] ..."
m = re.search(r"\[([A-Za-z0-9_]+)\]", s)
print(m.group(1) ) #cus_Y4o9qMEZAugtnW
```
> output:
>> cus_Y4o9qMEZAugtnW

## reference:
source: https://stackoverflow.com/questions/8569201/get-the-string-within-brackets-in-python