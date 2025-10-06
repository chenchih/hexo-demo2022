---
title: Basic easy  useful python code
date: 2025-10-05 10:35:31
tags:
  - python
  - usefulCode
categories:
  - python 
---

This post would like to share some of the commonly use code can be easier use, you can think of cheatsheet for basic python code. This allow you to copy the code if you want to use it.
這篇筆記只想分享一些基本或常用到的程式可以用，，可以想成懶人包。


# Basic Code

## Exception capture Error on code

If you every had some experience to write code to do specfic cacultion like division of 0 and when print it will occcur Error. To not show the Error, we can use the try and exception related code. 

> **source:** [Youtube:@Cod1ngTogether](https://www.youtube.com/@Cod1ngTogether/shorts)

- Error Occur 
```
num1= 10
num2= 0
result = num1/num2
print(result) #ZeroDivisionError: division by zero
```
it will occur Error like below:
```
File "C:\new\basic_ex\try_expection.py", line 11
    except exception e:
                     ^
SyntaxError: invalid syntax
```

**Soluttion:** for this code is to add try and exception

- Try exception
```
try:
    num1= 10
    num2= 0
    result = num1/num2
    print(result) #ZeroDivisionError: division by zero
#catch ZeroDivisionError error
except ZeroDivisionError:
    print('Error: not able to divide by zero, please try again thanks!!!')

#catch every error it occur
except Exception as e:
    print(f"Error ocurred:{e}")
```

> **output:** `Error: not able to divide by zero, please try again thanks!!!`

- Real world case use function
```
def readFile(filename):

    try:
        with open(filename, "r") as file:
            content= file.read()
    except FileNotFoundError:
        print('File not found!!! Help you create one....')
        with open("missingfile.txt", "w") as file:
            content= "Hello World"
            file.write(content)
    else:
        print("File Read successfully")
        return content
    finally:
        print("Closing FIle")
if __name__ == '__main__':
    filename= input('Your filename(ex test.txt): ')
    content= readFile(filename)
    print(content)
```

>> - If the file is found will go to else and then finally to close file
>> - If not found will got to except, and finally to close file


# Relate Project

## Password Generator 
```
import random

letters="abcsefghijklmnopqrstuvwxyz"
number="12345676890"
special = "!@#$%^&*()"
chars = letters + number+special

print("Your Password: ")
passw= ""
for x in range(16):
    passw+= random.choice(chars)
print(passw)


```