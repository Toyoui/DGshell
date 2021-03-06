# DGshell
Deploy goedge Prelude based on docker in debian10.

Please ensure the purity of the system.

Requirements: Debian 64 bit architecture

## 1.Run 60% bases
```
wget -N https://raw.githubusercontent.com/Toyoui/DGshell/main/Dgshell.sh && bash Dgshell.sh
```

## 2.Edit my.cnf
```
cd /home/data/mysql/config vi my.cnf
```
### 2.1.Fill in the following
```
[mysqld]
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
datadir         = /var/lib/mysql
secure-file-priv= NULL
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0

# Custom config should go here
!includedir /etc/mysql/conf.d/

default_authentication_plugin= mysql_native_password
```

## 3.Run bases by docker
### 3.1.Run ansible/centos7-ansible
```
docker images
```
![图片](https://user-images.githubusercontent.com/91711069/172286956-0f2529d6-cf6b-4a9a-8703-568656318ae6.png)

```
docker run -d -i -t IMAGE ID /bin/bash

// eg: docker run -d -i -t 688353a31fde /bin/bash
```
### 3.2.Run mysql8
```
docker run \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=123456 \
    -v /home/data/mysql/data:/var/lib/mysql:rw \
    -v /home/data/mysql/log:/var/log/mysql:rw \
    -v /home/data/mysql/config/my.cnf:/etc/mysql/my.cnf:rw \
    -v /etc/localtime:/etc/localtime:ro \
    --name mysql8 \
    --restart=always \
    -d mysql
```
## 4.Get and Install Godege
### 4.1.Get
[Click to Goedge](https://goedge.cn/downloads)

![图片](https://user-images.githubusercontent.com/91711069/172288027-2d97a4a1-18ec-4115-96d3-0937e1e4a463.png)

Then copy the downloadlink
```
wget downloadlink

//eg: wget https://dl.goedge.cn/edge/v0.4.7.1/edge-admin-linux-amd64-plus-v0.4.7.1.zip
```
### 4.2.Install
```
unzip -o edge-admin-linux-amd64-plus-v0.4.7.1.zip
cd /root/edge-admin
bin/edge-admin start

// check it running
ps aux | grep edge-admin
```

