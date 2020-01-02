---
title: CentOS7安装Docker-CE
date: 2020-01-02 10:24:29
tags:
  - Linux
  - Docker
categories:
  - Linux
---
### 1.OS需要为CentOS7的维护版，docker分为CE社区版和EE企业版
### 2.卸载系统自带的旧版本
```bash
  yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```
### 3.安装Docker CE
  #### 1）安装所需依赖包
  ```bash
  yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
  ```
  #### 2）导入docker的软件库（稳定版）
  ```bash
  yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
  ```
  #### 3）安装Docker CE
  默认安装最新版
  ```bash
  yum -y install docker-ce
  ```
  安装指定版本
  ```bash
  yum list docker-ce --showduplicates | sort -r
  yum install docker-ce-<VERSION STRING>
  ```
### 4.启动docker、设置开机自启
  ```bash
  systemctl start docker
  systemctl enable docker
  ```
### 5.测试docker安装
  ```bash
  docker run hello-world
  ```
### 6.卸载Docker-CE
  ```bash
  yum -y remove docker-ce
  rm -rf /var/lib/docker
  ```
### 或者直接脚本安装
  ```bash
  curl -fsSL https://get.docker.com -o get-docker.sh
  sh get-docker.sh
  ```