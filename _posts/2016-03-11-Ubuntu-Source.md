---
layout: post
title:  "Ubuntu添加修改源地址"
date:   2016-03-11 10:10:10
categories: Liunx
excerpt: Ubuntu添加修改源地址
---

* content
{:toc}

---

## 修改sources.list

---

用编辑器打开 `/etc/apt/sources.list`，在末尾添加源地址，如以下内容

### 北邮镜像地址

```
deb ftp://openware.byr.edu.cn/pub/mirror/ubuntu/ precise main multiverse restricted universe
deb ftp://openware.byr.edu.cn/pub/mirror/ubuntu/ precise-backports main multiverse restricted universe
deb ftp://openware.byr.edu.cn/pub/mirror/ubuntu/ precise-proposed main multiverse restricted universe
deb ftp://openware.byr.edu.cn/pub/mirror/ubuntu/ precise-security main multiverse restricted universe
deb ftp://openware.byr.edu.cn/pub/mirror/ubuntu/ precise-updates main multiverse restricted universe
```    

### virtualbox源

添加网站：[https://www.virtualbox.org/wiki/Linux_Downloads](https://www.virtualbox.org/wiki/Linux_Downloads)

```
deb http://download.virtualbox.org/virtualbox/debian trusty contrib
deb http://download.virtualbox.org/virtualbox/debian saucy contrib
deb http://download.virtualbox.org/virtualbox/debian raring contrib
deb http://download.virtualbox.org/virtualbox/debian quantal contrib
deb http://download.virtualbox.org/virtualbox/debian precise contrib
deb http://download.virtualbox.org/virtualbox/debian lucid contrib non-free
deb http://download.virtualbox.org/virtualbox/debian wheezy contrib
deb http://download.virtualbox.org/virtualbox/debian squeeze contrib non-free
```   

```shell
#添加key
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
```

## add-apt-repository

该命令脚本添加ppa到当前的库中并自动导入公钥

### gcc/g++ 最新版仓库：

```shell
sudo add-apt-repository ppa:ubuntu-toolchain-r/test  
```

---

## 当从源获取数据错误时

---

### 如遇到： `The following signatures were invalid: BADSIG ...` 等时执行以下命令：

```shell
sudo -s -H
apt-get clean
rm /var/lib/apt/lists/*
rm /var/lib/apt/lists/partial/*
apt-get clean
apt-get update
```    

### 如遇到： `W:GPG错误：http://debian.ustc.edu.cn lucid Release: 运行 gpgv 时发生未知错误` 时解决方法：

```shell
mkdir temp
sudo mv /usr/local/lib/libreadline* temp
sudo ldconfig
sudo apt-get update
```