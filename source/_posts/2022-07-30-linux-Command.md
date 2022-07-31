---
title: Linux Command
date: 2022-07-30 08:07:57
tags: linux
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
