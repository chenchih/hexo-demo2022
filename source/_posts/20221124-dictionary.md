---
title: Dictionary
date: 2022-11-24 14:31:31
tags: 
- python 
categories:
- python
---
今天想分享如何用dictionary字典方式存資料。
## key and Value 如何使用宣槓取直
### declare dictionary宣告dict
It\'s an unorder , it\'s not next to each other, so we can\'t use index like we use in list.  Dictionary will have a a key and value look like this:
```
dict={
    'keyA':1,
    'keyB':2
}
```

### Access and Get value取我們的直: 
取key的直: `print(dict['keyA'])` => `1`
取所有直 `print(dic)` => `{'keyA': 1, 'keyB': 2}`

### 宣告不同data type
```
dict={
    'keyA':[1,2,3], #list
    'keyB':'hello', #tuple
    'keyC': True
}
```


- 取keyA的直 
> `print(dict)` 
>> output
>> {'keyA': [1, 2, 3], 'keyB': 'hello', 'keyC': True}

- 取keyA的第2直:
> `print(dict['keyA'][1])` => `2`

- list 裡面放dict
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
| Method | Description |
| :-- | :-- |
| clear()  | Removes all items from the dictionary. |
| copy()  | Returns a shallow copy of the dictionary. |
| fromkeys(seq[, v])| Returns a new dictionary with keys from seq and value equal to v (defaults to None). |
| get(key[,d]) | Returns the value of the key. If the key does not exist, returns d (defaults to None). |
| items()  | Return a new object of the dictionary's items in (key, value) format. |
|keys()   |  Returns a new object of the dictionary's keys.|
|pop(key[,d])   | Removes the item with the key and returns its value or d if key is not found. If d is not provided and the key is not found, it raises KeyError. |
| popitem()  |Removes and returns an arbitrary item (key, value). Raises KeyError if the dictionary is empty.|
|setdefault(key[,d])   | Returns the corresponding value if the key is in the dictionary. If not, inserts the key with a value of d and returns d (defaults to None). |
|update([other])   |  Updates the dictionary with the key/value pairs from other, overwriting existing keys.|
|values()   |  Returns a new object of the dictionary's values |

### key
key need to be immutable, which mean can not change. 
```
dict={
    123:[1,2,3], #list
    True:'hello', 
    'hi': True,
    [100]: True

}
```
- `print(dict[123]) #[1,2,3]`
- `print(dict[True]) #hello`
- `print(dict['hi']) #True`

If add ` [100]:True` will occur error because it's a immutable, can't change key. list can be change, so we can't chnage it. Dictionary often use string as it's key

#### multiply key
如果有相同的key，最後一個會被取代overwrite，因此key要unquie。
As you can see below, if we declare same key, the last key will overwrite the first one, this is why when I print it the last value I show up. 
```
dict={
 "123":"hello",
 "123":"world"
}
print(dict['123']) #world
```
### get() create a dict
```
user={
 "name":"James",
 "phone":"123"
}
```

#### get key avoid error when no key exisit 
如果我們有key用原本語法會有error，我們可以用get()方法就不會跳出error。

> get a nonexist key:
>> `print(user['age'])` => `pop error`
>> `print(user.get("age"))` => `#none` 

#### create key with default value 
if user don't have key age, add a default value。建立key，給予預設直。
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

> set value 設預設value:  `user.get("age", 55)`
> get key value取key的直: `user.get("age")`

### create empty dictionary
```
user2=dict(name="test")
print(user2) #
```
> output
>> {'name': 'test'}

### keys values items
```
user={
 "name":"James",
 "phone":"123"
}

print('name' in user) # false
print('id' in user) # false
print('id' in user.keys()) # false
print('James' in user.values()) # True
print(user.items()) #dict_items([('name', 'James'), ('phone', '123')])
```
### clear() clear dictionary
```
print(user.clear()) #None
print(user)  #{}
```

### copy dictionary
```
user2=user.copy()
print(user) #{'name': 'James', 'phone': '123', 'age': 60}
print(user2) #{'name': 'James', 'phone': '123', 'age': 60}
```
### pop() 
```
print(user.pop('name'))#James
print(user) #{'phone': '123'}
```
### update()
```
print(user.update({'name': 'John'}))  
#{'name': 'John', 'phone': '123', 'age': 60}

#if key not exist still update 
print(user.update({'name11': 'MAry'}))
#{'name': 'John', 'phone': '123', 'age': 60, 'name11': 'MAry'}

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
## Build-In function
| Function | Description |
| :-- | :-- |
| all()  | Return True if all keys of the dictionary are True (or if the dictionary is empty). |
| any()  | Return True if all keys of the dictionary are True (or if the dictionary is empty).|
| len()  | Return the length (the number of items) in the dictionary.|
| sorted()  | Compares items of two dictionaries. (Not available in Python 3)|

### Example
```
# Dictionary Built-in Functions
squares = {0: 0, 1: 1, 3: 9, 5: 25, 7: 49, 9: 81}

# Output: False
print(all(squares))

# Output: True
print(any(squares))

# Output: 6
print(len(squares))

# Output: [0, 1, 3, 5, 7,
```

## Example
#### Creating Python Dictionary Example
```
# empty dictionary
my_dict = {}

# dictionary with integer keys
my_dict = {1: 'apple', 2: 'ball'}

# dictionary with mixed keys
my_dict = {'name': 'John', 1: [2, 4, 3]}

# using dict()
my_dict = dict({1:'apple', 2:'ball'})

# from sequence having each item as a pair
my_dict = dict([(1,'apple'), (2,'ball')])
```
#### Access Element from dictionary
```
# get vs [] for retrieving elements
my_dict = {'name': 'Jack', 'age': 26}

# Output: Jack
print(my_dict['name'])

# Output: 26
print(my_dict.get('age'))

# Trying to access keys which doesn't exist throws error
# Output None
print(my_dict.get('address'))

# KeyError
print(my_dict['address'])
```
### Changing and Adding Dictionary elements
```
# Changing and adding Dictionary Elements
my_dict = {'name': 'Jack', 'age': 26}

# update value
my_dict['age'] = 27

#Output: {'age': 27, 'name': 'Jack'}
print(my_dict)

# add item
my_dict['address'] = 'Downtown'

# Output: {'address': 'Downtown', 'age': 27, 'name': 'Jack'}
print(my_dict)
#{'name': 'Jack', 'age': 27}
#{'name': 'Jack', 'age': 27, 'address': 'Downtown'}
```
### Removing elements from Dictionary
```
# Removing elements from a dictionary

# create a dictionary
squares = {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# remove a particular item, returns its value
# Output: 16
print(squares.pop(4))

# Output: {1: 1, 2: 4, 3: 9, 5: 25}
print(squares)

# remove an arbitrary item, return (key,value)
# Output: (5, 25)
print(squares.popitem())

# Output: {1: 1, 2: 4, 3: 9}
print(squares)

# remove all items
squares.clear()

# Output: {}
print(squares)

# delete the dictionary itself
del squares

# Throws Error
print(squares)
```

### Python Dictionary Comprehension
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

### Dictionary Operations
```
# Membership Test for Dictionary Keys
squares = {1: 1, 3: 9, 5: 25, 7: 49, 9: 81}

# Output: True
print(1 in squares)

# Output: True
print(2 not in squares)

# membership tests for key only not value
# Output: False
print(49 in squares)
```

### Iterating Through a Dictionary
- ex1: Iterating through a Dictionary
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
#skip \n
   lines = textfile.read().splitlines()
   #print(lines)   
for i in lines:
    #sli = i.split(' ')    
    (key,val)=i.split(" ")
    d[int(key)]=val
   # print(key,"",val)
print(d)
```
