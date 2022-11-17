---
title: Python Print
date: 2022-07-30 08:05:22
tags: python
categories:
- python
---
## 1. Print

### Ex1 Print Basic Interger and String 
```
str_name= "hello"
num_value= 999
print(f"str value is {str_name}, and number is {num_value}")
```
> **output:**
>> `str value is hello, and number is 999`

## %-formatting-OLD

### Example 1 Print String with `%` Operator
```
text = 'world'
print("hello " + text)
print('hello %s' % text)

name = "Test"
num = 100
print("Hello, %s. My num is  %s." % (name, num))
```
> **output:**
>> `hello world`
>> `hello world`
>> `Hello, Test. You are 100.`



## 3. str.format()- NEW
str.format() 是對 %-formatting 的改進，可以用函式呼叫語法，可以通過 format() 方法對被轉換為字串的物件

### ex1: Print Basic String 
```
text = 'world'
year = 2022
print('hello {} {}'.format(text, year))
# hello world 2022
```
### ex2 print dict字典 with `**`
```
person = {'name': 'Eric', 'age': 74}
print ("Hello, {name}. You are {age}.".format(name=person['name'], age=person['age']))
print ("Hello, {name}. You are {age}.".format(**person))
```
> **output**
>> `Hello, Eric. You are 74.`

### ex3: print X decimal places
```
float = 2.154327
format_float = "{:.2f}".format(float)
print(format_float)
```
> **output:**
>> 2.15
### ex4: print decimal format

```
number = 1.345
f = '{0:.2g}'.format(number)
print(f)
f = '{0:.3g}'.format(number)
print(f)
f = '{0:.4g}'.format(number)
print(f)
```
> **output:**
>> 1.3
>> 1.34
>> 1.345


### Ex5: 轉16進位

> `print('{:x}'.format(23))`
> **output:**
>> 17


## 4 printf - New
### Ex1 Print Basic String
```
text = 'world'
num = 9000
print(f'Hello , {text}')
print( f"{5 * 5 }")
```
> **output:**
>> Hello world
>> 25

### Ex2 Print Basic Integer
```
x = 10
y = 27
print(f'x + y = {x + y}')
# 37
```
### Ex3 Print X decimal places
-  print 2 decimal places
```
now_value=123.456
print(f'{now_value:.2f}')
```
> **output:**
>> 123.46

- Comma between number, and print 2 decimal places
```
number=1000000
print(f'The number, 1000000, format with a comma {number:,.2f}')
```
> **output:**
>> The number, 1000000, format with a comma 1,000,000.00

### Ex4 Date and Time
```
from datetime import datetime
now = datetime.utcnow()
print(f"{now}") # 2022-07-30 09:21:30.500456
print(f"{now=:%y-%m-%d}") # now=22-07-30

```
## 5 other print function
### Ex1: round number:
```
number = 1.345
print(round(number))
# 1
```

### Ex2: tab 
> `print(('===\t=========== \t =========== \t =========== \n').expandtabs(8))`
>> **output:**
>> `===     ===========      ===========     ===========`

### Ex3: lower String
```
name = "Ja Laaaa"
print (f"{name.lower()} is funny.")
```
> **output:**
>>　`ja laaaa is funny.`

## 6 Print List
There are couple of ways to print list

> `test = ['A' , 'B', 'C' , 'D']`

- Method 1: using for loop
```
for i in test:
    print(i,end=' ') 
print()
# A B C D
```
- Method 2: *listname unpack list
We can use without for loop to unpack list
>  print(*test) # A B C D

Print new line: 
> print(*test, sep='\n')

- reference: 
https://python.plainenglish.io/3-ways-to-print-list-elements-on-separate-lines-in-python-815454bb2cd4