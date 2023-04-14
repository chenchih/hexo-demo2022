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

### match()

> This function matches a regular expression pattern at the beginning of a string. If the pattern is found, it returns a match object, otherwise, it returns None.

```
import re
teststring="123abc456789abc123ABC"
pattern=re.compile(r"abc")
match=pattern.match(teststring)
print(match)

```

> output:
>
> > None or empty
> > `[Note]: ` Match only match at the beginning, because abc is not in the beginning, so will return none.

#### Example

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
> > #apple

`[Note]` In this example, re.match() searches for the pattern "apple" at the beginning of the string "apple banana cherry". Since the pattern is found at the beginning of the string, re.match() returns a match object, and the code prints "Match found!".

### search()

> This function searches for a regular expression pattern anywhere in a string. If the pattern is found, if the first is found or occurrence, it returns a match object, otherwise, it returns None.

```
import re
teststring="123abc456789abc123ABC"
pattern=re.compile(r"abc")
search=pattern.search(teststring)
print(search)

```

> output:
>
> > `<re.Match object; span=(3, 6), match='abc'>`

#### Example

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

> output:
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

#### Example:

```
import re
text = "apple banana cherry"
pattern = r"a"
match_list = re.findall(pattern, text)
print(match_list)
```

> output:
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
> > `<re.Match object; span=(3, 6), match='abc'>` > > `<re.Match object; span=(12, 15), match='abc'>`

Or you can use this method without compile

```
match=re.finditer(r"abc",teststring)
for i in match:
    print(i)

```

### match vs search vs findall

> `match()` is used when you want to check if a pattern exists at the beginning of a string, while `search()` is used checks for a match anywhere in the string of a pattern in a string, and `findall() `is used when you want to extract multiple occurrences of a pattern from a string.

#### Example 1

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

> `output:`
>
> > No match!!
> > search --> searchObj.group() : dogs

## Group option

## meta character

### Sets

| Example      | 說明                                                                                       |
| :----------- | :----------------------------------------------------------------------------------------- |
| `[arn]`      | Returns a match where one of the specified characters (a, r, or n) are present             |
| `[a-n]`      | Returns a match for any lower case character, alphabetically between a and n               |
| `[^arn]`     | Returns a match for any character EXCEPT a, r, and n                                       |
| ` [0123-]`   | Returns a match where any of the specified digits (0, 1, 2, or 3) are present              |
| `[0-9]`      | Returns a match for any digit between 0 and 9                                              |
| `[0-5][0-9]` | Returns a match for any two-digit numbers from 00 and 59                                   |
| `[a-zA-Z]`   | Returns a match for any character alphabetically between a and z, lower case OR upper case |

#### Example 1 using [] look for any single character contain l or o

```
teststring = "hello 123_"
pattern = re.compile(r"[lo]")
match = pattern.finditer(teststring)
```

> `output:`
>
> > <re.Match object; span=(2, 3), match='l'>
> > <re.Match object; span=(3, 4), match='l'>
> > <re.Match object; span=(4, 5), match='o'>

#### Example 2 using range all letter a-z will match

```
teststring = "hello 123_"
pattern = re.compile(r"[a-z]")
```

> `output:`
>
> <re.Match object; span=(0, 1), match='h'>
> <re.Match object; span=(1, 2), match='e'>
> <re.Match object; span=(2, 3), match='l'>
> <re.Match object; span=(3, 4), match='l'>
> <re.Match object; span=(4, 5), match='o'>

you can also use `[0-9]` to find digit which is same as`\d`

### quantifiers

| character     | 說明                                                           |
| :------------ | :------------------------------------------------------------- |
| `*`           | 0 or more                                                      |
| `+` 1 or more |
| `?`           | 0 or 1, used when a character can be optional may exist or not |
| `{4}`         | exact number                                                   |
| `{4,6}`       | range numbers (min, max)                                       |
| Use `*`       | match 0 or more                                                |

#### Example1 - use `*` match 0 or more

```
teststring = "hello_123"
pattern = re.compile(r"\d*")
```

### Conditions

### grouping

## Modifying strings method

| Method   | 說明                                                                          |
| :------- | :---------------------------------------------------------------------------- |
| Split    | Split the string into a list, splitting it wherever the RE matches            |
| sub Find | all substrings where the RE matches, and replace them with a different string |

## Flag

## Reference
