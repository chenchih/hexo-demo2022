---
title: IO_ReadWriteFile_python
date: 2022-08-21 15:45:05
tags: python 
categories:
- python
---

## Open Read Write File
> open syntax:　
>> `open( file, mode, encoding="utf-8")`

|mode 字串	| 說明 |
| :-- | :-- |
|r	|Read only `讀取模式` ( 預設 )|
|r+	|Read and write|
|w	|Write only 寫入模式，`檔案若存在，會清空內容再寫入`； 若檔案不存在，則建立新檔開啟寫入|
|w+	|write+read|
|a　|Append only 附加模式，若`檔案存在，則寫入內容`會附加至檔 案尾端|
|a+ |Append and Read (‘a+’) |
### Read 

|讀取方法	| 描述 |
| :-- | :-- |
|read( )	| 一次讀取檔案所有的內容，回傳為字串|
|readline( ) |	只讀取一行內容|
|readlines( ) |	將所有檔案內容，每行讀入回傳為串列|

```
fileObj = open("路徑檔名" , "r", encoding="utf-8") 
content = fileObj.read( ) 
fileObj.close( )
```

### Write

```
fileObj = open("路徑檔名" , "w", encoding="utf-8")
fileObj.write(輸出資料)
fileObj.close( ) 
```

## Example

### Ex1. read file and print 

> Note: Avoid reading with new line
> `line = line.strip()`
or 
> `print(line,end='')`

```
with open('test.txt') as f,open('out.txt', 'w') as f_out:
    for line in f:
        line = line.strip()
        print(line)

```

### Ex2: Read a file from text file and write to another file

```
with open('test.txt') as f,open('out.txt', 'w') as f_out:
    for line in f:
        line = line.strip()
        #print(line)
        f_out.write('{}\n'.format(line))

```


### ex3 write file
```
with open ('video_title_url.txt', 'w', encoding='UTF-8') as f_out:
    for line_index in downloadlink:
        line = line_index.strip()
        f_out.write('{}\n'.format(line))   
    print("end")

```