---
title: Excel_ReadWrite
date: 2022-10-23 11:58:07
tags: python fileIO excel
categories:
- python
---

## Create empty Excel File
```
import openpyxl
fn = 'new_excel.xlsx'
wb = openpyxl.Workbook()
wb.save(fn)
```
## Create Sheet工作表的
### Create Empty Sheet 新增工作
```
import openpyxl
fn = 'new_excel.xlsx'
wb = openpyxl.Workbook()
wb.create_sheet("Sheet1", 0) 
wb.create_sheet("Sheet2", 1)
wb.save(fn)
```
### Read Excel Sheet 讀取excel檔案每個工作表的名稱 
```
import openpyxl
fn = 'new_excel.xlsx'
wb = openpyxl.load_workbook(fn)
print(wb.sheetnames)
print(wb.active)
print(wb.active.title)
```

output: 
```
['Sheet1', 'Sheet2', 'Sheet']
<Worksheet "Sheet1">
Sheet1
```

### edit Name of worksheet 修改工作表名稱
```
import openpyxl
workbook = openpyxl.load_workbook("new_excel.xlsx")
sheet = workbook['Sheet1'] #orginal sheet name原本工作表名稱
sheet.title = 'Sheet100' #修改工作表名稱
workbook.save("new_excel_new.xlsx") #save new Excel file 
print(workbook.sheetnames)
```
output:
```
['Sheet100', 'Sheet2', 'Sheet']
```
### 修改工作表顏色
```
import openpyxl
workbook = openpyxl.load_workbook("new_excel_new.xlsx")
sheet = workbook.active
sheet.sheet_properties.tabColor = "1072BA"
workbook.save("sampleNEW.xlsx")
print(workbook.sheetnames)
```

### 隱藏/取消隱藏工作表

```
import openpyxl
workbook = openpyxl.load_workbook("new_excel_new.xlsx")
sheet = workbook['Sheet100']
sheet.sheet_state = 'hidden' #hidden sheet
#sheet.sheet_state = 'visible' #visible sheet
workbook.save("sample.xlsx")
```

### copy sheet 複製工作表
```
import openpyxl
workbook = openpyxl.load_workbook("sample.xlsx")
sheet = workbook['Sheet100'] #orginal sheet 
target = workbook.copy_worksheet(sheet)
target.title = 'new' #clone new sheet name 新的工作表名稱
workbook.save("sample.xlsx")
```

### 刪除工作表
```
import openpyxl
workbook = openpyxl.load_workbook("sample.xlsx")
print(workbook.sheetnames)
#['Sheet100', 'Sheet2', 'Sheet', 'new']
sheet = workbook['Sheet100']
workbook.remove(sheet)
workbook.save("sample.xlsx")
print(workbook.sheetnames)
#['Sheet2', 'Sheet', 'new']
```
## 讀工作表
```
import openpyxl
fn = 'new_excel.xlsx'
wb = openpyxl.load_workbook(fn)
wb.active = 0
ws = wb.active
print('excel活動工作表： ', ws)
for row in ws:
    for cell in row:
        print(cell.value)
print()
print('D1內容： ', ws['D1'].value)
```
### 寫入儲存格
```
import openpyxl

fn = 'new_excel.xlsx'
wb = openpyxl.load_workbook(fn)

wb.active = 0
ws = wb.active

print('B2內容： ', ws['B2'].value)

ws['B2'].value =  20
print('B2內容： ', ws['B2'].value)

ws.cell(column=2, row=3).value = 999
wb.save(fn) 
```
### 讀取指定區域內容
```
import openpyxl
from openpyxl.utils import get_column_letter, column_index_from_string

fn = 'sample.xlsx'
wb = openpyxl.load_workbook(fn, data_only=False) # 要excel開啟才可以看到值，否則會顯示None

wb.active = 0
ws = wb.active

for row in ws['A2':'D5']:
    for cell in row:
        print(cell.value, end=' ')
    print()
```

### 新增/刪除 欄、列
```
import openpyxl
from openpyxl.styles import Font

fn = 'sample.xlsx'
wb = openpyxl.load_workbook(fn)
ws = wb.active

ws.insert_rows(1)
ws.insert_cols(1, 2)
#ws.delete_rows(1, 2)
#ws.delete_cols(1, 2)

wb.save(fn)
```


### 設定日期格式
```
import openpyxl
import datetime

workbook = openpyxl.load_workbook("new_excel.xlsx")

sheet = workbook['Sheet1']
sheet['A1'] = datetime.datetime(2010, 7, 21)

# sheet['A1'].number_format = 'yyyy-mm-dd h:mm:ss'
# sheet['A1'].number_format = 'yyyy-mm-dd'
sheet['A1'].number_format = 'dd-mm-yyyy'

for row in sheet['A1':'D5']:
    for cell in row:
        print(cell.value, end=' ')
    print()

workbook.save("sample.xlsx")
```

## reference:
- https://hackmd.io/@amostsai/SJkC1_EcX?type=view#python%E8%AE%80%E5%8F%96%E4%BF%AE%E6%94%B9excel