---
layout: post
title:  "NDN连通性测试工具-ndn-tlv-ping"
date:   2016-03-19 10:10:10
categories: CCN-NDN
excerpt: 基于NFD搭建的NDN网络，通过ndn-tlv-ping工具测试跨网连通性
---

* content
{:toc}

Reachability Testing Tool for NDN，其为NDN数据平面可达性测试工具。

安装使用参考：[https://github.com/named-data/ndn-tlv-ping](https://github.com/named-data/ndn-tlv-ping)

## 实验前提

* 安装了 ndn-cxx
* 安装了 NFD

## 实验步骤

### 安装ndn-tlv-ping

```shell
git clone https://github.com/named-data/ndn-tlv-ping.git
./waf configure
./waf
sudo ./waf install
```

### 使用

首先要有两台基于ip网络能ping通的电脑。

在一台电脑上（如ip：10.0.3.7）做pingserver：

```shell
nfd-start
# /test/pingserver为pingserver监听地址
ndnpingserver /test/pingserver
```    

在另一台电脑上（如ip：10.0.3.8）做pingclient：

```shell
nfd-start
# 配置FIB：添加pingserver的ip地址
nfdc register /test/pingserver udp4://10.0.3.7
ndnping /test/pingserver
```    

### 查看NFD状态

命令行方式：

```shell
nfd-status
```    

更直观的方式：

```shell
nfd-status-http-server
```

默认开启服务的地址：127.0.0.1：8080，可以通过 `man` 或 `-h` 查看更多设置选项。

ip:10.0.3.8主机 http显示效果如下：

![]({{"/pic/2016-3-19-0.png"}})

![]({{"/pic/2016-3-19-1.png"}})

![]({{"/pic/2016-3-19-2.png"}})

开始ip：10.0.3.7主机没有配置 FIB，故无 `/test/pingserver` 相关信息，之后开启pingserver:

![]({{"/pic/2016-3-19-3.png"}})

![]({{"/pic/2016-3-19-4.png"}})

当ip：10.0.3.8主机ping ip：10.0.3.7主机时自动多了这么一条：

![]({{"/pic/2016-3-19-5.png"}})
