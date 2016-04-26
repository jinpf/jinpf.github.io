---
layout: post
title:  "Liunx一些常用命令"
date:   2016-03-02 10:10:10
categories: Liunx
excerpt: 记录一些Liunx常用命令以备以后查阅
---

* content
{:toc}


## 查看电脑信息

```shell
# 查看CPU信息
cat /proc/cpuinfo

# 显示当前硬件信息
sudo lshw

# 显示内存信息
free

# 显示硬盘存储信息
df -h
```

## 后台运行程序

正在运行程序强制后台运行： `ctrl+z`，系统显示前面的编号就是作业号。

```shell
#查看后台运行程序：
jobs

#将后台运行程序转到前台：
fg %jobnum  #jobnum代表作业号

#将一个在后台暂停的命令，变成继续执行
bg %jobnum  #jobnum代表作业号

#从后台启动程序（注意：如果关闭shell，该程序也会关闭）
cmd &  #cmd代表要启动的程序
```

## 结果重定向

将命令行结果重定向到文件中，命令行不显示

```shell
# 将正确和错误的输出都重写输出到文件中，如果cmd为：类似于touch
cmd &> filename
# 将正确和错误的输出追加到文件中
cmd &>> filename
```

将命令行结果重定向到文件中，同时命令行显示

```shell
# 重写的方式
cmd | tee filename
# 追加的方式
cmd | tee -a filename
```