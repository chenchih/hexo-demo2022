---
title: count_string_occurrences 文字出現的次數
date: 2024-11-28 14:18:55
tags:
  - python
  - string
categories:
  - [python, example]
---

This exercise is to show you how to count your string occurrences, or how many duplicated value. 我想分享如何找估重複文字次數。

## iterate through list, and store in dictionary

### [方法一] 基本 loop 把它存在 dictionary

> **output**: `{'James': 1, 'Kelly': 2, 'Sammie': 1`

```
listofName=['James','Kelly', 'Sammie', 'Kelly']
dictcollect={}
for name in listofName:
    if name in dictcollect:
        dictcollect[name]+=1

    else:
        dictcollect[name]=1
print(dictcollect)

```

其實可以寫成更簡短方式，其實跟上面方式一樣

```
listofName=['James','Kelly', 'Sammie', 'Kelly']
dictcollect={}
for name in listofName:
    dictcollect[name]=dictcollect.get(name,0)+1
print(dictcollect)
```

如果沒出現就離開，出現就會+1，也可以這樣做 `1+dictcollect.get(name,0)`。

`dictcollect.get(name, 0)` checks if the name already exists as a key in the dictionary.
If it exists, the current count is retrieved.
If it doesn't exist, 0 is returned.

### [方法二] collection 裡面的 count

也可以利用 collection 方式來算，要先匯入 nodule `from collection import count`

```
from collections import Counter
listofName=['James','Kelly', 'Sammie', 'Kelly']
namecounting=Counter(listofName) #collections.Counter
print(namecounting)
#Counter({'Kelly': 2, 'James': 1, 'Sammie': 1})
```

> **output**: `Counter({'Kelly': 2, 'James': 1, 'Sammie': 1})`

如果想轉成 dict:

```
#convert to dict
print(dict(namecounting))
#{'James': 1, 'Kelly': 2, 'Sammie': 1}

#conver to list
print(list(namecounting))
#['James', 'Kelly', 'Sammie']
```

> **output**: `{'James': 1, 'Kelly': 2, 'Sammie': 1}`
