---
title: Network automatic Script for testing
date: 2025-09-28 17:24:39
tags:
  - network
  - automation
categories:
  - Network 
  - DebugNote
---

This is the automatic script which i will be using on debug or reproduce issue like stability test for Network.

## Shell Script 

This script will be added inside console, keep running and logged log. 

syntax of bashscript: 
```
#!/bin/sh
while true
do
   echo "Polling EthPhy Status !"


    sleep 1 ;
done
```


### Read top evey 60 second and logf file
```
while true; do
  date
  free
  top -b -n1 | head -15
  sleep 60
done >> /tmp/memlog.txt
```

### check bbu status every 10 second
```
#!/bin/sh
htx_pcd_app -a start -r BATTERY_HOST
while [ 1 ];
do
        date
        echo "####################"
        battery_host -m 1 -s
        echo "###################"
        echo ""
        echo "================"
        uci show bbu -c /var/tmp
        echo "================"
        sleep 10
        echo ""
        echo ""
done
```

## TTL Macro Script 

This is use when connect DUT to console, it will run command and record the log 


### Run stability and run some system command

In this script will run this command below to check is there any memory leak or high cpu. The purpose of this test is to verify Ipv6 drop, and acs will also not get ipv6 global after IP drop
- get acs ipv6 parameter: ` tr69_trigger getvalues Device.PPP.Interface.1.IPv6CP`
- ip address: `ifconfig`
- get free memory: `free -m`
- ps: `ps`
- top: `top -b -n1 | head -15`

```
:START
;sendln 'date'
pause 2
sendln ''
sendln 'echo "-----------------------------------"'
;sendln 'ifconfig'
pause 10
sendln ''
sendln ''
sendln ''
sendln ' tr69_trigger getvalues Device.PPP.Interface.1.IPv6CP'
pause 60


;sendln 'echo "System Memory (free -m)"'
;sendln 'free -m'
;pause 5
;sendln ''
;sendln ''



;sendln 'echo "ps"'
;sendln 'ps'
;pause 30
;sendln ''
;sendln ''

;sendln 'echo "top"'
;sendln 'top -b -n1 | head -15'
;pause 60
sendln 'echo "-----------------------------------"'
sendln ''
sendln ''
goto START

```

## Other scipt on system

### shell script: acs server clean log 
```
#chenchih 04/01/2021
#!/bin/bash
#3touch hhhhh.txt
#read -p "Please enter your log bane:" filename
echo "storage space"
df -h
locationlog="/opt/jboss/server/default/log"
cd $locationlog
ls
echo -n "Please enter your log name you want to delete:(ex:2021-03-01): " 
read filename
rm -f server.log.$filename*
echo "===================deleted================"
ls
```