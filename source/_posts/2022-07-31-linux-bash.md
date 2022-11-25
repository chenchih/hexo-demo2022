---
title: Linux Bash Script
date: 2022-07-31 08:07:57
tags: 
- linux 
- bash
categories:
- linux 
---
今天我想分享如何用linux shell script 語法。
我們需要加這個在script裡面，然後檔案改成`.sh`

```
#! /bin/bash
```

- How to execute script
> `chmod 777 myscript.sh`
> `./myscript.sh`

## 1. variable 
### define variable
```
text1=Hello
name=CC
echo $text1 $name
```
> output:
>> Hello CC

### read and echo variable
> read variable
>> read a

> read vairable without skip new line: 
>> read -p "Your Options: " option

> echo without new line
>> echo -n "message" 

#### example: 
```
echo "======================IPERF==================="
echo "1) "
echo "2) "
echo "q) "
echo "============================="
echo -n "Choice:"
read choice
```
### expression
> `var=$((3+9))`
> `echo $var`
>> output:
>>　12


- example 
```
echo "Enter a numner"
read a
echo "Enter a numner"
read b
echo $sum
echo $a $b
sum=$((a+b))
```

## 2. condition

### if elif else 
#### Syntax
```
if [[ condition ]]
then
	statement
elif [[ condition ]]; then
	statement 
else
	do this by default
fi
```

> check file empty
>> `if [[ -z "$tftp_dir" ]]`

#### example
```
read x
read y

if [ $x -gt $y ]
then
echo X is greater than Y
elif [ $x -lt $y ]
then
echo X is less than Y
elif [ $x -eq $y ]
then
echo X is equal to Y
fi
```

## 3. Loop
### for loop
#### loop number
```
for i in {1..5}
do
    echo $i
done
```
#### Looping with strings

```
for X in hello world 
do
	echo $X
done
```

### while loop
#### adding 1 ~100
```
#!/bin/bash
i=1
while [[ $i -le 10 ]] ; do
   echo "$i"
  (( i += 1 ))
done
```

###  get arguments for scripts

```
#!/bin/bash
for x in $@
do
    echo "Entered arg is $x"
done
```

> ./filename value1 value2 value3