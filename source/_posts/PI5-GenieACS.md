---
tags:
  - linux
  - network
categories:
  - linux
  - ubuntu
date: 2025-08-28 18:48:35
---

今天想分享我用 Rassberry PI5 架 ACS Server，如果你知道 ACS Server 是甚麼，可以看我如何架。ACS Auto Configure server，類似遠端的工具可以看到你的通訊產品的狀況如上線時間，reboot,更新 FW 等等

# Raspberry PI Model

- Check Ubuntu Version

```
lsb_release -a
```

- Check Kernel

```
uname -ar
```

- check Raspberry Model

```
cat /proc/device-tree/model
#or
cat /proc/cpuinfo | grep 'Model'
```

- Check CPU type

```
lscpu
```

# Install Genie ACS

##

```
curl -sL https://deb.nodesource.com/setup_14.x -o nodesource_setup.sh
sudo bash nodesource_setup.sh
sudo apt install nodejs
node -v
```
