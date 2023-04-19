---
title: substringSearchg檔案內容搜尋相關關鍵字
date: 2022-10-18 17:44:27
tags:
  - python
  - fileIO
  - search
  - regExp
categories:
  - python
---

今天分享如何搜尋字串裡面的 substring 或如果有檔案(log)想找相關字來做分析。

## split() 方式

我的 string 是:

> `st="[20221013.162853.788442][info]:[[40;32m>>> DL- ingress traffic: 0.010799(Mbps), egress traffic: 0.087016(Mbps), ReTx: 0.000220(Mbps)[0m]"`

我想抓出**時間**和**TPUT**的直，如:
`[20221013.162853.788442]` 和 `0.010799(Mbps)` 同時要把 `[]` 和 `(Mbps)`移除，可以用下面方式:

- Step1: 宣告我的 string

```
st="[20221013.162853.788442][info]:[[40;32m>>> DL- ingress traffic: 0.010799(Mbps), egress traffic: 0.087016(Mbps), ReTx: 0.000220(Mbps)[0m]"
```

- Step2 抓取時間直

```
dateStr = st.split('[', 1)[1].split(']')[0]
print(dateStr) #20221013.162853.788442
```

> output:
>
> > 20221013.162853.788442

- Step3 抓取 TPUT 直
  這裡會用到 `spit`和 `strip`
  `spit`是把字源切開，切完只留下 Tput，會發現有空白，因此在後面加 `strip`把空白移除就可以。

```
#一次把所有東西spit切掉
Tput = st.split(" DL- ingress traffic:", 1)[1].split(',')[0].split('(')[0].strip()
#如果不喜歡可以用下面一個一切
print(Tput) # 0.010799
```

> output:
>
> > 0.010799

想說明以下，我很懶不想一個一個切，因為不想宣告多的變數，所以一次把他切。如果妳想一個一 個用可以用這樣方法:

```
subString = st.split(" DL- ingress traffic:", 1)[1]
TPUT=subString.split(',')[0]
TPUT=TPUT.split('(')[0]
```

以上的方法很簡單的方法，但是這種方法很不好因為如果整個索引改變了我們程式就會壞了。我現在都是用 split，他就是用我們的索引在切。還有一個問題就是程是不乾靜，因此如果有更好方法避免用此方法。下面我會用 regular expression 方法呈現出我們要找的直。

## Regular expression

Regular Expression 也好用，下面只教如何抓取時間。 以下我會介紹紹不同的例子抓取相關字串 string

我們需要 `import re`

**Regular expression method** 有以下的方式可以用:

- match()
- search()
- findall()
- finditer()
  |

reference: https://cheatography.com/davechild/cheat-sheets/regular-expressions/

### Step 1 抓取時間或是數字

繼續從上面字串的例子，用不同 regular expression 方法。

- Example1: 時間

```
import re
s = "list[20221013.162853.788442]"
m = re.search(r"\[([0-9.]+)\]", s)
print(m.group(1)) #20221013.162853.788442
```

> output:
>
> > 20221013.162853.788442

- Example2:
  我們也可以下這樣:

```
regex = re.compile(r'[2]\d{7}\.\d{6}\.\d{6}') #'[2] start with 2
match = regex.search(string)
print(match.group(0)) #20221018.165317.401606
```

- Example3:
  `([12]\d{3}-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01]))`

如果有**文字**可以這樣用，我在 stackoverflow 看到

```
s = "alpha.Customer[cus_Y4o9qMEZAugtnW] ..."
m = re.search(r"\[([A-Za-z0-9_]+)\]", s)
print(m.group(1) ) #cus_Y4o9qMEZAugtnW
```

> output:
>
> > cus_Y4o9qMEZAugtnW

### Step 2 抓取日期和 TPUT 直和其他直

#### re.search()方式

抓取時間和 TPUT 的直:

> `re.search(r'\[(\d+\.\d+\.\d+)\].*?(Tput=[^]]+)', string)`
>
> | group | output                                                                                                                   |
> | ----- | ------------------------------------------------------------------------------------------------------------------------ |
> | 1     | 20221018.165317.401606                                                                                                   |
> | 2     | Tput= 0.000091 Mbps, Mcs= 9.0(Sigma= 0.0), RbNum= 1.4, ReTxRatio= 33.3, Layers= 1.0, PdschBler= 0.0, nonWPdschBler= 33.3 |

```
import re
string = "[20221018.165317.401606][info]:[DL- UE[ 0]: Tput= 0.000091 Mbps, Mcs= 9.0(Sigma= 0.0), RbNum= 1.4, ReTxRatio= 33.3, Layers= 1.0, PdschBler= 0.0, nonWPdschBler= 33.3]"
m1 = re.search(r'\[(\d+\.\d+\.\d+)\].*?(Tput=[^]]+)', string)
#group(1) => 20221018.165317.401606
#group(2) => Value=    0.000091 Mbps, Mcs=  4.0(Sigma= 0.0), Num=   1.4
print(m1.group(2))
print(m1.group(1),'\nTPUT:', newstr[1], '\nMcs',newstr[4].split('(')[0],'\nRb',newstr[7].split(',')[0])
```

> output
>
> > #20221018.165317.401606
> > #TPUT: 0.000091
> > #Mcs 9.0
> > #Rb 1.4

#### re.findall() 方式

抓取 `數字.數字`相關的直: 會把原先的日期切掉，無法抓日期會有問題

> `re.findall(r"[0-9]*\.[0-9]+", string)`
>
> > ['20221018.165317', '.401606', '0.000091', '9.0', '0.0', '1.4', '33.3', '1.0', '0.0', '33.3']

你們會好氣為什麼我要用 `newstr=search[2:-1]` ，我的目的在這裡主要是又取所有直，如果們有時間會被抓取下來。你有發現我取的直都是 X.X 的直，所以所有府和他的都會抓取。時間日期也會但是時間格式有 3 對，最後一段不會被抓取，因此在這裡我們不需要日期才把索引從 `[2:-1]`，`-1`最到最後索引。

```
m2=re.findall(r"[0-9]*\.[0-9]+", string)
newstr=m2[2:-1] #split time with value
print(newstr)
```

> output:
>
> > ['0.000091', '9.0', '0.0', '1.4', '33.3', '1.0', '0.0']

#### re.search and re.sub() 方式 (最好方法)

`re.sub()`:取代參數
在這個例子我會做以下的事情：

- 移除 `()` `[]` : 用 `re.sub("[\(\[].*?[\)\]]", "", string)`
- 移除 `()`: `re.sub("[\(].*?[\)]", "", string)`
- 移除 `,`:use `replace`
- `split()`: 轉成 list
- `re.split(',|:')`: 兩個條件

> 're.search(r'\[(\d+\.\d+\.\d+)\].\*?(Tput=[^]]+)', string)'
> output:

| group | output                                                                                                                   |
| ----- | ------------------------------------------------------------------------------------------------------------------------ |
| 1     | 20221018.165317.401606                                                                                                   |
| 2     | Tput= 0.000091 Mbps, Mcs= 9.0(Sigma= 0.0), RbNum= 1.4, ReTxRatio= 33.3, Layers= 1.0, PdschBler= 0.0, nonWPdschBler= 33.3 |

- 把()或[]取代空白
  > `re.sub("[\(\[].*?[\)\]]", ""`

```
m3 = re.search(r'\[(\d+\.\d+\.\d+)\].*?(Tput=[^]]+)', string)
#'Tput= 0.000091 Mbps, Mcs= 9.0(Sigma= 0.0), RbNum= 1.4, ReTxRatio= 33.3, Layers= 1.0, PdschBler= 0.0, nonWPdschBler= 33.3'
#remove () [] for ((Sigma= 0.0)), 移除ˇ多個空白，把
m3New= re.sub("[\(\[].*?[\)\]]", "",m3.group(3)).replace(',','').split() #convert to list
```

> output:
>
> > ['Tput=', '0.000091', 'Mbps,', 'Mcs=', '9.0,', 'RbNum=', '1.4,', 'ReTxRatio=', '33.3,', 'Layers=', '1.0,', 'PdschBler=', '0.0,', 'nonWPdschBler=', '33.3']

我們可以找相關字串，就把後面的直給我們(非常推薦這這個方式)

```
def getelement(li, element):
    ind = li.index(element)
    return li[ind+1]

# get next element
print(getelement(m3New, 'Tput='),' ', getelement(m3New, 'RbNum='), '', getelement(m3New, 'Mcs='))
# 0.000091   1.4  9.0
```

> output:
>
> > `0.000091   1.4  9.0`

#### re.search()

```
m4=re.search(r"^\[([\d\.]+).+Tput= ([\d\.]+).+Mcs= ([\d\.]+).+RbNum= ([\d.]+).+ReTxRatio= ([\d\.]+).+.", string)
```

> output
>
> | group | output                 |
> | ----- | ---------------------- |
> | 1     | 20221018.165317.401606 |
> | 2     | 0.000091               |
> | 3     | 9.0                    |
> | 4     | 1.4                    |

### Step 3 把直加進 list 再印出來或寫進檔案

我們幫剛才用 regular expression 找相關的字串，現在我們要把我們的直丟進 list 裡面，再印出來或寫出來等等都可以做到。我們有不同做法:

#### 基本方式

如果你有 `6column`請把下面%6 改你有幾個 column。

- print result 把 list 裡面抓取資料列印出來

```
cycle = 0

    for element in result:
        cycle += 1
        #print(element, end="")

        print(element, end=" ")
        if cycle % 6 == 0:
            print("")

```

- Write into text file 把 list 裡面抓取資料寫進檔案

```
#checkfile()
cycle = 0
#    with open("result.txt", "a+") as f:
    with open(filename, "a") as f:

        cycle += 1
        for element in result:
            #print(element+ " ")
            f.write(element+ " ")
        f.write("\n")
        #f.write()
```

#### For Loop 方法

- List Comprehensions 簡短
  下面方法是我要印時間和 Tput 直，只有欄，因此我就用 `%2`

```
for i in [result[c:c+2] for c in range(0,len(result)) if c%2 == 0]:
    print(*i)
```

- List compensation 轉成基本 for loop

以面的方式如果你不習慣用 Comprehensions 可以用下面方式，這是一般 `for loop`，如果你不喜歡用 List Comprehensions，可以用下面方法

```
temp = []
for c in range(0, len(results)):
    if c % 2 == 0:
        temp.append(results[c:c+2])

for i in temp:
    print(*i)
```

#### Enumerate 方法

`*list`，這是 python 新功能，他主要是你不用再用 `for回圈`把 list 讀出來，用 `*list`名稱就可以，非常方便

- print result 把 list 裡面抓取資料列印出來

```
results = ['A', 'B', 'C', 'D']
for index, c in enumerate(results):
    if index % 2 == 0:
        print(*results[index:index + 2])
```

- Write into text file 把 list 裡面抓取資料寫進檔案

```
with open('output.txt', 'a') as output:
    results = ['A', 'B', 'C', 'D']
    for index, c in enumerate(results):
        if index % 2 == 0:
            print(*results[index:index + 2], file=output)
```

#### 用 zip 最好方式

- print result 把 list 裡面抓取資料列印出來

```
results = iter(["A", "B", "C", "D"])
for i in zip(results, results):
    print(*i)
```

- Write into text file 把 list 裡面抓取資料寫進檔案

```
results = iter(["A", "B", "C", "D"])
with open('output.txt', 'a') as output:
    for i in zip(results, results):
        print(*i, file=output)
```

- 補充如果 list 是文字

```
results = ['A', 'B', 'C', 'D']
for index in range(0, len(results), 2):
    print(*results[index:index + 2])
```

### 完整程式

我把切格方式加進 function，妳也可以不用加到 function。我再把它存進 list 裡面。

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

### Step 4 轉成 excel

在這我會用兩個不同 module 來寫入 excel，一個是 pandas，一個是 openpyxl。如果用 pandas，請兩個都要安裝，部穰會有問題。

> 安裝:
>
> > pip install openpyxl
> > pip install pandas

- openpyxl
  以下是改欄位大小: `sheet[0].column_dimensions[i].width = 2`
  文字大小: `sheet[0]['A1'].font = Font(size = 14, bold = True)`

```
import openpyxl, string
from openpyxl.utils import get_column_letter
from openpyxl.styles import Font

def excelconvertMAC(result):
    f = open(result, 'r+')  # open text
    #########if load excel file ########################
    # excel=openpyxl.load_workbook(r'D:\\test\\test.xlsx') #open excel
    excel = openpyxl.Workbook()
    sheet = excel.worksheets
    line = f.readline();  # read text
    while line:
        #list123 = []
        #list123 = line.split(sep=' ')  # convert,
        list123 = line.split()  # convert
        #remove below
        #for i in range(0, len(list123)):  # remove space
        #    list123[i] = list123[i].strip('\n')
        #sheet[0].append(list123)  # write into excel

        if list123[1] == 'Tput':
            sheet[0].append(list123)  # write into excel
        elif list123[2] == 'RbNum':
            sheet[0].append(list123)  # write into excel
        elif list123[3] == 'MCS':
            sheet[0].append(list123)  # write into excel
        elif list123[4] == 'PdschBler':
            sheet[0].append(list123)  # write into excel
        elif list123[5] == 'nonWPdschBler':
            sheet[0].append(list123)  # write into excel
        else:
            list123[1] = float(list123[1])
            list123[2] = float(list123[2])
            list123[3] = float(list123[3])
            list123[4] = float(list123[4])
            list123[5] = float(list123[5])
            sheet[0].append(list123)  # write into excel

#adjust the column width
        column = 1
        while column < 6:
            i = get_column_letter(column)
            #print(i)
            sheet[0].column_dimensions[i].width = 25

            column += 1

        sheet[0]['A1'].font = Font(size = 14, bold = True)
        sheet[0]['B1'].font = Font(size = 14, bold = True)
        sheet[0]['C1'].font = Font(size = 14, bold = True)
        sheet[0]['D1'].font = Font(size = 14, bold = True)
        sheet[0]['E1'].font = Font(size = 14, bold = True)
        sheet[0]['F1'].font = Font(size = 14, bold = True)
        #debug use
        #sheet1 = excel.worksheets[0]
        #sheet1['A1'] .font = Font(size = 24, bold = True)
        #sheet1['A1'] = 'Hello Python, Hello Excel.'
        line = f.readline()  # read next line
    #excel.save(r'C:\MAC_add_Submission\MAC_List.xlsx')
    excel.save('result.xlsx')
resultfilename=input("please enter your report txt file name: ")
#resultfilename="result.txt"
excelconvertMAC(resultfilename)
```

- pandas

```
import pandas as pd

with open("result.txt", "r") as file:
    column_names = next(file).split()
    df = pd.read_csv(file, sep=" ", names=column_names)
df.to_excel("test.xlsx", index=False)

writer = pd.ExcelWriter("test.xlsx", engine="xlsxwriter", )
df.to_excel(writer, sheet_name="Data", index=False)
sheet = writer.sheets["Data"]

# Set column widths (option)
sheet.set_column(0, len(column_names)-1, 25)

#st header's header (option)
header_format = writer.book.add_format({'bold':True, 'font_size':14})
for index, name in enumerate(column_names):
    sheet.write(0, index, name, header_format)

writer.save()
```

### 補充另外例子

上面你們看到式如何抓取時間和相關 Tput 直。在這我想再分享另外一個直
今天我們有字串 string 為:

> string2= `[20221110.112127.316856][info]:[PDCP DL- ingress traffic: 0.590000(Mbps), egress traffic: 0.000000(Mbps)]`

我們想要抓取 ingress traffic 的 `0.590000` egress traffic 的 `0.000000 `

- re.search()方法
  > `re.search(r'(ingress [^(]+).+(egress [^(]+)',string2)`
  >
  > > output
  > >
  > > | group | output                    |
  > > | ----- | ------------------------- |
  > > | 1     | ingress traffic: 0.590000 |
  > > | 2     | egress traffic: 0.000000  |

```
searchtest=re.search(r'(ingress [^(]+).+(egress [^(]+)',string2)
test= searchtest.group(1)+", "+ searchtest.group(2)
#ingress traffic: 0.590000, egress traffic: 0.000000
test1=test.replace(", ", ":").strip().split(':')
```

> output
>
> > `['ingress traffic: 0.590000', 'egress traffic: 0.000000']`

- re.findall()方法

他會回傳 list 裡面會包 tuple，如果想要全部都是 list 請用 `itertools`把他轉成 list

> `list(itertools.chain(*findtest))`

```
search2 = re.findall(r'^\[([\d\.]+).+ingress traffic: ([\d\.]+).+egress traffic: ([\d\.]+).+.', string2)
#[('20221110.112127.316856', '0.5900000', '0.000000')]

#tuple convert to list tuple轉成list
import itertools
out = list(itertools.chain(*findtest))
print(out)
```

> output
>
> > `['ingress traffic: 0.590000', 'egress traffic: 0.000000']`

- 指定給一個參數
  > `re.search(r'ingress traffic: ([\d\.]+).+ egress traffic: ([\d\.]+)',string2)`

```
searchresult=re.search(r'ingress traffic: ([\d\.]+).+ egress traffic: ([\d\.]+)',string2)
ingress= searchresult.group(1)
egress = searchresult.group(2)
```

或是用 `\s`空白方法(小寫 s 是空白，大寫 S 是沒空白)

> `re.search(r'(ingress traffic):\s+(\d+.\d+)',string2)`

```
ingress =re.search(r'(ingress traffic):\s+(\d+.\d+)',string2)
#ingress traffic: 0.590000
egress =re.search(r'(egress traffic):\s+(\d+.\d+)',string2)
#egress traffic: 0.000000
print(ingress.group(2), " ", egress.group(2))
#0.590000  0.000000
```

- re.split()

  > `newtest= re.split(': | * ', string__)`
  >
  > > output:
  > > ['ingress', 'traffic', '', '0.000000,', 'egress', 'traffic', '', '0.000000']

## Project

- Log 介紹
  ![](https://i.imgur.com/azewIA8.png)

### Case1 Layer2-SIngleUE Datetime and Ingress Tput

其實這個例子跟上面的 Step1 一樣，只是我有修改一些東西

- 讀 log 檔案

```
elogfile=input("Please enter your elog file:")
with open(elogfile, 'r') as filedata:
    for line in filedata:
        if givenString in line:
             # Print the line, if the given string is found in the current line
             #print(line.strip())
             timeparse(line)
```

- 抓取時間看 TPUT

```
datestr = data.split('[', 1)[1].split(']')[0]
Tput = data.split(" DL- ingress traffic:", 1)[1].split(',')[0].split('(')[0].strip()
```

- 寫進 list 和檔案

```
result.clear()
result.append(datestr)
result.append(Tput)
listprint() #write file =>ok
listprint2() #print =>ok
#write to file
def listprint():
    #checkfile()
    cycle = 0
    with open(filename, "a") as f:
        cycle += 1
        for element in result:
            #print(element+ " ")
            f.write(element+ " ")
        f.write("\n")
#print
def listprint2():
    cycle = 0
    for element in result:
        cycle += 1
        print(element, end=" ")
        #print ('='*30)
        if cycle % 2 == 0:
            print(" ")
```

> [完整 code](https://github.com/chenchih/5G_automationLinux/tree/main/log_graph/FinalCode/Layer2/SingleUE/timedate_tputONLY)

### Case2 Layer2-SIngleUE other value

- 選你要抓取哪個資料

```
 accepted_strings = re.compile(r"([DU]L\-\ UE(\[\s*(\d{1,2})\])?)|both$")
givenString = input("Please enter your search (Ex: DL- UE / UL- UE / UL- UE[ 0] / both:):")
```

> 你可以選以下:
>
> > 基本的 DL: `DL- UE`
> > 基本的 UL: `UL- UE`
> > 兩個都抓 DL 和 UL: `both`
> > 特定的 ID: `UL- UE[ 0]` `UL- UE[ 10]` `UL- UE[10]`  
> > 我們來看這個範例:

```
accepted_strings = re.compile(r"([DU]L\-\ UE(\[\s*(\d{1,2})\])?)|both$")
print (accepted_strings.match("DL- UE"))
print (accepted_strings.match("UL- UE"))
print (accepted_strings.match("UL- UE[ 0]"))
print (accepted_strings.match("UL- UE[10]"))
print (accepted_strings.match("UL- UE[ 10]"))
#<re.Match object; span=(0, 6), match='DL- UE'>
#<re.Match object; span=(0, 6), match='UL- UE'>
#<re.Match object; span=(0, 10), match='UL- UE[ 0]'>
#<re.Match object; span=(0, 10), match='UL- UE[10]'>
#<re.Match object; span=(0, 11), match='UL- UE[ 10]'>
```

可是如果你用 `accepted_strings = re.compile(r"([DU]L\-\ UE(\[\ {0,1}(\d)\])?)|both$")`

後面兩筆會抓不到裡面的 ID，因為他只要有兩個數字都會抓不到，只也一個數字和空台才抓到，因此我們需要用上面的才會抓到面面不管幾個 1 或 2 位數或空空白。

- 檢查和讀 log

```
if accepted_strings.match(givenString):
    if givenString =="both":
        UL = 'UL- UE'
        DL = 'DL- UE'
        writefile("UL")
        ULDLprint(UL)
        writefile("DL")
        ULDLprint(DL)
    else:
        writefile(givenString)
            with open(elogfileName, 'r') as filedata:
                for line in filedata:
                    if givenString in line:
                         parse(line, givenString)
else:
    print("Not found, please reenter correct option")
```

- 抓取時間和其他資料

```
datestr = data.split('[', 1)[1].split(']')[0]
search = re.search(r'\[(\d+\.\d+\.\d+)\].*?(Tput=[^]]+)', data)
m3New= re.sub("[\(\[].*?[\)\]]", "",search.group(2)).replace(',','').strip().split()
result.clear()
givenString=ULDLstr
```

- 寫進 list 和檔案
  當我們有抓取我要的資料時，他會是 list 的資料，這時我們要抓取他旁邊的數字的直。因此我有寫一個函數可以取旁邊的直再存進 list。

```
#取出字串旁邊的直，就可以要到取道我們要的直
def getelement(li, element):
    ind = li.index(element)
    return li[ind+1]

result.append(datestr)
result.append(getelement(m3New, 'Tput='))
result.append(getelement(m3New, 'RbNum='))
result.append(getelement(m3New, 'Mcs='))
result.append(getelement(m3New, bler1))
result.append(getelement(m3New, bler2))
listprint() #write file =>ok
```

- 寫進檔案
  把他寫進去跟上面 case1 一樣

```
def listprint():
    #checkfile()
    cycle = 0
    with open(filename, "a") as f:
        for element in result:
            #print(element+ " ")
            f.write(element+ " ")
        f.write("\n")
```

[完整 code](https://github.com/chenchih/5G_automationLinux/tree/main/log_graph/FinalCode/Layer2/SingleUE)

### Case3 Layer2-Multiply UE

- 讀 log 檔案

```
with open(elogfileName, 'r') as filedata:
        for line in filedata:
            #print(line)
            if "m>>> DL-" in  line:
                if countDL == 0:
                    emptywrite("DL")
                    writefile("DL")
                    countDL+=1
                for nextline in filedata:
                    if re.search(r'\[(\d+\.\d+\.\d+)\].*?(>>> DL- Mcs=[^]]+)', nextline):
                        #print(line, nextline, end='')
                        givenString="DL"
                        parse(line, givenString)
                        parse_bler(nextline, givenString)

                        break # so you can start looking for the first match again
```

- 抓取時間看 TPUT

```
def parse(data, ULDLstr):
    datestr = data.split('[', 1)[1].split(']')[0]
    Tputvalue=re.search(r'(ingress [^(]+).+(egress [^(]+)',data)
    m3New= Tputvalue.group(1)+", "+ Tputvalue.group(2)
    m3New_1=m3New.replace(", ", ":").strip().split(':')
    result.append(datestr)
    result.append(getelement(m3New_1, 'ingress traffic').strip())
    result.append(getelement(m3New_1, 'egress traffic').strip())
def parse(data, ULDLstr):
    blerresult = re.search(r'\[(\d+\.\d+\.\d+)\].*?(Mcs=[^]]+)', data)
    blerDL= re.sub("[\(\[].*?[\)\]]", "",blerresult.group(2)).replace(',','').strip().split()

    result.append(getelement(blerDL, 'RbNum='))
    result.append(getelement(blerDL, 'Mcs='))
    result.append(getelement(blerDL, bler1).strip())
    result.append(getelement(blerDL, bler2).strip())
```

> [完整 code](https://github.com/chenchih/5G_automationLinux/tree/main/log_graph/FinalCode/Layer2/multiplyUe_average)

### Case4 PDCP

- 讀 log 檔案
- 抓取時間看 TPUT

```
datestr = data.split('[', 1)[1].split(']')[0]
searchtest=re.search(r'(ingress [^(]+).+(egress [^(]+)',data)
m3New= searchtest.group(1)+", "+ searchtest.group(2)
    m3New_1=m3New.replace(", ", ":").strip().split(':')
```

- 寫進 list 和檔案
  > [完整 code](https://github.com/chenchih/5G_automationLinux/tree/main/log_graph/FinalCode/PDCP)

### 把多個檔案和再一起

- 方法一

```

directory = "/path/to/files"
# Output file name
output_file = "merged.txt"

# Loop through all files in the directory and append their contents to the output file
with open(output_file, "w") as outfile:
    for filename in os.listdir(directory):
            if filename.startswith("elog_gnb_du_layer2"):
                with open(os.path.join(directory, filename), "r") as infile:
                    outfile.write(infile.read())
```

- 方法二

```
import glob

file_pattern = 'elog_gnb_du_layer2*'
file_list = glob.glob(file_pattern)

with open('merged_file.txt', 'w') as outfile:
    for file in file_list:
        with open(file, 'r') as infile:
                outfile.write(infile.read())
```

> [完整 code](https://github.com/chenchih/5G_automationLinux/blob/main/log_graph/FinalCode/Layer2/merge_multiply_elogfile.py)

### excel

其他方法請去我 github 看不同 excel 方式

-

```
import openpyxl, string
from openpyxl.utils import get_column_letter
from openpyxl.styles import Font

def excelconvertMAC(result):
    f = open(result, 'r+')  # open text
    #########if load excel file ########################
    # excel=openpyxl.load_workbook(r'D:\\test\\test.xlsx') #open excel
    excel = openpyxl.Workbook()
    sheet = excel.worksheets
    line = f.readline();  # read text

    while line:
        list123 = line.split()  # convert
        if "=" in line:
            pass
        else:
            if list123[1] == 'Tput':
                sheet[0].append(list123)  # write into excel
            elif list123[1] == 'DL-Tput':
                #pass
                sheet[0].append(list123)  # write into excel
            elif list123[1] == 'UL-Tput':
                #pass
                sheet[0].append(list123)  # write into excel
            else:
                list123[1] = float(list123[1])
                list123[2] = float(list123[2])
                list123[3] = float(list123[3])
                list123[4] = float(list123[4])
                list123[5] = float(list123[5])
                sheet[0].append(list123)  # write into excel
                #excel cell's font
                sheet[0]['A1'] .font = Font(size = 14, bold = True)
                sheet[0]['B1'].font = Font(size = 14, bold = True)
                sheet[0]['C1'].font = Font(size = 14, bold = True)
                sheet[0]['D1'].font = Font(size = 14, bold = True)
                sheet[0]['E1'].font = Font(size = 14, bold = True)
                sheet[0]['F1'].font = Font(size = 14, bold = True)
        #adjust the column width
        column = 1
        while column < 6:
            i = get_column_letter(column)
            #print(i)
            sheet[0].column_dimensions[i].width = 25

            column += 1
        line = f.readline()  # read next line
    excel.save(excelfilename+'.xlsx')
```

- pandas

```
lists = {}
current_key = None
#with open ('test.txt', 'r')as myfile:
with open (resultfilename, 'r')as myfile:
    readline=myfile.read().splitlines()

    for line in readline:
        #print(line)
        if "=" in line:
            current_key = line.strip("=")

            lists[current_key] = []
        else:
            assert current_key is not None # there shouldn't be data before a header

            lists[current_key].append(line)
```

## 總結

以上是我再抓取檔案裡的資料想找相關字串會用到，我想信很多人會常用到此功能。可以到我 github 看完整 code。
我開發 3 個不同抓取資料，主要是要抓取資料不同，再把資料解成文字檔案，也可以轉成 excel。
github project: https://github.com/chenchih/5G_automationLinux/tree/main/log_graph

| no  | regular expression                                                        | output                                                                                                                                                                  |
| --- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | `re.findall(r"[0-9]*\.[0-9]+", string)`                                   | ['20221018.165317', '.401606', '0.000091', '9.0', '0.0', '1.4', '33.3', '1.0', '0.0', '33.3']                                                                           |
| 2   | `re.search(r'\[(\d+\.\d+\.\d+)\].*?(Tput=[^]]+), string)`                 | **group1:** 20221018.165317.401606 **group2:** Tput= 0.000091 Mbps, Mcs= 9.0(Sigma= 0.0), RbNum= 1.4, ReTxRatio= 33.3, Layers= 1.0, PdschBler= 0.0, nonWPdschBler= 33.3 |
| 3   | `re.search(r"^\[([\d\.]+).+Tput= ([\d\.]+).+Mcs= ([\d\.]+).+.", string)`  | **group1:** 20221018.165317.401606 **group2:** 0.000091 **group3:** 9.0                                                                                                 |
| 4   | `re.search(r'(ingress [^(]+).+(egress [^(]+)',string2`                    | **group1:** ingress traffic: 0.000000 **group2:** egress traffic: 0.000000                                                                                              |
| 5   | `re.search(r'(ingress traffic):\s+(\d+.\d+)',string2)`                    | ['ingress', 'traffic', '', '0.000000,', 'egress', 'traffic', '', '0.000000']                                                                                            |
| 6   | 取時間直:`re.search(r'[2]\d{7}\.\d{6}\.\d{6}',string) #'[2] start with 2` | **group0:** 20221018.165317.401606                                                                                                                                      |
| 7   | 取時間直 `re.search(r'\[([0-9.]+)\]',string)`                             | **group0:** 20221018.165317.401606                                                                                                                                      |

## reference:

- https://stackoverflow.com/questions/8569201/get-the-string-within-brackets-in-python
- https://www.rexegg.com/regex-quickstart.html
- https://python-tutorials.in/python-regular-expressions/
