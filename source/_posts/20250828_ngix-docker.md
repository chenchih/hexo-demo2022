---
title: Setup Ngix and docker
date: 2025-08-28 16:44:06
tags:
  - linux
  - docker
categories:
  - linux
  - ubuntu
---

今天我想要分享用 UBUNTU 架設 ngix http server,同時我也會用 docker 方式安裝。

## NGIX Setup ubuntu

### Step1. Install Nginx

```
sudo apt install nginx -y
```

### Step2. show nginx status

Verify Nginx is Running show statusd

```
sudo systemctl status nginx
```

{% asset_img ngix_Status.PNG %}

### Step3: Firewall setting

```
sudo ufw allow 'Nginx HTTP'
sudo ufw reload
```

### Step4 Navigate browser to test Nginx

please navigate your web browser using your local IP it should occur index page

```
http://172.21.201.250
or
http://127.0.0.1
```

It will look like this, http web server is setup success

{% asset_img ngix_index.PNG %}

### Step5 (optional) Index to show like file management

- change permission

```
sudo chmod 644 /var/www/html/
```

- edit configure setting

```
sudo nano /etc/nginx/sites-available/default
    location / {
        try_files $uri $uri/ =404;
        autoindex on; # <--- Add this line
    }
```

- reload configure

Test Nginx configuration for syntax errors:

```
sudo nginx -t
```

Reload Nginx to apply changes

```
sudo systemctl reload nginx
```

- rename index.html to any other file type

```
sudo mv /var/www/html/index.nginx-debian.html /var/www/html/index.nginx-debian.html.bak
```

{% asset_img filemange.PNG %}

## NGIX Docker Setup

Ubuntu version: 20.04

### Step1 Install docker and enable services after boot

```
sudo apt update
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker chenchih # Add your user to the docker group
# Remember to log out and log back in (or reboot) for the group change to take effect
```

### Test docker 測試 Docker

```
docker run hello-world
```

### Pull ngix package

```
#Pull or Run Nginx in Docker
docker pull nginx:latest
```

### Run Nginx Container

Run the Nginx Container with this option:

- `--name my-nginx`: Gives your container a memorable name.
- `-p 8080:80`: Port mapping. Your Pi's 8080 will point to the container's 80.
- `-d`: Detached mode (runs in the background).
- `nginx`:latest: The image to use.

```
docker run --name my-nginx -p 8080:80 -d nginx:latest
```

{% asset_img runNgix.PNG %}

### Check Container running?

Note: You always use an image to create a container, so I will show how to list image and container.

- List and verify the Container is Running:

```
docker ps -a # Lists all containers, including  stopped items
```

{% asset_img listdocker.PNG %}

- Shows all the local images

```
docker images
```

The docker images command is used to list all the Docker images you have downloaded or built on your local machine. The images will be pull into this path: `/var/lib/docker/`, is the default storage location for all Docker data on Linux, not just images. This includes:

> - Images: The layers of all images you have pulled or built.
> - Containers: The writable layers of your running containers.
> - Volumes: The data for any named volumes you've created.
> - Networks: Configuration data for your Docker networks.

{% asset_img dockerImage.PNG %}

### Access the Nginx Web Server

You can access `http://localhost:8080` or instead use your IP address like `http://<your_pi_ip_address>:8080` it will look like below:

{% asset_img ngix_index.PNG %}

### Stop and remove the Container (Cleanup)

```
docker stop my-nginx # Stops the running container
docker rm my-nginx # Removes the container instance
```

check docker with `docker ps -a` will now show it's gone.

{% asset_img stop_Container.PNG %}

### Remove the downloaded image (to free space)

```
docker rmi nginx:latest
```

{% asset_img removeDockerimge.PNG %}

## Docker command summary

- `docker ps -a`: Show me all my containers (running or stopped).
- `docker rm <container_name_or_id>`: Please remove this specific container instance for me.
- `docker images`: Show me all the image blueprints I have downloaded.
- `docker rmi <image_name:tag_or_id>`: Please remove this specific image blueprint from my local storage.
