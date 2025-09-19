---
title: Rassberry Genie ACS
date: 2025-09-13 09:00:00
tags:
  - linux
  - network
categories:
  - linux
  - ubuntu
---

今天想分享我用 Rassberry PI5 架 ACS Server，如果你知道 ACS Server 是甚麼，可以看我如何架。ACS Auto Configure server，類似遠端的工具可以看到你的通訊產品的狀況如上線時間，reboot,更新 FW 等等

> **Note:**
>
> > For English Note please refer to my [github note link](https://github.com/chenchih/Env_Setup_Note/tree/master/Linux_SetEnv/GenieACS)

# Raspberry PI Model

## Check Ubuntu Version

```
lsb_release -a
```

{% asset_img checkOS.png %}

## Check Kernel

```
uname -ar
```

## check Raspberry Model

```
cat /proc/device-tree/model
#or
cat /proc/cpuinfo | grep 'Model'
```

{% asset_img modelType.png %}

## Check CPU type

```
lscpu
```

{% asset_img CPUType.png %}

# Install Genie ACS

我有寫自動化可以自行幫你架，如果有興趣可以到這[連結](https://github.com/chenchih/Env_Setup_Note/blob/master/Linux_SetEnv/GenieACS/genie_acs_new.sh).

這是整個架構圖

{% asset_img genie_automatic.png%}

> **Note:**
>
> > 以下我都是以**ubuntu 24.04/25.04** 為主，但如果你是用**20.04 我下面會提示說明他是 20.04**

## Download and Install nodejs

```
curl -sL https://deb.nodesource.com/setup_14.x -o nodesource_setup.sh
sudo bash nodesource_setup.sh
sudo apt install nodejs
node -v
```

## MongoDB

### MogoDB GPG Key

```
#update
sudo apt update
#install curl
sudo apt install gnupg curl -y
#use curl to download MongoDB
curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | \ sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg \ --dearmor
```

### Mongodb 下載

```
#add the url into sources.list
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/8.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-8.0.list
#update
sudo apt update
```

> **Note:**
>
> > 如果是 20.04 請用下面方式因為是 SSL1.1

```
sudo apt update
sudo apt install mongodb-org
sudo systemctl start mongod.service
sudo systemctl status mongod
sudo systemctl enable mongod
mongo --eval 'db.runCommand({ connectionStatus: 1 })'
```

#### 安裝 mogodb

```
# Install MongoDB
sudo apt install -y mongodb-org
```

#### 啟動 mongod

```
# Start and Enable the MongoDB Service
sudo systemctl start mongod
sudo systemctl enable mongod
sudo systemctl status mongod
```

## GenieACS

一下是修改 genieacs 檔案

## 下載/安裝

```
sudo apt update
sudo apt install nodejs npm

sudo npm install -g genieacs@1.2.13
sudo useradd --system --no-create-home --user-group genieacs

mkdir /opt/genieacs
mkdir /opt/genieacs/ext
chown genieacs:genieacs /opt/genieacs/ext
```

## GenieACS 設定

### genieacs.env

> 請修改 genieacs 檔: `vi /opt/genieacs/genieacs.env`

```
GENIEACS_CWMP_ACCESS_LOG_FILE=/var/log/genieacs/genieacs-cwmp-access.log
GENIEACS_NBI_ACCESS_LOG_FILE=/var/log/genieacs/genieacs-nbi-access.log
GENIEACS_FS_ACCESS_LOG_FILE=/var/log/genieacs/genieacs-fs-access.log
GENIEACS_UI_ACCESS_LOG_FILE=/var/log/genieacs/genieacs-ui-access.log
GENIEACS_DEBUG_FILE=/var/log/genieacs/genieacs-debug.yaml
NODE_OPTIONS=--enable-source-maps
GENIEACS_EXT_DIR=/opt/genieacs/ext
```

### 修改權限

```
sudo chown genieacs:genieacs /opt/genieacs/genieacs.env
sudo chmod 600 /opt/genieacs/genieacs.env
```

### 加 jwt secret

如果你沒有加上 jwt secret 會出現在下面問題:

{% asset_img secretkey.png %}

```
node -e "console.log(\"GENIEACS_UI_JWT_SECRET=\" + require('crypto').randomBytes(128).toString('hex'))" >> /opt/genieacs/genieacs.env
```

### 建立 log 資料夾

```
mkdir /var/log/genieacs
chown genieacs:genieacs /var/log/genieacs
```

### 修改 genieacs systemd unit

#### genieacs-cwmp

看檔案在哪: `which genieacs-cwmp`

修改檔案: `sudo systemctl edit --force --full genieacs-cwmp`

```
[Unit]
Description=GenieACS CWMP
After=network.target

[Service]
User=genieacs
EnvironmentFile=/opt/genieacs/genieacs.env
ExecStart=/usr/local/bin/genieacs-cwmp

[Install]
WantedBy=default.target
```

> **Note:**
>
> > 如果 Ubuntu 20.04 修改成

```
ExecStart=/usr/bin/genieacs-cwmp
```

#### genieacs-fs

看檔案在哪: `which genieacs-fs`

修改檔案: `sudo systemctl edit --force --full genieacs-fs`

```
[Unit]
Description=GenieACS FS
After=network.target

[Service]
User=genieacs
EnvironmentFile=/opt/genieacs/genieacs.env
ExecStart =/usr/local/bin/genieacs-fs

[Install]
WantedBy=default.target
```

> **Note:**
>
> > 如果 Ubuntu 20.04 修改成

```
ExecStart=/usr/bin/genieacs-fs
```

#### genieacs-ui

看檔案在哪: `which  genieacs-ui`

修改檔案: `sudo systemctl edit --force --full genieacs-ui`

```
[Unit]
Description=GenieACS UI
After=network.target

[Service]
User=genieacs
EnvironmentFile=/opt/genieacs/genieacs.env
ExecStart=/usr/local/bin/genieacs-ui

[Install]
WantedBy=default.target
```

> **Note:**
>
> > 如果 Ubuntu 20.04 修改成

```
ExecStart=/usr/bin/genieacs-ui
```

### logroate

修改檔案: `nano /etc/logrotate.d/genieacs`

```
/var/log/genieacs/*.log /var/log/genieacs/*.yaml {
    daily
    rotate 30
    compress
    delaycompress
    dateext
}
```

### 啟動服務

設定做完可以啟動服務看有沒有問題

- 啟動服務

```
sudo systemctl enable genieacs-cwmp
sudo systemctl start genieacs-cwmp
sudo systemctl status genieacs-cwmp

sudo systemctl enable genieacs-nbi
sudo systemctl start genieacs-nbi
sudo systemctl status genieacs-nbi

sudo systemctl enable genieacs-fs
sudo systemctl start genieacs-fs
sudo systemctl status genieacs-fs

sudo systemctl enable genieacs-ui
sudo systemctl start genieacs-ui
sudo systemctl status genieacs-ui
```

# CPE 設定 ACS

## GenieACS 網頁啟動

如果上面沒問題可以開啟網頁 http://127.0.0.1:3000 或 http://<本地 IP>:3000 就會出現 genieacs 網頁，請點如圖連結來啟動她

{% asset_img activate.png %}

## CPE 註冊 ACS server

每加 CPE 用指令位置不一樣，就類似下面這樣。

```
setvalue Device.ManagementServer.URL="http://172.21.201.111:7547"
setvalue Device.ManagementServer.ConnectionRequestUsername="admin"
setvalue Device.ManagementServer.ConnectionRequestPassword="admin"
```

{% asset_img acs_online.PNG %}

## FW 升級設定

我們可以透過 ACS 做升級，但需要做一些設定如如下

### 加入 image 設定

- Step 1: 點去 Devices
- Step 2: 檢查 CPE 的 OUI, Product Class 複製
- Step 3: 點進 `Admin`
- Step 4: 選 `Files`，選`1.Firmware Upgrade Image` 把剛剛複製的資訊把它輸入或貼上去
- Step 5: 上傳你要的 image 上去

{% asset_img upgrade_image.PNG %}

### ACS 升級 CPEFW

上面有做 FW 設定，現在我們可以做 CPE 升級

- Step 1: 點去 Devices
- Step 2: 勾選取你要生的 CPE
- Step 3: 點 push
- Step 4: 選取你要升的 image
- Step 5: 點 queue 再點 commit

可以看下面圖片:
{% asset_img upload_fw.PNG %}

# Reference

- https://docs.genieacs.com/en/latest/installation-guide.html#install-genieacs
