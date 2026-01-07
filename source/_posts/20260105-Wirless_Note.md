---
title: 20260105_Wirless Note
date: 2026-01-05 16:55:37
tags:
  - network
  - wifi
categories:
  - Network
  - DebugNote
---

今天想要分享 WIFI 筆記跟，工具，和 CLI 指令

# Capture Wireless OTA Beacon

不同平台有不同抓法，我在這用 Linux 分享，因為它是免費也最簡單用。如果你有 MAC 那是最簡單方式，甚麼都不用安裝你需要有 wireshark。

There're many type of tool you can use to cpature, but I'm going to use the most easiest way to capture Wireless Beacon Packet OTA(AIR) packet. I will be using Linux which is free and easy to setup. If you have MAC then it's more easy no need to install any tool, just need a wireshark then you can capture.

## Step1 Install airmon-ng

Linux Distribution: Ubuntu

```
sudo apt install airmon-ng
```

## Step2 Check your Wirless interface

Please noted down your wirless interface ex: `wlan0`

```
ifconfig #to list all interface
```

## Step3 Run command

Please check your wirless current channel to capture else you're not able to capture. You can use tool like insider, or GUI to check current channel

- Capture

```
sudo airmon-ng check kill
sudo airmon-ng start <wlan> #your wirless interface
sudo iw dev <wlan>mon set channel <channel>
```

For example:

```
sudo airmon-ng start wlan0
sudo iw dev wlan0mon set channel 36
```

- Wireshark

You can filter your wireless backhaul or wifi interface for easy to debug or find the correct packet with below command, just paste the command into below wireshark picture the place where I mark red on it.

```
wlan host <MAC address>
```

{% asset_img wireshark-aircap.PNGg %}

- Finish Capture:

```
sudo airmon-ng stop <wlan>mon
sudo systemctl restart NetworkManager
```

## Step4 Wireshark

When you're capture overnight or overweekend, you need to set a special setting, else you disk might be full when capturing it.

{% asset_img wireshar_file_cpture.PNGg %}

Please enable `ring biffer` it will overwrite file after X size, in my example I set afer 200MB with 10 file, which total to 2GB. This mean after 10 file, the next time it will overwrite the first one.

# Wireless Command

I like to show you how to use wireless command to check current SSID around, or password you ever connected and forget. Please Noted the password is only able to check you ever type in password. You're not able to hack on any ssid password with command. The command is just for some productively without using mouse to connect.

However you can still hack ssid password by other security tool, which I am not going to cover here, you can search on internet if you're interested.

I will show you window and linux command some how they are different. This is useful especially if you remote to server or server does not contain UI interface.

## List saved SSID

This allow to list all the SSID you have ever connected before which mean you ever type in the password and connected.

```
#window
netsh wlan show profile

#linux
nmcli connection show
```

## Show Password

```
#window
netsh wlan show profile name="ssidname" key=clear

#linux
sudo nmcli connection show "My Home WiFi" | grep psk
```

## Scan all ssid

```
#window
netsh wlan show networks
#linux
nmcli device wifi list
```

- Show More detail infor (Window)

```
netsh wlan show networks mode=bssid
```

## Make a connection to SSID

In previous command you check available SSID you can use, now you need to make a connection

```
#linux
ncli device wifi connect "ssidname" password <ssidPassword>

#window
netsh wlan connect name="ssidname"
```

For window there if you connect first time, then follow below step. If you used to connected, then you above. In window to connected SSID need to have a profile file.

### First Time Connected (window)

There're several step to do before connecting only with window OS

#### Step 1 : Create a `ssid.xml` file (ex: `WIFI-CAK9XRN.xml`)

Please replace `{}` the string of your ssid, and password.

```
<?xml version="1.0"?>
<WLANProfile xmlns="http://www.microsoft.com/networking/WLAN/profile/v1">
    <name>{SSID}</name>
    <SSIDConfig>
        <SSID>
            <name>{SSID}</name>
        </SSID>
    </SSIDConfig>
    <connectionType>ESS</connectionType>
    <connectionMode>auto</connectionMode>
    <MSM>
        <security>
            <authEncryption>
                <authentication>WPA2PSK</authentication>
                <encryption>AES</encryption>
                <useOneX>false</useOneX>
            </authEncryption>
            <sharedKey>
                <keyType>passPhrase</keyType>
                <protected>false</protected>
                <keyMaterial>{password}</keyMaterial>
            </sharedKey>
        </security>
    </MSM>
    <MacRandomization xmlns="http://www.microsoft.com/networking/WLAN/profile/v3">
        <enableRandomization>false</enableRandomization>
    </MacRandomization>
</WLANProfile>
```

#### Step 2: Create xml file with interface

Let Create a profile with file you create in previous step, and you Wirless interface.

If you don't know your itnerface please use `netsh wlan show interfaces` to check which interface your wan is.

```
netsh wlan add profile filename=".\WIFI-CAK9XRN.xml" interface="Wi-Fi"
```

You can show profile again, it should display the profile you create

```
netsh wlan show profile
```

> **Note:** If you modify your `.xml` file, you need to remove the profile, else it will not apply

```
netsh wlan delete profile name="SSID"
```

#### Step3 connect ssid

```
netsh wlan connect name="WIFI-CAK9XRN"
```

#### Export your profile

```
#export all your profile (this is all saved network)
netsh wlan export profile key=clear

#export specfic profile
netsh wlan export profile name=profile name
```

## connect status

```
#linux
nmcli dev status

#window
netsh wlan show interfaces
```

## Forget Network (SSID)

```
#Linux
sudo nmcli connection delete "<CONNECTION_NAME ex: WIFI-CAK9XRN>"

#Window
netsh wlan delete profile name="<CONNECTION_NAME>"
```

## Discconect your SSID

```
#linux
nmcli device disconnect <interface Name ex: wlan0>

#window
netsh wlan disconnect
```

Alternative you can use

```
sudo nmcli connection down <CONNECTION_NAME>
```

## Wifi Summary:

Window is much complicated on setting, Linux is much easier, so I will list commonly use command

### Window

```
# get your ssid password
netsh wlan show profile name="<SSID Network Name>" key=clear

#show your profile
netsh wlan show profie

# connect SSID
netsh wlan connect name="<SSID Network Name>"

# connected status

# Forget SSID network
netsh wlan delete profile name="<SSID Network Name>"

# disconnect Wirless
nmcli device disconnect

# add profile the file contain ssid and password
netsh wlan add profile filename=<WirlessFIle.xml> interface=<WIFI Interface>

# delete profile
sudo nmcli connection delete <SSID Ntwork Name>
```

### Linux

```
# get your ssid password
sudo nmcli connection show "My Home WiFi" | grep psk

# show all ssid
nmcli device wifi list

# connect ssid
ncli device wifi connect "ssidname" password <ssidPassword>

# connected status
nmcli dev status

# Forget SSID network
netsh wlan delete profile name=<SSID Network Name>
# disconnect Wirless
nmcli device disconnect <interface Name ex: wlan0
```

## Reference:

- https://www.serverwatch.com/guides/netsh-commands/
- https://blog.csdn.net/qq_42887760/article/details/104343451
