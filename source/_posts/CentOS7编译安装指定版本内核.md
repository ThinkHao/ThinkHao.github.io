---
title: CentOS7编译安装指定版本内核
date: 2020-01-02 16:45:41
tags:
  - Linux
  - Kernel
categories:
  - Linux
---
工作中，在Linux服务器上部署服务时，常常有升级内核的需求，有过一两次的折腾经历，便想通过博客记录下来，方便日后查看。

以下操作步骤，均已在本地虚拟机中测试通过。
### 1.下载内核文件
```bash
cd /usr/local/src/
wget https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-5.2.11.tar.xz
```
### 2.解压压缩包
```bash
tar xf linux-5.2.11.tar.xz
```
### 3.把旧内核的配置文件拷贝到当前目录
```bash
cp /boot/config-3.10.0-957.el7.x86_64 ./.config
```
### 4.安装依赖包
```bash
yum -y groupinstall "development tools"
```
如果groupinstall报错，就添加参数--setopt=group_package_types=mandatory,default,optional
```bash
yum -y install ncurses-devel
yum -y install elfutils-libelf-devel openssh-devel bc
```
### 5.运行make menuconfig（窗口不能太小，否则会报错）
#### 1) 修改内核名称 General setup --->local version -append to kernel release
#### 2) 添加NTFS文件系统支持模块 File systems --->DOS/FAT/NT Filesystems --->NTFS file system support
### 6.编译安装模块
```bash
make modules_install
```
### 7.安装内核核心文件
```bash
make install
```
### 8.重启
```bash
reboot
```
重启后，正常情况下，内核就已经完成升级了。