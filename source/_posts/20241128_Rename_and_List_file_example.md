---
title: Rename_and_List_file_example 列出檔案目錄和如重新立名
date: 2024-11-28 15:16:40
tags:
  - python
  - file
categories:
  - [python, example]
---

今天我想分享關於目錄和檔案相關範例，如重新立名，出檔案，我會用很多方式呈現出來。

## List current directory 目錄利出檔案

### list your file in current directory 目錄列出檔案

我們常在 linux 和 window 都會用 ‵ls‵ 或　‵dir‵ 來列出我們目錄底下所有檔案。 可以用 `os.listdir()` 就可以利出所有目錄和檔案

> 目前目錄下: `os.listdir()`
>
> 指定位置: `os.listdir(path)`

```
import os
for file in os.listdir():
    print(file)
```

> output:

```
counter.py
elogfile
elogfile.txt
elogfile2
elogfile2.txt
list_file.py
logchecking.py
logchecking_rename.py
```

### filter specific file or file type 篩選檔名

有幾個方式可以用，如果要指定檔案類型 我們可以用: `startswith()` 或 `endswith()`.

You can filter file name or file extension with os module, however it have some limitation. You can use with the two option, which allow you to filter file start with specific file name or end with specific name which refer to the file extension.

```
import os
patternfixed=".txt"
patternfixed_start="elogfile"

matching_files = [file for file in os.listdir() if file.endswith(patternfixed)]
# ['elogfile.txt', 'elogfile2.txt']

matching_files = [file for file in os.listdir() if file.startswith(patternfixed_start)]

# ['elogfile', 'elogfile.txt', 'elogfile2', 'elogfile2.txt']
```

但這只能塞選出開頭或結尾檔名，更老的方式是用`fnmatch` 可以加一些 pattern 例如　`*XXX`，以下面範例我用 `elog*` 或 `*.txt` 會篩選出來檔名開頭是`elog`，file type 是`.txt `

From below example I use the `fnmatch` module which allow me to use the pattern to filter specific file name or file type. So I add am `* asterisk` which is more flexible to filter file start with `elog` or file extension as `.txt` file.

```
import os, fnmatch

pattern = "elog*" or "*.txt"
matching_files = [file for file in os.listdir() if fnmatch.fnmatch(file, pattern)]

# result in list
print(matching_files)
# ['elogfile', 'elogfile.txt', 'elogfile2', 'elogfile2.txt']

#iterate through list
for file in matching_files:
    print(file)
```

**Summary of listfile**

|       Method        | Supports Wildcards |      Flexibility Example       |                        Use Case                         |
| :-----------------: | :----------------: | :----------------------------: | :-----------------------------------------------------: |
|    `endswith()`     |     No Matches     | files by their exact extension |                  Get all `.txt` files                   |
|   `startswith()`    |     No Matches     |  files by their exact prefix   |            Get files starting with `log\* `             |
| `fnmatch.fnmatch()` |    Yes Matches     |        complex patterns        | Get files with names like `log\**.txt‵ or ‵*data\*.csv` |

## count matching file

I provide serveral method to achieve it, see which one you perfer. Overall my best otpion is using glob module.

我有用很多不同方式，可以選哪一個妳喜號。

### [方法一] os.listdir 跟 len

這個方法我在上面篩選有用過一樣的程式，只是我要算出有找到幾個檔案。

Easy to understand. Directly counts files matching the pattern.
Less efficient for large directories with many files

```
import os
file_pattern_file_startwith = "elog"
filelen = len([file for file in os.listdir() if file.startswith(file_pattern)])
matching_files= [file for file in os.listdir() if file.startswith(file_pattern)]

print(f'contain {filelen} file, filename: {matching_files}')
#contain 2 file, filename: ['elogfile', 'elogfile2']
contain 2 file, filename: ['elogfile', 'elogfile2']
```

會發現有用兩個方式，一個用簡端方式，另一個是用傳通的方式，這個個其實是一樣的，只是有血人不習慣用簡端方式九可以參考一般的方式。

You will have notice I had provided two function which both functionality are the same, one is shorter code using comprehension method, and the other one uses traditional method. In case if you're not used of using the shorter code, you can reference the traditional way.

```
file_pattern_file_startwith = "elog"
matching_files=[]
filelen = 0
for file in os.listdir():  #Loop through each file in the directory
    if file.startswith(file_pattern_file_startwith): #Check if the file matches the pattern
        matching_files.append(file)
        filelen += 1
print(f'contain {filelen} file, filename: {matching_files}')
```

可以改成函數 code 比較彈性和乾淨 change the above code into function for more flexibility and cleaner and more readability.

**make it into function**

```
def check_file_count_listcomprehension (file_pattern):
    filename = [file for file in os.listdir() if file.startswith(file_pattern)]
    filecount = len(filename)
    return filename,filecount

file_pattern_file_startwith = "elog"
matching_files,filelen=check_file_count_listcomprehension(file_pattern_file_startwith)
print(f'contain {filelen} file, filename: {matching_files}')

```

### [方法二] sum 方式

Memory-efficient, Faster for large directories as it doesn't require storing unnecessary data.

```
import os

file_pattern_file_startwith = "elog"

matching_files = [file for file in os.listdir() if file.startswith(file_pattern_file_startwith)]

filelen=sum(1 for file in os.listdir() if file.startswith(file_pattern_file_startwith))

print(f'contain {filelen} file, filename: {matching_files}')
#contain 2 file, filename: ['elogfile', 'elogfile2']
```

> output: `contain 2 file, filename: ['elogfile', 'elogfile2']`

**make it into function**

```
def check_file_count_withsum(file_pattern):
    filelen = sum(1 for file in os.listdir() if file.startswith(file_pattern))  # Count matching files
    filenames = [file for file in os.listdir() if file.startswith(file_pattern)]  # List matching files
    return filelen, filenames  # Return both count and filenames
file_pattern_file_startwith = "elog"

# Call the function and get results
filelen, matching_files = check_file_count_withsum(file_pattern_file_startwith)

# Print results
print(f'Contain {filelen} file(s), filename(s): {matching_files}')
```

### [方法三] glob 方式

Supports advanced wildcard patterns `(*, ?, etc.)`, making it more versatile.
Convenient for matching complex patterns.
Less efficient for large directories with many files

```
import os, glob
file_pattern = "elog*"

# Get the list of matching files (debug used)
matching_files = glob.glob(file_pattern)
filelen=len(matching_files)
print(f'contain {filelen} file, filename: {matching_files}')
#contain 2 file, filename: ['elogfile', 'elogfile2']
```

> output: `contain 2 file, filename: ['elogfile', 'elogfile2']`

**make it into function**

```
def check_file_count(file_pattern):
    filename=glob.glob(file_pattern)
    return filename, len(filename)

file_pattern = "elog*"

matching_files,filelen=check_file_count(file_pattern)
print(f'contain {filelen} file, filename: {matching_files}')
#contain 2 file, filename: ['elogfile', 'elogfile2']
```

## Rename File

在這邊我們來修改檔名，我會用單一案跟多個檔案。
In this part I wants to show you how to rename with one file and multiple file. Let use any of the method from above to get the file you want.

### single file rename

```
import os, glob
file_pattern = "elogfile"
matching_files = glob.glob(file_pattern)
filelen=len(matching_files)
```

As you can see the result of the file it matches will return as list datatype, you can try with this `print(type(matching_files))#<class 'list'>`
如果要修改檔名妳資料類別一定要是 str，篩選結果不會是 str，需要轉成 str，才能改名稱。我們可以用 `print(type(matching_files))#<class 'list'>` 他會顯示他的資料類別是 list。下面有介紹一些方法如何轉成 str 也可以順利修改檔名。

You need to change it into str to be able to convert. You can either use the index or join method like

> get the first name: `print(matching_files[0])`
>
> convert list to string:　‵filename="".join(matching_files)‵

Let rename the file using the below code, syntax: `rename(original_file_name, new_file_name)`. In the below example you can see my original file name called `elogfile`, and change to `newelogfile` name.

```
import os, glob, fnmatch

#search filename elogfile

org_filename = "elogfile"
logfilename="newelogfile"

#check file
matching_files = glob.glob(org_filename)

#count exist file
filelen=len(matching_files)
print(f'contain {filelen} file, filename: {matching_files}')
#print(f'Found only  {filelen} file: {matching_files[0]}')

#rename filename
try:
    os.rename(matching_files[0], logfilename)
    print(f'Renamed {matching_files[0]} to {logfilename}')
except Exception as e:
    print(f"Error renaming file: {e}")

#list current directory filename that contain *logfile*
print('='*70)
checkfilepattern = "*logfile*"
listfiles= [file for file in os.listdir() if fnmatch.fnmatch(file, checkfilepattern)]
print(f"List current filename: {listfiles}")
```

As you can see the filename is been changed, I show the current directory filename with filter file contain `logfile` which you can see only the `elogfile` is been change the `elogfile2` still the same. This is a basic of rename with SINGLE FILE.

> **Output:**

```
contain 1 file, filename: ['elogfile']
Renamed elogfile to newelogfile
======================================================================
List current filename: ['elogfile2', 'newelogfile']
PS C:\Users\test\Desktop\elog_parser\Layer2\singleUe\debug_log_check>
```

### Rename with Multiple File

Now let me show how to change to multiple filename, using the same example from previous, with filename `elogfile` and `elogfile2` and change to newelogfile.

```
import os, glob, fnmatch
#search filename elogfile

org_filename = "elogfile*"
logfilename="newelogfile"

#check file
matching_files = glob.glob(org_filename)

#count exist file
filelen=len(matching_files)
print(f'contain {filelen} file, filename: {matching_files}')
#contain 2 file, filename: ['elogfile', 'elogfile2']

#rename filename
for i, file in enumerate(matching_files):
    try:
        new_name = f"{logfilename}_{i}"  # Generate a unique name for each file
        os.rename(file, new_name)  # Rename each file
        print(f"Renamed {file} to {new_name}")
    except Exception as e:
         print(f"Error renaming file {file}: {e}")
print('='*70)
checkfilepattern = "newelogfile*"
listfiles= [file for file in os.listdir() if fnmatch.fnmatch(file, checkfilepattern)]
print(f"List current filename: {listfiles}")
```

> **Output:**

```
contain 2 file, filename: ['elogfile', 'elogfile2']
Renamed elogfile to newelogfile_0
Renamed elogfile2 to newelogfile_1
======================================================================
List current filename: ['newelogfile_0', 'newelogfile_1']

```
