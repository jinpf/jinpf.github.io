---
layout: post
title:  "Ubuntu中文乱码解决办法"
date:   2016-03-10 10:10:10
categories: Liunx
excerpt: 中文乱码解决办法
---

* content
{:toc}

## 添加中文编码

```shell
sudo locale-gen
sudo dpkg-reconfigure locales
```

## 修改

```shell
/etc/default/locale
/etc/environment
```

添加或修改以下变量：

```shell
LANG="zh_CN.UTF-8"
LANGUAGE="zh_CN:zh:en_US:en"
```

## 重启

```shell
sudo reboot
```