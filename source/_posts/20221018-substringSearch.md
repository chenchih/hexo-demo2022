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
這裡會用到`spit`和`strip`
`spit`是把字源切開，切完只留下Tput，會發現有空白，因此在後面加`strip`把空白移除就可以。

```
#一次把所有東西spit切掉 
Tput = st.split(" DL- ingress traffic:", 1)[1].split(',')[0].split('(')[0].strip()
#如果不喜歡可以用下面一個一切
print(Tput) # 0.010799
```
> output:
>> 0.010799

想說明以下，我很懶不想一個一個切，因為不想宣告多的變數，所以一次把他切。如果妳想一個一 個用可以用這樣方法:
#subString = st.split(" DL- ingress traffic:", 1)[1]
#TPUT=subString.split(',')[0]
#TPUT=TPUT.split('(')[0]

## Regular expression
Regular Expression 也好用，下面只教如何抓取時間。
- 數字only
```
import re
s = "list[20221013.162853.788442]"
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

## 用毒檔案方式(最實用)
我把切格方式加進function，妳也可以不用加到function。我再把它存進list裡面。

```
givenString = "DL- ingress traffic"
result = []
#function spit time and tput value
def timeparse(data):         
    datestr = data.split('[', 1)[1].split(']')[0]
    Tput = data.split(" DL- ingress traffic:", 1)[1].split(',')[0].split('(')[0].strip()
    result.append(datestr)
    result.append(Tput)
    print(datestr, Tput)
    #return datestr

with open('elog', 'r') as filedata:
    for line in filedata:   
        if givenString in line:

             # Print the line, if the given string is found in the current line
             #print(line)
             timeparse(line)

print ("="*30)
print(result)
#把list 面東西印出來
for i in [result[c:c+2] for c in range(0,len(result)) if c%2 == 0]:
    print(*i)       
```

### 以下有幾個方法可以印出list+換行

-  List Comprehensions 簡短
```
for i in [result[c:c+2] for c in range(0,len(result)) if c%2 == 0]:
    print(*i) 
```

- 轉成正常for loop
方法一
```
temp = []
for c in range(0, len(results)):
    if c % 2 == 0:
        temp.append(results[c:c+2])

for i in temp:
    print(*i)
```
或是

方法二
```
results = ['A', 'B', 'C', 'D']
for index, c in enumerate(results):
    if index % 2 == 0:
        print(*results[index:index + 2])
```

- 用 zip 最好方式
```
results = iter(["A", "B", "C", "D"])
for i in zip(results, results):
    print(*i)
```



## reference:
source: https://stackoverflow.com/questions/8569201/get-the-string-within-brackets-in-python