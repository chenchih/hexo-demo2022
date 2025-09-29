---
title: Linux Command
date: 2022-07-30 08:07:57
tags: 
- linux
categories:
- linux 
- ubuntu
---

## alias
### Method 1: put your alias in `.alias_pofile`
Recommend use this file, will not destory `.bashrc` file. 
```
cd ~
touch .alias_pofile
```
### Method 2: edit `.bashrc`
This method need to reboot to take effect


## change directory 
### change folder or directory 
`cd` : change directory to home `~` directory
`cd folder`: change to specific directory
### change upper directory
`cd ..`: change upper  directory 
`cd ../..`:  change directory to 2 upper directory
`cd ../folder`: move upper directory and go to new direcotry
`cat ../folder/filename`: read upper directory filename 

## find 
- find file type `.sh`
> command:　`find . -type f -name "*.sh"`

## dump or write file 
### EOF read multipy line into file
#### Example 1
```
cat >>/etc/apt/sources.list<<EOF
######################
EOF
```

#### Example 2
```
cat << EOF > /etc/samba/smb.conf
[global]
workgroup = WORKGROUP
map to guest = bad user
EOF
```

## Write and Modify File
There are some shortcut key need to know using `vi` linux edit tool, which often use for edit file. Some people might use `nano`, `nvim`, or `vim` ; this is use for often vim. 

- Jump to specific line: `ctrl+G` + `line`
- search string: 
  - `/` or `?`
   - search next match string: `n`
- save file:
    - `wq` or `x!`: save and exit 
    - `q!`: exit without saving
- string select(visual mode): `ctrl+v`  select cursor反白選取文字 
  - copy: `y`
  - cut: `d`
  - paste: `p`
  - undo: `u`

## modify file with advance tool

### replace string from a file

-  Find and replace string to file
```
sed  -i 's/oldstring/newstring/g' xxx.txt
```
- Search string, and replace with new string and value
Search `TddConfigCommon.PatternType = TDD2` and change value like `P1` or `P2`
```
#change 
sed -i "/TddConfigCommon.PatternType = /c\TddConfigCommon.PatternType = P1" /home/test/Desktop/5GScript/confChange.txt
```
###