---
title: Dictionary
date: 2022-11-24 14:31:31
tags:
  - python
categories:
  - python
---

今天想分享如何用 dictionary 字典方式存資料。

## key and Value 如何使用宣槓取直

> - collection of of {key:value} pairs
> - no duplicate
> - allow changeable and ordered

### declare dictionary 宣告 dict

It\'s an unorder , it\'s not next to each other, so we can\'t use index like we use in list. Dictionary will have a a key and value look like this:

> syntax:
>
> > declare: `dictname= {key:value}`
> > get key: `print(dictname['key'])`

### Access and Get value 取我們的直:

```
dict={
    'keyA':1,
    'keyB':2
}
```

取 key 的直: `print(dict['keyA'])` => `1`
取所有直 `print(dict)` => `{'keyA': 1, 'keyB': 2}`

### 宣告不同 data type

```
dict={
    'keyA':[1,2,3], #list
    'keyB':'hello', #tuple
    'keyC': True
}
```

- 取 keyA 的直

> `print(dict)`
>
> > output
> > {'keyA': [1, 2, 3], 'keyB': 'hello', 'keyC': True}

- 取 keyA 的第 2 直:

> `print(dict['keyA'][1])` => `2`

- list 裡面放 dict

```
dict=[{
    'keyA':[1,2,3], #list
    'keyB':'hello', #tuple
    'keyC': True
},
{
    'keyA':[4,5,6], #list
    'keyB':'hello', #tuple
    'keyC': True
}]
```

> `print(dict[0]['keyA'][2])` => `2`

## Method

| Method              | Description                                                                                                                                      |
| :------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| clear()             | Removes all items from the dictionary.                                                                                                           |
| copy()              | Returns a shallow copy of the dictionary.                                                                                                        |
| fromkeys(seq[, v])  | Returns a new dictionary with keys from seq and value equal to v (defaults to None).                                                             |
| get(key[,d])        | Returns the value of the key. If the key does not exist, returns d (defaults to None).                                                           |
| items()             | Return a new object of the dictionary's items in (key, value) format.                                                                            |
| keys()              | Returns a new object of the dictionary's keys.                                                                                                   |
| pop(key[,d])        | Removes the item with the key and returns its value or d if key is not found. If d is not provided and the key is not found, it raises KeyError. |
| popitem()           | Removes and returns an arbitrary item (key, value). Raises KeyError if the dictionary is empty.                                                  |
| setdefault(key[,d]) | Returns the corresponding value if the key is in the dictionary. If not, inserts the key with a value of d and returns d (defaults to None).     |
| update([other])     | Updates the dictionary with the key/value pairs from other, overwriting existing keys.                                                           |
| values()            | Returns a new object of the dictionary's values                                                                                                  |

> Declare Dict

```
country = {
     "USA": "WDC",
    "China":"BJN",
    "Taiwan":"TP",
    "Thailand":"BKK"
}
user={
 "name":"James",
 "phone":"123",
 123:[1,2,3], #list
 True:'hello',
 'hi': True,
}
```

### key

key need to be immutable, which mean can not change.

```
print(user['phone']) #123
print(user[123]) #[1, 2, 3]
print(user[True]) # hello
print(user['hi']) #True
```

- `print(dict[123]) #[1,2,3]`
- `print(dict[True]) #hello`
- `print(dict['hi']) #True`

If add ` [100]:True` will occur error because it's a immutable, can't change key. list can be change, so we can't chnage it. Dictionary often use string as it's key

#### multiply key

如果有相同的 key，最後一個會被取代 overwrite，因此 key 要 unquie。
As you can see below, if we declare same key, the last key will overwrite the first one, this is why when I print it the last value I show up.

```
dict={
 "123":"hello",
 "123":"world"
}
print(dict['123']) #world
```

### get()

```
#get value
print(country.get("USA"))
#WDC
```

#### get key avoid error when no key exisit

如果我們有 key 用原本語法會有 error，我們可以用 get()方法就不會跳出 error。

> get a nonexist key(key 不存在)
>
> > `print(user['age'])` => `pop error` > > `print(user.get("age"))` => `#none`

#### create key with default value

if user don't have key age, add a default value。建立 key，給予預設直。

> `print(user.get("age", 55))` => `55`

But if if we have key age, then it will ignore 55。

```
user={
 "name":"James",
 "phone":"123",
 "age":60,
}
print(user.get("age", 55)) => `60`
print(user.get("age")) => `60`
```

### keys values items

```
user={
 "name":"James",
 "phone":"123"
}

print('name' in user) #false
print('id' in user) #false
print('id' in user.keys()) #false
print('James' in user.values()) #True
print(user.items()) #dict_items([('name', 'James'), ('phone', '123')])
```

### Get() 取 value 的值

```
country = {
     "USA": "WDC",
    "China":"BJN",
    "Taiwan":"TP",
    "Thailand":"BKK"
}

```

- get the value
  > `print(country.get("USA"))`
  >
  > > `output:`
  > > WDC

### Update 新增與修改

- 新增 item key and Value，add new item key and value

  > `country.update({"Japan":"TKY"})` > `print(country)`
  >
  > > `output:`
  > > {'USA': 'WDC', 'China': 'BJN', 'Taiwan': 'TP', 'Thailand': 'BKK', 'Japan': 'TYY'}

- 修改 Value，update exist value change exists key
  > `country.update({"Japan":"TTT"})` > `print(country) `
  >
  > > `output:`
  > > {'USA': 'WDC', 'China': 'BJN', 'Taiwan': 'TP', 'Thailand': 'BKK', 'Japan': 'TTT'}

### pop and popitem 移除 item

- pop 移除

  > `country.pop("Taiwan")` > `print(country)`
  >
  > > `output:`
  > > {'USA': 'WDC', 'China': 'BJN', 'Thailand': 'BKK', 'Japan': 'TTT'}

- popitem:移除最後一組
  pop item will remove the latest item
  > `country.popitem()` > `print(country)`
  >
  > > `output:`
  > > {'USA': 'WDC', 'China': 'BJN', 'Thailand': 'BKK'}

### clear 清除 empty or clear

> `country.clear()` > `print(country)`
>
> > `output`
> > {}

### keys and values (get value or key)

```
country = {
     "USA": "WDC",
    "China":"BJN",
    "Taiwan":"TP",
    "Thailand":"BKK"
}

```

- keys

```
#get the keys
keys= country.keys()
print(keys)
#dict_keys(['USA', 'China', 'Taiwan', 'Thailand'])
```

- values

```
#get the value
values= country.values()
print(values)
# dict_values(['WDC', 'BJN', 'TP', 'BKK'])
```

### copy dictionary

```
countrybk=country.copy()
print(countrybk)
print(country)
#{'USA': 'WDC', 'China': 'BJN', 'Taiwan': 'TP', 'Thailand': 'BKK'}
#{'USA': 'WDC', 'China': 'BJN', 'Taiwan': 'TP', 'Thailand': 'BKK'}

user2=user.copy()
print(user) #{'name': 'James', 'phone': '123', 'age': 60}
print(user2) #{'name': 'James', 'phone': '123', 'age': 60}
```

### Method Example

```
# Dictionary Methods
marks = {}.fromkeys(['Math', 'English', 'Science'], 0)
print(marks)
# Output: {'English': 0, 'Math': 0, 'Science': 0}

for item in marks.items():
    print(item)

# Output: ['English', 'Math', 'Science']
print(list(sorted(marks.keys())))
```

## iterate key and value

### keys

```
for key in country.keys():
    print(key)
#USA
#China
#Taiwan
#Thailand
```

### value

```
for value in country.values():
    print(value)
#WDC
#BJN
#TP
#BKK
```

### items() keys and values

```
for key, value in country.items():
    print(f"{key}:{value}")
#USA:WDC
#China:BJN
#Taiwan:TP
#Thailand:BKK
```

## Dictionary Comprehension

> - dictionary = {key: expression for (key,value) in iterable}
> - dictionary = {key: expression for (key,value) in iterable if conditional}
> - dictionary = {key: (if/else) for (key,value) in iterable}
> - dictionary = {key: function(value) for (key,value) in iterable}

### using for condition

> Syntax:
>
> > `dictionry={key:expression for (key, value) in iterate}`

```
citiesinF={"Beijing": 20, "Boston":10, "New York":30, "Califorina": 35}
citiesinC= {key:round((value-32)*(5/9)) for (key,value) in citiesinF.items()}
print(citiesinC)
```

> `output:`
>
> > {'Beijing': -7, 'Boston': -12, 'New York': -1, 'Califorina': 2}

### using if condition

> Syntax:
>
> > `dictionry={key:expression for (key, value) in iterate if conditional}`

```
weather={"Beijing": "snowing", "Boston":"cloudy", "New York":"sunny"}
sunnyweather={key: value for (key,value) in weather.items() if value =="sunny"}
print(sunnyweather)
```

> `output:`
>
> > {'New York': 'sunny'}

### using if else condition

> Syntax:
>
> > `dictionry={key:if/else for (key, value) in iterate}`

```
citiestemp={"Beijing": 20, "Boston":10, "New York":30, "Califorina": 35}
desccities={key: ("warm"if value >= 20 else "cold") for (key,value) in citiestemp.items()}
print(desccities)
```

> `output:`
>
> > {'Beijing': 'warm', 'Boston': 'cold', 'New York': 'warm', 'Califorina': 'warm'}

### using function

> Syntax:
>
> > `dictionry={key:function(value)) for (key, value) in iterate}`

```
def checktemp(value):
    if value >= 25:
        return "cool"
    elif 69 >= value >=40:
        return "warm"
    else:
        return "cold"

citiestemp={"Beijing": 20, "Boston":10, "New York":30, "Califorina": 35}
desccities={key: checktemp(value) for (key,value) in citiestemp.items()}
print(desccities)
```

> `output:`
>
> > {'Beijing': 'cold', 'Boston': 'cold', 'New York': 'cool', 'Califorina': 'cool'}

### Example

```
# Dictionary Comprehension
squares = {x: x*x for x in range(6)}

print(squares)
#{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

squares = {}
for x in range(6):
    squares[x] = x*x
print(squares)
#{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}
```

## Build-In function

| Function | Description                                                                         |
| :------- | :---------------------------------------------------------------------------------- |
| all()    | Return True if all keys of the dictionary are True (or if the dictionary is empty). |
| any()    | Return True if all keys of the dictionary are True (or if the dictionary is empty). |
| len()    | Return the length (the number of items) in the dictionary.                          |
| sorted() | Compares items of two dictionaries. (Not available in Python 3)                     |

### Build-In Example

```
# Dictionary Built-in Functions
squares = {0: 0, 1: 1, 3: 9, 5: 25, 7: 49, 9: 81}

# Output: False
print(all(squares))

# Output: True
print(any(squares))

# Output: 6
print(len(squares))

# Output: [0, 1, 3, 5, 7]

```

## ALL Examples

### Creating Python Dictionary Example

```
# empty dictionary
my_dict = {}

# dictionary with integer keys
my_dict = {1: 'apple', 2: 'ball'} #{1: 'apple', 2: 'ball'}

# dictionary with mixed keys
my_dict = {'name': 'John', 1: [2, 4, 3], 'age': 26} #{1: 'apple', 2: 'ball'}

print(my_dict['name']) #John
print(my_dict.get('age')) #26
```

### Changing and Adding Dictionary elements

```
# Changing and adding Dictionary Elements
my_dict = {'name': 'Jack', 'age': 26}
#{'name': 'Jack', 'age': 26}

# update value
my_dict['age'] = 27
#{'name': 'Jack', 'age': 27}

# add item
my_dict['address'] = 'Downtown'
#{'name': 'Jack', 'age': 27, 'address': 'Downtown'}
```

### Removing elements from Dictionary

```
# create a dictionary
squares = {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# remove a particular item, returns its value
print(squares.pop(4)) #16
print(squares) #{1: 1, 2: 4, 3: 9, 5: 25}

# remove an arbitrary item, return (key,value)
print(squares.popitem()) # (5, 25)
print(squares)#{1: 1, 2: 4, 3: 9}

# remove all items
squares.clear()
print(squares) #{}

# delete the dictionary itself
del squares

# Throws Error
print(squares)
```

### Dictionary Operations

```
# Membership Test for Dictionary Keys
squares = {1: 1, 3: 9, 5: 25, 7: 49, 9: 81}
print(1 in squares) #True
print(2 not in squares) #True

# membership tests for key only not value
print(49 in squares) #False
```

### Iterating Through a Dictionary

- Iterating through a Dictionary

```
# Iterating through a Dictionary
squares = {1: 1, 3: 9, 5: 25, 7: 49, 9: 81}
for i in squares:
    print(squares[i], end=" ")
# 1 9 25 49 81
```

- Iterating all keys and values

```
account = {'eric': 17, 'ben':30}
for name, age in account.items():
    print("Hi " + name+ "your age: "+str(age))
# Hi ericyour age: 17
# Hi benyour age: 30
```

- Iterating all keys

```
account = {'eric': 17, 'ben':30}
for name in account.keys():
    print("hi " + name)
# hi eric
# hi ben
```

- Iterating all values

```
account = {'eric': 17, 'ben':30}
for age in account.values():
    print("age " + str(age))
# age 17
# age 30
```

### [Amazon test] read file from text file

- Question: Read file into datastucture and search like logfile
  If we have a log.txt, as below, you need to and search specfic string, like cat.
- log.txt

```
1 cat
2 lion
3 apple
```

- Answer2: using dictionary

```
d={}
with open("log.txt", "r") as textfile:
   #lines = textfile.readlines()
   lines = textfile.read().splitlines()
   #print(lines)
for i in lines:
    #sli = i.split(' ')
    (key,val)=i.split(" ")
    d[int(key)]=val
   # print(key,"",val)
print(d)
```
