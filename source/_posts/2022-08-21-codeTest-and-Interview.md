---
title: codeTest_and_Interview
date: 2022-08-21 15:44:18
tags: python codetest interview
categories:
- python
---

## Interview Code Test
I am sharing some Code Test during my Interview, and also some practice Code example. 
今天分享我一些Live Coding 面試問題，還有一些刷題的問題。


## Amazon Live Code 
### Q1. read file into datastucture and search like logfile
If we have a log.txt, as below, you need to and search specfic string, like cat.

- log.txt
```
1 cat
2 lion
3 apple
```

#### Answer 1: list 
```
with open("log.txt", "r") as textfile:
   lines = textfile.readlines()
for i in lines:
    sli = i.split(' ')
    #print(sli)
    if "cat" in sli:
        print(sli[0], sli[-1])

```

#### Answer2: using dictionary 
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


## HackCode
### Q1. Alphabelt_filter
```
class LetterFilter:

    def __init__(self, s):
        self.s = s      

# Enter your code here. 
# Complete the classes below.
# Reading the inputs and writing the outputs are already done for you.
#
# class LetterFilter:
#
```
#### Method 1: solution for HackCode
```
def eliminate_consonants(x):
        vowels= ['a','e','i','o','u']
        for char in x:
            if char not in vowels:
                print(char, end = "")
eliminate_consonants('mississippi')
```

#### Method 2: solution for HackCode
```
class LetterFilter:

    def __init__(self, s):
        self.s = s      

# Enter your code here. 
# Complete the classes below.
# Reading the inputs and writing the outputs are already done for you.
#
# class LetterFilter:
#
    #def __init__(self, s):
       #self.s = s
	
    def filter_vowels(self):                
        # Enter your code here
        # Return a string       
        vowel = "aeiou"
        count = 0
        arr = []
        for y in self.s:
            if y in vowel:
                arr.append(y)
                count += 1
        result = self.convertListStr(arr)
        return result
            
    def filter_consonants(self):
        # Enter your code here
        # Return a string
        consonants = "bcdfghjklmnpqrstvwxyz"
        count = 0
				arr = []
        #print(self.s)
        for y in self.s:
            if y in consonants:
                arr.append(y)
                count += 1
        result = self.convertListStr(arr)
        return result
    def convertListStr(self,text):        
        str= ""
        result = str.join(text)
        return result
s = input("please enter string: ")
f = LetterFilter(s)
print(f.filter_vowels())
print(f.filter_consonants())
```

### Q2. Mutations
Input: 
STDIN           Function
-----           --------
abracadabra     s = 'abracadabra'
5 k             position = 5, character = 'k'

#### Solution
```
def mutate_string(string, position, character):
    list1= []
    list1[:0]=string
    list1[position] = character  
    return "".join(list1)
if __name__ == '__main__':
    s = input()
    i, c = input().split()
    s_new = mutate_string(s, int(i), c)
    print(s_new)
```

### Q3. fizz_buzz
#### Solution
```
def fizzBuzz(n): 
    # Write your code here
    for num in range(1, n+1):
        if num % 3 == 0 and num % 5 == 0:
            print("FizzBuzz")
        elif num % 3 is 0:
            print("Fizz")
        elif num % 5 is 0:
            print("Buzz")
        else:
            print(num)  
if __name__ == '__main__':
    n = int(input().strip())
    fizzBuzz(n)
```

### JS 
#### Q1.

## LeedCode
