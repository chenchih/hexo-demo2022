---
title: substringSearchg檔案內容搜尋相關關鍵字
date: 2022-10-18 17:44:27
tags: python fileIO search
categories:
- python
---

今天分享如何搜尋字串裡面的substring或如果有檔案(log)想找相關字來做分析。


## spit 方式
我的string是: 
> `st="[20221013.162853.788442][info]:[[40;32m>>> DL- ingress traffic: 0.010799(Mbps), egress traffic: 0.087016(Mbps), ReTx: 0.000220(Mbps)[0m]"`

我想抓出**時間**和**TPUT**的直，如:
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
```
subString = st.split(" DL- ingress traffic:", 1)[1]
TPUT=subString.split(',')[0]
TPUT=TPUT.split('(')[0]
```
以上的方法很簡單的方法，但是這種方法很不好因為如果整個索引改變了我們程式就會壞了。我現在都是用split，他就是用我們的索引在切。還有一個問題就是程是不乾靜，因此如果有更好方法避免用此方法。下面我會用regular expression方法呈現出我們要找的直。


## Regular expression
Regular Expression 也好用，下面只教如何抓取時間。 以下我會介紹紹不同的例子抓取相關字串string

我們需要`import re`

Regular expression 有以下的方式可以用:
- match()
- search()
- findall()
- finditer()


### Step 1 抓取時間或是數字
繼續從上面字串的例子，用不同regular expression方法。
- Example1: 
```
import re
s = "list[20221013.162853.788442]"
m = re.search(r"\[([0-9.]+)\]", s)
print(m.group(1) ) #20221013.162853.788442
```
> output:
>> 20221013.162853.788442

- Example2:
我們也可以下這樣:
```
regex = re.compile(r'[2]\d{7}\.\d{6}\.\d{6}') #'[2] start with 2
match = regex.search(string)
print(match.group(0)) #20221018.165317.401606
```

- Example3: 
 `([12]\d{3}-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01]))`

如果有**文字**可以這樣用，我在 stackoverflow看到
```
s = "alpha.Customer[cus_Y4o9qMEZAugtnW] ..."
m = re.search(r"\[([A-Za-z0-9_]+)\]", s)
print(m.group(1) ) #cus_Y4o9qMEZAugtnW
```
> output:
>> cus_Y4o9qMEZAugtnW

### Step 2抓取TPUT直和其他直

#### re.search()方式
抓取時間和TPUT的直:
> re.search(r'\[(\d+\.\d+\.\d+)\].*?(Tput=[^]]+)', string)
```
import re
string = "[20221018.165317.401606][info]:[DL- UE[ 0]: Tput= 0.000091 Mbps, Mcs= 9.0(Sigma= 0.0), RbNum= 1.4, ReTxRatio= 33.3, Layers= 1.0, PdschBler= 0.0, nonWPdschBler= 33.3]"
m1 = re.search(r'\[(\d+\.\d+\.\d+)\].*?(Tput=[^]]+)', string)
#group(1) => 20221018.165317.401606
#group(2) => Value=    0.000091 Mbps, Mcs=  4.0(Sigma= 0.0), Num=   1.4
print(m1.group(2))
newstr=m1.group(2).split(' ')
print(m1.group(1),'\nTPUT:', newstr[1], '\nMcs',newstr[4].split('(')[0],'\nRb',newstr[7].split(',')[0])

##output
#20221018.165317.401606 
#TPUT: 0.000091 
#Mcs 9.0 
#Rb 1.4
```

#### re.findall() 方式 
抓取`數字.數字`相關的直:
> re.findall(r"[0-9]*\.[0-9]+", string)

你們會好氣為什麼我要用`newstr=search[2:-1]` ，我的目的在這裡主要是又取所有直，如果們有時間會被抓取下來。你有發現我取的直都是X.X的直，所以所有府和他的都會抓取。時間日期也會但是時間格式有3對，最後一段不會被抓取，因此在這裡我們不需要日期才把索引從`[2:-1]`，`-1`最到最後索引。


```
m2=re.findall(r"[0-9]*\.[0-9]+", string)
newstr=m2[2:-1] #split time with value
#['20221018.165317', '.401606', '0.000091', '9.0', '0.0', '1.4', '33.3', '1.0', '0.0', '33.3']
newstr=search[2:-1] #split time with value
print(newstr)
#
```

> output:
>> `['0.000091', '9.0', '0.0', '1.4', '33.3', '1.0', '0.0']`

#### re.search and re.sub() 方式 

`re.sub()`:取代參數
在這個例子我會做以下的事情：
- 移除 `()` `[]` : 用 `re.sub("[\(\[].*?[\)\]]", "", string)`
- 移除 `()`: `re.sub("[\(].*?[\)]", "", string)`
- 移除 `,`:use `replace`
- `split()`: 轉成list

```
m3 = re.search(r'\[(\d+\.\d+\.\d+)\].*?(Mcs=+)*?(Tput=[^]]+)', string)
#'Tput= 0.000091 Mbps, Mcs= 9.0(Sigma= 0.0), RbNum= 1.4, ReTxRatio= 33.3, Layers= 1.0, PdschBler= 0.0, nonWPdschBler= 33.3'
#remove () [] for ((Sigma= 0.0)), 移除ˇ多個空白，把 
m3New= re.sub("[\(\[].*?[\)\]]", "",m3.group(3)).replace(',','').split() #convert to list
```

>output:
>> `['Tput=', '0.000091', 'Mbps,', 'Mcs=', '9.0,', 'RbNum=', '1.4,', 'ReTxRatio=', '33.3,', 'Layers=', '1.0,', 'PdschBler=', '0.0,', 'nonWPdschBler=', '33.3']`


我們可以找相關字串，就把後面直給我們(非常推薦這這個方式)

```
def getelement(li, element):
    ind = li.index(element)
    return li[ind+1]

# get next element 
print(getelement(m3New, 'Tput='),' ', getelement(m3New, 'RbNum='), '', getelement(m3New, 'Mcs='))
# 0.000091   1.4  9.0
```

>output:
>> `0.000091   1.4  9.0`

#### re.search()
```
#method4
m4=re.search(r"^\[([\d\.]+).+Tput= ([\d\.]+).+Mcs= ([\d\.]+).+RbNum= ([\d.]+).+ReTxRatio= ([\d\.]+).+.", string)
print(m4.group())
#m4.group(1) =>20221018.165317.401606
#m4.group(2) => 0.000091 
#m4.group(3) =>9.0
#m4.group(4) =>1.4
```
### Step 3 把直加進list 再印出來

我們幫剛才用regular expression找相關的字串，現在我們要把我們的直丟進list 裡面，再印出來或寫出來等等都可以做到。
我們有不同做法:

#### List Comprehensions 簡短
下面方法是我要印時間和Tput直，只有欄，因此我就用`%2`
```
for i in [result[c:c+2] for c in range(0,len(result)) if c%2 == 0]:
    print(*i) 
```

#### 轉成正常for loop
以面的方式如果你不習慣用Comprehensions可以用下面方式，這是一般for loop，如果你不喜歡用List Comprehensions。
- 方法一
```
temp = []
for c in range(0, len(results)):
    if c % 2 == 0:
        temp.append(results[c:c+2])

for i in temp:
    print(*i)
```

- 方法二 (用*)
`*list`，這是python新功能，他主要是你不用再用`for回圈`把list讀出來，用`*list`名稱就可以，非常方便
```
results = ['A', 'B', 'C', 'D']
for index, c in enumerate(results):
    if index % 2 == 0:
        print(*results[index:index + 2])
```

#### 用 zip 最好方式
```
results = iter(["A", "B", "C", "D"])
for i in zip(results, results):
    print(*i)
```

### 完整程式
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

## 補充另外例子
上面你們看到式如何抓取時間和相關Tput直。在這我想再分享另外一個直
今天我們有字串string為:

> string2= `[20221110.112127.316856][info]:[PDCP DL- ingress traffic: 0.000000(Mbps), egress traffic: 0.000000(Mbps)]`

我們想要抓取 ingress traffic 的 `0.000000` egress traffic 的 `0.000000 `

- re.search()方法
```

searchtest=re.search(r'(ingress [^(]+).+(egress [^(]+)',string2)
test= searchtest.group(1)+", "+ searchtest.group(2)
#ingress traffic: 0.000000, egress traffic: 0.000000
test1=test.replace(", ", ":").strip().split(':')
```
> output
>> `['ingress traffic: 0.000000', 'egress traffic: 0.000000']`

- re.findall()方法
```
search2 = re.findall(r'^\[([\d\.]+).+ingress traffic: ([\d\.]+).+egress traffic: ([\d\.]+).+.', string2)
#[('20221110.112127.316856', '0.000000', '0.000000')]
#convert to list 
import itertools
out = list(itertools.chain(*findtest))
print(out)
```
> output
>> `['ingress traffic: 0.000000', 'egress traffic: 0.000000']`

- 方法3 指定給一個參數
```
searchresult=re.search(r'ingress traffic: ([\d\.]+).+ egress traffic: ([\d\.]+)',string2)
ingress= searchresult.group(1) 
egress = searchresult.group(2)
```
或是用`\s`空白方法(小寫s是空白，大寫S是沒空白)
```
ingress =re.search(r'(ingress traffic):\s+(\d+.\d+)',string2)
#ingress traffic: 0.590000   
egress =re.search(r'(egress traffic):\s+(\d+.\d+)',string2)
#egress traffic: 0.000000
print(ingress.group(2), " ", egress.group(2))
#0.590000  0.000000
```

## 總結
以上是我再抓取檔案裡的資料想找相關字串會用到，我想信很多人會常用到此功能。可以到我github看完整code。
我開發3個不同抓取資料，主要是要抓取資料不同，再把資料解成文字檔案，也可以轉成excel。
github project: https://github.com/chenchih/5G_automationLinux/tree/main/log_graph
=======
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
寫檔案:
```
with open('output.txt', 'a') as output:
    results = ['A', 'B', 'C', 'D']
    for index, c in enumerate(results):
        if index % 2 == 0:
            print(*results[index:index + 2], file=output)
```

- 用 zip 最好方式
```
results = iter(["A", "B", "C", "D"])
for i in zip(results, results):
    print(*i)
```

-方法４
```
results = ['A', 'B', 'C', 'D']
for index in range(0, len(results), 2):
    print(*results[index:index + 2])
```

write file:
```
results = iter(["A", "B", "C", "D"])
with open('output.txt', 'a') as output:
    for i in zip(results, results):
        print(*i, file=output)
```



## reference:
- https://stackoverflow.com/questions/8569201/get-the-string-within-brackets-in-python
- https://www.rexegg.com/regex-quickstart.html
- https://python-tutorials.in/python-regular-expressions/