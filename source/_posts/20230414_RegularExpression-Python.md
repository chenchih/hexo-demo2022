---
title: RegularExpression-Python
date: 2023-04-14 16:35:18
tags:
  - python
  - regExp
categories:
  - python
---

今天有想在這裡分享 Regular Expression，這也是大家不想碰到的，可就是一個很復雜的就越耗用。
我也沒有很勵害，但之前開發自動化，用很多。因此想藉由這編文章來寫下我所寫道的筆記和參考很多教學。

在介紹之前我們在 python 都會用到 re 或是 rex ，但在這我只會分享用 re，也就是要 `import re`，不然不能用。

## 常用的 req module

| Module   | 說明                                                                       |
| :------- | :------------------------------------------------------------------------- |
| match    | Determine if the RE matches at the beginning of the string.                |
| search   | Scan through a string, looking for any location where this RE matches      |
| findall  | Find all substrings where the RE matches, and returns them as a list.      |
| finditer | Find all substrings where the RE matches, and returns them as an iterator. |

### compile()
```
import re
text ='https://chenchih.page , Author is ChenChih'
pattern=re.compile('Chenchih',re.I)
print(pattern.match(text)) #None
print(pattern.search(text).group()) #chenchih
print(pattern.findall(text)) #['chenchih', 'ChenChih']
```
> output:
> > None
>>  `cheenchih`
>>  `['chenchih', 'ChenChih']`



### match()

> This function matches a regular expression pattern at the beginning of a string. If the pattern is found, it returns a match object, otherwise, it returns None.

```
import re
teststring="123abc456789abc123ABC"
pattern=re.compile(r"abc")
match=pattern.match(teststring)
print(match)
```

> `output:`
>
> > None or empty
> > `[Note]: ` Match only match at the beginning, because abc is not in the beginning, so will return none.

#### Match Example 
```
import re
text = "apple banana cherry"
pattern = r"apple"
match_obj = re.match(pattern, text)
if match_obj:
    print("Match found!")
else:
    print("Match not found!")
print(match_obj.group())

```
> `output：`
>
> > Match found!
> > apple

`[Note]` In this example, `re.match()` searches for the pattern "apple" at the beginning of the string "apple banana cherry". Since the pattern is found at the beginning of the string, `re.match()` returns a match object, and the code prints "Match found!".

### search()

> This function searches for a regular expression pattern anywhere in a string. If the pattern is found, if the first is found or occurrence, it returns a match object, otherwise, it returns None.

```
import re
teststring="123abc456789abc123ABC"
pattern=re.compile(r"abc")
search=pattern.search(teststring)
print(search)
```

> `output:`
>
> > <re.Match object; span=(3, 6), match='abc'>

#### Search Example

```
import re
text = "apple banana cherry"
pattern = r"banana"
match_obj = re.search(pattern, text)

if match_obj:
    print("Match found!")
else:
    print("Match not found!")
print(match_obj.group())
```

> `output:`
>
> > Match found!
> > banana

`[Note]`In this example, re.search() searches for the pattern "banana" anywhere in the string "apple banana cherry". Since the pattern is found in the middle of the string, re.search() returns a match object, and the code prints "Match found!".

### findall()

> This function returns a list of all non-overlapping matches of a regular expression pattern in a string.

```
import re
teststring="123abc456789abc123ABC"
pattern=re.compile(r"abc")
match=pattern.findall(teststring)
for i in match:
    print(i)
```

> output
>
> > abc
> > abc

#### Findall Example:
```
import re
text = "apple banana cherry"
pattern = r"a"
match_list = re.findall(pattern, text)
print(match_list)
```

> `output:`
>
> > ['a', 'a', 'a', 'a']

### finditer()

> returns iterator of matched objects in the string while

```
import re
teststring="123abc456789abc123ABC"
pattern=re.compile(r"abc")
match=pattern.finditer(teststring)
for i in match:
    print(i)
```

> output:
>
> > `<re.Match object; span=(3, 6), match='abc'>` 
> > `<re.Match object; span=(12, 15), match='abc'>`

Or you can use this method without compile

```
match=re.finditer(r"abc",teststring)
for i in match:
    print(i)

```

### match vs search vs findall

> `match()` is used when you want to check if a pattern exists at the beginning of a string, while `search()` is used checks for a match anywhere in the string of a pattern in a string, and `findall() `is used when you want to extract multiple occurrences of a pattern from a string.

#### Example 1 match search findall

```
import re
text ='https://chenchih.page , Author is chenchih'
print("====match=======")
patternresult1=re.match('https', text)
patternresult2=re.match('chenchih', text)
print("match: https",patternresult1)
print("match: chenchih",patternresult2)
print("====search=======")
patternresult1=re.search('https', text)
patternresult2=re.search('chenchih', text)
print("search: https",patternresult1)
print("search: chenchih",patternresult2)

print("====findall=======")
patternresult1=re.findall('https', text)
patternresult2=re.findall('chenchih', text)
print("findall: https",patternresult1)
print("findall: chenchih",patternresult2)
```
> `output:`
> > ====match=======
> > match: https <re.Match object; span=(0, 5), match='https'>
> >match: chenchih None
> > ====search=======
> > search: https <re.Match object; span=(0, 5), match='https'>
> > search: chenchih <re.Match object; span=(8, 16), match='chenchih'>
> > ====findall=======
> > findall: https ['https']
> > findall: chenchih ['chenchih', 'chenchih']

#### Example2: match and search

```
import re
line = "Cats are smarter than dogs"
matchObj = re.match(r'dogs', line, re.M | re.I)
if matchObj:
    print("match --> matchObj.group() : ", matchObj.group())
else:
    print("No match!!")
searchObj = re.search(r'dogs', line, re.M | re.I)
if searchObj:
    print("search --> searchObj.group() : ", searchObj.group())
else:
    print("Nothing found!!")

```

> output:
>
> > No match!!
> > search --> searchObj.group() : dogs

## Methods on a Match object 
| Method  | 說明                                            |
| :------- | :------------------------------------------------ |
|group()|	Return the string matched by the RE|
|start()| 	Return the starting position of the match|
|end()	|Return the ending position of the match|
|span()	|Return a tuple containing the (start, end) positions of the match|

```
import re
teststring="123abc456789abc123ABC"
pattern=re.compile(r"abc")
match=pattern.finditer(teststring)
for i in match:
    print(i.span()) # or 
    print(i.span(), match.start(), match.end())
```
> `output:`
>> (3, 6)
>> (3, 6) 3 6
>> (12, 15)
>> (12, 15) 12 15


### Group option
When match/search/findall function returns a match object on success, none on failure. We use group(num) or groups() function of match object to get matched expression.

```
import re
text ='https://chenchih.page , Author is chenchih'
re1=re.match('http', text).group()
re2=re.search('https', text).group()
print(re1) #http
print(re2) #https
```
> `output:`
> > http
> > https

- Match Group Example
```
import re
text = "My favorite fruits are apples and bananas."
pattern = r"My favorite fruits are (.*?) and (.*?)\."
match_obj = re.match(pattern, text)

if match_obj:
    fruit1 = match_obj.group(1)
    fruit2 = match_obj.group(2)
    print("Fruits:", fruit1, "and", fruit2)
else:
    print("Match not found.")
```
> `Output:`
>> Fruits: apples and bananas

In this example, the regular expression pattern My favorite fruits are `(.*?)` and `(.*?)`. matches the text "My favorite fruits are " followed by two fruits separated by the word "and" and ending with a period. The two groups `(.*?)` capture the two fruit names, and the backslash is used to escape the period at the end of the sentence. 


- Search Group Example
```
import re

text = "The quick brown fox jumps over the lazy dog."
pattern = r"(brown|red) fox jumps over"

match_obj = re.search(pattern, text)

if match_obj:
    color = match_obj.group(1)
    print("Color:", color)
else:
    print("Match not found.")
```
> `output:`
>> Color: brown

In this example, the regular expression pattern `(brown|red)` fox jumps over matches either the text "brown fox jumps over" or "red fox jumps over". The group() method is then used to extract the text that was captured by the group.

## meta character or special character
|Example|說明|
| :----------- | :------------------------------- |
|.	|Any character (except newline character) `he..o`|
|^	|Starts with `^hello`|
|\$|	Ends with `world\$`|
|*	|Zero or more occurrences `aix*`|
|+ |	One or more occurrences `aix+`|
|{}	| Exactly the specified number of occurrences `al{2}`|
|[]	|A set of characters `[a-m]`|
|\	|Signals a special sequence (can also be used to escape special characters) `\d`|
|\|	|Either or `falls\|stays`|
|()	|Capture and group|

### Example:
####  `.` dot any character
> `.` Dot, default mode, this matches any character except a newline.

```
import re
teststring = "123abc456789abc123ABC"
pattern = re.compile(r".")
match = pattern.finditer(teststring)
for i in match:
    print(i.group())
```
> `output:`
>> 1
2
3
a
b
c
4
5
6
7
8
9
a
b
c
1
2
3
A
B

####  `\` ignore special character 
> indicate special forms or to allow special character like `. ^ $ * + ?`
```
teststring = "123abc456789abc123ABC."
pattern = re.compile(r"\.")
for i in match:
    print(i)
```
> `output:`
>> <re.Match object; span=(21, 22), match='.'>

#### `^` check beginning
- check 123
```
teststring = "123abc456789abc123ABC"
pattern = re.compile(r"^123")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
> `output:`
>> <re.Match object; span=(0, 3), match='123'>

- check abc
```
teststring = "123abc456789abc123ABC."
pattern = re.compile(r"^abc")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
> `output:`
>> empty because it’s not beginning

#### `$` check end
- abc
```
teststring = "123abc456789abc123ABC"
pattern = re.compile(r"abc$")
```
> `output:`
>> empty because case sensitive, let change string to ABC
Since it's case case sensitive, so it will return None

- ABC
> `pattern = re.compile(r"ABC$")`
>> `output: `
>> <re.Match object; span=(18, 21), match='ABC'>

##  Meta characters / Special Sequences

| Example      | 說明                                                                                       |
| :----------- | :------------------------------------------------------------------------------------- |
|\d |	Matches any decimal digit; this is equivalent to the class `[0-9]`.|
|\D |	Matches any non-digit character; this is equivalent to the class `[^0-9]`.|
|\s |	 Matches any whitespace character|
|\S |	 Matches any non-whitespace character;|
|\w |	Matches any alphanumeric (word) character; this is equivalent to the class `[a-zA-Z0-9_]`.|
|\W| 	Matches any non-alphanumeric character; this is equivalent to the class `[^a-zA-Z0-9_]`.|
|\b| 	Returns a match where the specified characters are at the beginning or at the end of a word r`"\bain"` |r"ain\b"|
|\B 	|Returns a match where the specified characters are present, but NOT at the beginning (or at the end) of a word r`"\Bain"` r`"ain\B"\`|
|\A 	|Returns a match if the specified characters are at the beginning of the string `"\AThe"`|
|\Z	|Returns a match if the specified characters are at the end of the string `"Spain\Z"`|

### Example:

#### `\d` decimal and `D` non Decimal
- `d`: `re.compile(r"\d")` 
```
teststring = "hello 123_ heyho hohey"
pattern = re.compile(r"\d")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
> output:
> > `<re.Match object; span=(6, 7), match='1'>`
`<re.Match object; span=(7, 8), match='2'>`
`<re.Match object; span=(8, 9), match='3'>`

- `D`: `re.compile(r"\D")`
```
teststring = "hello 123_ heyho hohey"
pattern = re.compile(r"\D")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
> `output:`
>> <re.Match object; span=(0, 1), match='h'>
<re.Match object; span=(1, 2), match='e'>
<re.Match object; span=(2, 3), match='l'>
<re.Match object; span=(3, 4), match='l'>
<re.Match object; span=(4, 5), match='o'>
<re.Match object; span=(5, 6), match=' '>
<re.Match object; span=(9, 10), match='_'>
<re.Match object; span=(10, 11), match=' '>
<re.Match object; span=(11, 12), match='h'>
<re.Match object; span=(12, 13), match='e'>
<re.Match object; span=(13, 14), match='y'>
<re.Match object; span=(14, 15), match='h'>
<re.Match object; span=(15, 16), match='o'>
<re.Match object; span=(16, 17), match=' '>
<re.Match object; span=(17, 18), match='h'>
<re.Match object; span=(18, 19), match='o'>
<re.Match object; span=(19, 20), match='h'>
<re.Match object; span=(20, 21), match='e'>
<re.Match object; span=(21, 22), match='y'>

#### `\s` space
```
teststring = "hello 123_ heyho hohey"
pattern = re.compile(r"\s")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
> `output:`
> > <re.Match object; span=(5, 6), match=' '>
<re.Match object; span=(10, 11), match=' '>
<re.Match object; span=(16, 17), match=' '>
 
#### `W` word and `w`
-  `w` match character
```
teststring = "hello 123_ heyho hohey"
pattern = re.compile(r"\w")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
> `output:`
> > <re.Match object; span=(0, 1), match='h'>
<re.Match object; span=(1, 2), match='e'>
<re.Match object; span=(2, 3), match='l'>
<re.Match object; span=(3, 4), match='l'>
<re.Match object; span=(4, 5), match='o'>
<re.Match object; span=(6, 7), match='1'>
<re.Match object; span=(7, 8), match='2'>
<re.Match object; span=(8, 9), match='3'>
<re.Match object; span=(9, 10), match='_'>
<re.Match object; span=(11, 12), match='h'>
<re.Match object; span=(12, 13), match='e'>
<re.Match object; span=(13, 14), match='y'>
<re.Match object; span=(14, 15), match='h'>
<re.Match object; span=(15, 16), match='o'>
<re.Match object; span=(17, 18), match='h'>
<re.Match object; span=(18, 19), match='o'>
<re.Match object; span=(19, 20), match='h'>
<re.Match object; span=(20, 21), match='e'>
<re.Match object; span=(21, 22), match='y'>

- `W` match non character `re.compile(r"\W")`
```
teststring = "hello 123_ heyho hohey"
pattern = re.compile(r"\W")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
>> `output:`
>>　<re.Match object; span=(5, 6), match=' '>
<re.Match object; span=(10, 11), match=' '>
<re.Match object; span=(16, 17), match=' '>

#### `b`block 
- find beginning of a block \b
> `pattern = re.compile(r"\bhey")`
>> `output:`
>> <re.Match object; span=(11, 14), match='hey'>
![ ](https://i.imgur.com/fCBdVqv.png)

 - find \B opposite of \b
> `teststring = "hello 123_ heyho hohey"`
> `output`
> > <re.Match object; span=(19, 22), match='hey'>

## Sets

| Example      | 說明                                                                                       |
| :----------- | :------------------------------------------------------------------------------------- |
| `[arn]`      | Returns a match where one of the specified characters (a, r, or n) are present             |
| `[a-n]`      | Returns a match for any lower case character, alphabetically between a and n               |
| `[^arn]`     | Returns a match for any character EXCEPT a, r, and n                                       |
| ` [0123-]`   | Returns a match where any of the specified digits (0, 1, 2, or 3) are present              |
| `[0-9]`      | Returns a match for any digit between 0 and 9                                              |
| `[0-5][0-9]` | Returns a match for any two-digit numbers from 00 and 59                                   |
| `[a-zA-Z]`   | Returns a match for any character alphabetically between a and z, lower case OR upper case |

### Example
#### `[]` look for any single character contain l or 0
```
teststring = "hello 123_"
pattern = re.compile(r"[lo]")
match = pattern.finditer(teststring)
```
> `output:`
> > <re.Match object; span=(2, 3), match='l'>
> > <re.Match object; span=(3, 4), match='l'>
> > <re.Match object; span=(4, 5), match='o'>

#### `[]` range `A-Z`
```
teststring = "hello 123_"
pattern = re.compile(r"[a-z]")
```
> `output:`
>
>> <re.Match object; span=(0, 1), match='h'>
>> <re.Match object; span=(1, 2), match='e'>
>> <re.Match object; span=(2, 3), match='l'>
>> <re.Match object; span=(3, 4), match='l'>
>> <re.Match object; span=(4, 5), match='o'>

you can also use `[0-9]` to find digit which is same as`\d`

## quantifiers

| character     | 說明                                                           |
| :------------ | :------------------------------------------------------------- |
| `*`           | 0 or more                                                      |
| `+`  | 1 or more                                                              |
| `?`           | 0 or 1, used when a character can be optional may exist or not |
| `{4}`         | exact number                                                   |
| `{4,6}`       | range numbers (min, max)                                       |
| `*`       | match 0 or more                                                |

### Example:
#### `*` match 0 or more
- `\d*` match `hello_123`
```
import re
teststring = "hello_123"
pattern = re.compile(r"\d*")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
> `output:`
>
> > <re.Match object; span=(0, 0), match=''>
<re.Match object; span=(1, 1), match=''>
<re.Match object; span=(2, 2), match=''>
<re.Match object; span=(3, 3), match=''>
<re.Match object; span=(4, 4), match=''>
<re.Match object; span=(5, 5), match=''>
<re.Match object; span=(6, 9), match='123'>
<re.Match object; span=(9, 9), match=''>

#### `+`  match 1 or more
- match`\d+` decimal `hello_123`
```
import re
teststring = "hello_123"
pattern = re.compile(r"\d+")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
> `output:`
>
> > <re.Match object; span=(6, 9), match='123'>

- match decimal `_\d`with `hello_123`
```
teststring = "hello_123"
pattern = re.compile(r"_\d")
```
> `output:`
>> <re.Match object; span=(5, 7), match='_1'>

- match decimal `_\d`with `hello123`
```
teststring = "hello123"
pattern = re.compile(r"_\d")
```
> `output:`
> > no match


#### `?` match 0 or 1
- `_?\d` with `hello123`
```
teststring = "hello123"
pattern = re.compile(r"_?\d")
```
> `output:`
>> <re.Match object; span=(5, 7), match='_1'>
<re.Match object; span=(7, 8), match='2'>
<re.Match object; span=(8, 9), match='3'>

- `_?\d` with `hello_1_2_3`
```
teststring = "hello_1_2_3"
pattern = re.compile(r"_?\d")
```
> `output:`
>> <re.Match object; span=(5, 7), match='_1'>
<re.Match object; span=(7, 9), match='_2'>
<re.Match object; span=(9, 11), match='_3'>


#### `{x,y}`  range numbers 
- `{x,y}` or `{n}` with `hello123`
```
teststring = "hello123"
pattern = re.compile(r"\d{1,3}")
match = pattern.finditer(teststring)
for i in match:
    print(i)
```
or `pattern = re.compile(r"\d{3}")`
`
> `output:`
>> <re.Match object; span=(5, 8), match='123'>


#### `.*` greedy
> This is greedy: it matches as much as it can, 
> The longest possible string ending in h
![](https://i.imgur.com/2PC3wgE.png)

#### `.*?` non greedy
> 	The ? makes the .* non-greedy, matching as little as it can to make a match, and the parenthesis makes it a capture group as well. 
>	The shortest possible string ending in h
![](https://i.imgur.com/GMV31XK.png)
![](https://i.imgur.com/LG1p6rT.png)


#### Date Example

```
import re
dates = '''
01.04.2020
2020.04.01
2020-04-01
2020-05-23
2020-06-11
2020-07-11
2020-08-11
2020/04/02
2020_04_04
2020_04_04
```

- `\d\d\d\d.\d\d.\d\d`
```
pattern = re.compile(r'\d\d\d\d.\d\d.\d\d')
matches=pattern.finditer(dates)
for i in matches:
    print(i)
```
> `output:`
>> <re.Match object; span=(13, 23), match='2020.04.01'>
<re.Match object; span=(25, 35), match='2020-04-01'>
<re.Match object; span=(36, 46), match='2020-05-23'>
<re.Match object; span=(47, 57), match='2020-06-11'>
<re.Match object; span=(58, 68), match='2020-07-11'>
<re.Match object; span=(69, 79), match='2020-08-11'>
<re.Match object; span=(81, 91), match='2020/04/02'>
<re.Match object; span=(93, 103), match='2020_04_04'>
<re.Match object; span=(104, 114), match='2020_04_04'>

- `\d\d\d\d[-/]\d\d[-/]\d\d`
> `re.compile(r'\d\d\d\d[-/]\d\d[-/]\d\d')`
> `output:`
> > <re.Match object; span=(25, 35), match='2020-04-01'>
<re.Match object; span=(36, 46), match='2020-05-23'>
<re.Match object; span=(47, 57), match='2020-06-11'>
<re.Match object; span=(58, 68), match='2020-07-11'>
<re.Match object; span=(69, 79), match='2020-08-11'>
<re.Match object; span=(81, 91), match='2020/04/02'>

- `\d\d\d\d[-/]0[56][-/]\d\d`
> `re.compile(r'\d\d\d\d[-/]0[56][-/]\d\d')`
> `output:`
>> <re.Match object; span=(36, 46), match='2020-05-23'>
<re.Match object; span=(47, 57), match='2020-06-11'>

-`\d\d\d\d[-/]0[5-7][-/]\d\d` or `\d{4}`
> `re.compile(r'\d\d\d\d[-/]0[5-7][-/]\d\d')`
or
> `re.compile(r'\d{4}[-/]0[5-7][-/]\d{2}')`
or 
> `output:`
>> <re.Match object; span=(36, 46), match='2020-05-23'>
<re.Match object; span=(47, 57), match='2020-06-11'>
<re.Match object; span=(58, 68), match='2020-07-11'>

change `\d\d\d\d` =>`\d{4}`, and `\d\d` =>`\d{2}`



## Condition 

```
my_string = """
hello world
1223
2020-05-20
Mr Simpson
Mrs Simpson
Mr. Brown
Ms Smith
Mr. T
"""
```
- `Mr\s\w+`
```
pattern = re.compile(r'Mr\s\w+')
matches=pattern.finditer(my_string)
for i in matches:
    print(i)
```
> `output:`
>> <re.Match object; span=(29, 39), match='Mr Simpson'>

- `\.?\s\w+`
> `re.compile(r'Mr\.?\s\w+')`
> `output:`
>> <re.Match object; span=(29, 39), match='Mr Simpson'>
<re.Match object; span=(52, 61), match='Mr. Brown'>
<re.Match object; span=(71, 76), match='Mr. T'>

let use condition we wants to get Mr, Mrs 
> `	re.compile(r'(Mr|Ms|Mrs)\.?\s\w+')`
> `output:`
>> <re.Match object; span=(29, 39), match='Mr Simpson'>
<re.Match object; span=(40, 51), match='Mrs Simpson'>
<re.Match object; span=(52, 61), match='Mr. Brown'>
<re.Match object; span=(62, 70), match='Ms Smith'>
<re.Match object; span=(71, 76), match='Mr. T'>


## grouping substring 
### email example
```
import re
my_string = """
pythonengineer@gmail.com
Python-engineer@gmx.de
python-engineer123@my-domain.org
"""
```

- `[a-zA-z0-9-]+@`
```
pattern = re.compile(r'[a-zA-z0-9-]+@')
matches=pattern.finditer(my_string)
for i in matches:
    print(i)
```
> `output:`
> > <re.Match object; span=(1, 16), match='pythonengineer@'>
<re.Match object; span=(26, 42), match='Python-engineer@'>
<re.Match object; span=(49, 68), match='python-engineer123@'>

- `[a-zA-z0-9-]+@[a-zA-Z-]+\.`
> `pattern = re.compile(r'[a-zA-z0-9-]+@[a-zA-Z-]+\.')`
> `output:`
> > <re.Match object; span=(1, 22), match='pythonengineer@gmail.'>
<re.Match object; span=(26, 46), match='Python-engineer@gmx.'>
<re.Match object; span=(49, 78), match='python-engineer123@my-domain.'>

#### set and condition example
- condition email example:
```
#condition
pattern = re.compile(r'[a-zA-z0-9-]+@[a-zA-Z-]+\.(com|de|org)')
matches=pattern.finditer(my_string)
for i in matches:
    print(i)
```
- set email example 
```
#set
pattern =  re.compile(r'[a-zA-z0-9-]+@[a-zA-Z-]+\.[a-zA-z]+')
matches=pattern.finditer(my_string)
for i in matches:
    print(i)
```
> `output:`
> > <re.Match object; span=(1, 22), match='pythonengineer@gmail.'>
<re.Match object; span=(26, 46), match='Python-engineer@gmx.'>
<re.Match object; span=(49, 78), match='python-engineer123@my-domain.'>

- use group instead match
```
pattern = pattern = re.compile(r'([a-zA-z0-9-]+)@([a-zA-Z-]+)\.([a-zA-z]+)')
matches=pattern.finditer(my_string)
for i in matches:
    print(i.group())
```
> `output:`
> >  pythonengineer@gmail.com
Python-engineer@gmx.de
python-engineer123@my-domain.org


## Modifying strings method

| Method   | 說明                                                                          |
| :------- | :---------------------------------------------------------------------------- |
| split()    | Split the string into a list, splitting it wherever the RE matches            |
| sub()  | Findall substrings where the RE matches, and replace them with a different string |

### Re.sub()
- substitute or replace Example 
```
import re
my_string = 'hello world, you are the best world'
pattern = re.compile(r'world')
substring=pattern.sub("planet", my_string)
print(substring)
```
> `output:`
> >  hello planet, you are the best planet

- URL Example
```
text ='https://chenchih.page , Author is ChenChih'
newtext= re.sub('chenchih', 'CC' ,text)
print(newtext) #https://CC.page , Author is ChenChih
newtext= re.sub('[C|c]hen[C|c]hih', 'CC' ,text)
print(newtext) #https://CC.page , Author is CC
```
> `output:`
> >  https://CC.page , Author is ChenChih
> >  https://CC.page , Author is CC


### Re.split()
- split string example
```
import re
my_string = '123abc456789abc123ABC'
pattern = re.compile(r'abc')
splitted=pattern.split(my_string)
print(splitted)
```
> `output:`
>> ['123', '456789', '123ABC']

### URL Example
```
import re
urls = """
http://python-engineer.com
https://www.python-engineer.org
http://www.pyeng.net
"""
```
- ex2.1 
```
pattern=re.compile(r"https?://(www\.)?([a-zA-Z-]+)\.[a-zA-Z]+")
matches=pattern.finditer(urls)
for i in matches:
    print(i)
```
> `output:`
>> <re.Match object; span=(1, 27), match='http://python-engineer.com'>
<re.Match object; span=(28, 59), match='https://www.python-engineer.org'>
<re.Match object; span=(60, 80), match='http://www.pyeng.net'>

- ex2.2
```
pattern=re.compile(r"https?://(www\.)?([a-zA-Z-]+)(\.[a-zA-Z]+)")
matches=pattern.finditer(urls)
for i in matches:
    print(i.group())
suburl=pattern.sub(r"\2\3", urls)
print(suburl)
```
> `output:`
```
http://python-engineer.com
https://www.python-engineer.org
http://www.pyeng.net

python-engineer.com
python-engineer.org
pyeng.net
```

- ex2.3
```
matches=pattern.finditer(urls)
for i in matches:
    print(i.group(1))
    print(i.group(2))
    print(i.group(3))

```
>  `output`
```
None
python-engineer
.com
www.
python-engineer
.org
www.
pyeng
.net
```

## Flag

| Flag   | 說明                                                                       |
| :------- | :----------------------------------------------------------- |
|re.A ( re.ASCII )|	Makes several escapes like \w, \b, \s and \d match only on ASCII characters with the respective property.|
|re.I (re.IGNORECASE )	|case-insensitive matching|
|re.M ( re.MULTILINE )	| Multi-line matching,  =used with metacharacter ^ (caret) and $ (dollar)|
|re.S ( re.DOTALL )|	DOT (.) special character match any character at all, including a newline. Without this flag, DOT(.) will match anything except a newline|
|re.X ( re.VERBOSE )	|comment in the regex. Enable verbose REs, which can be organized more cleanly and understandably.|
|re.L (re.LOCALE )	|case-insensitive matching dependent on the current locale. Use only with bytes patterns|

### example1
```
import re
text ='https://chenchih.page , Author is ChenChih'
pattern=re.compile('Chenchih',re.I) #chenchih
matches=pattern.finditer(text)
for match in matches:
    print(match)
```
> `output`
> > <re.Match object; span=(8, 16), match='chenchih'>
<re.Match object; span=(34, 42), match='ChenChih'>

```
import re
string="Hello World"
pattern=re.compile(r"world", re.I)
matches=pattern.finditer(string)
for match in matches:
    print(match)
```
> `output`
> > <re.Match object; span=(6, 11), match='World'>
## Reference
- https://superuser.com/questions/1123701/what-is-the-difference-between-and-in-regex
- https://stackoverflow.com/questions/27881366/regular-expressions-and
- https://stackoverflow.com/questions/22937618/reference-what-does-this-regex-mean
- https://rubular.com/r/N5yX9LTWTo
- https://regex101.com/
- https://chwang12341.medium.com%E7%B5%A6%E8%87%AA%E5%B7%B1%E7%9A%84python%E5%B0%8F%E7%AD%86%E8%A8%98-%E5%BC%B7%E5%A4%A7%E7%9A%84%E6%95%B8%E6%93%9A%E8%99%95%E7%90%86%E5%B7%A5%E5%85%B7-%E6%AD%A3%E5%89%87%E8%A1%A8%E9%81%94%E5%BC%8F-regular-expression-regex%E8%A9%B3%E7%B4%B0%E6%95%99%E5%AD%B8-a5d20341a0b2
