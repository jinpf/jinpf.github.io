---
layout: post
title:  "Ubuntu系统重装后相关安装笔记"
date:   2016-03-01 10:10:10
categories: Liunx
excerpt: 因为要经常安装新系统，所以将一些基本配置记下来以备以后查阅
---

* content
{:toc}

因为要经常安装新系统，所以将一些基本配置记下来以备以后查阅

## 0、添加用户

---

```shell
adduser username
```
    
之后系统会交互式的帮忙添加

```shell
# 删除用户(连同主目录一起删除)：
userdel -r username 

# 如果有信息填错，可以直接修改 /etc/passwd 和 /etc/shadow
# 或者用 usermod、chfn
```

## 1、将用户添加到sudoer

---


使某些用户或者组可以执行sudo命令

```shell
$su
PassWord:
vi /etc/sudoers
```

在相应位置添加：`USER ALL(ALL)ALL`之类 

---

## 2、修改shell配置

---

`/home/user`下有个文件`.bashrc`

修改部分别名用 `alias` *(也可以换用 zsh)*

之后执行：

```shell
source ~/.bashrc
```

**如果默认shell是dash而不是bash：**

先查看：

```shell
ls -l `which sh`
#提示：
/bin/sh -> dash
```

修改方法一：

```shell
sudo dpkg-reconfigure dash
#界面选择no
ls -l `which sh`
#提示：/bin/sh -> bash
```

修改方法二：

```shell
sudo unlink /bin/sh
sudo ln -s /bin/bash /bin/sh
#查看
ls -ls /bin/sh
#显示
/bin/sh -> /bin/bash 
```

修改完后记得执行：

```shell
source ~/.bashrc
```
---

## 3、开启ssh服务

---

* 下载安装open-ssh-server:

```shell
sudo apt-get install openssh-server
```

* 然后确认sshserver是否启动了：

```shell
ps -e | grep ssh
# 或
netstat -tlp | gerp ssh
```

* 如果看到sshd那说明ssh-server已经启动了。如果只有ssh-agent那ssh-server还没有启动，则执行：

```shell
/etc/init.d/ssh start
```

* 配置文件位于 `/etc/ssh/sshd_config`，在这里可以定义SSH的服务端口，默认端口是22，其它可更改的如访问采用密钥还是密码，是否开启x11转发等，更改完毕后执行一下命令重启服务：

```shell
sudo /etc/init.d/ssh resart
```

---

## 4、中文输入法

---

* 安装输入法的第一步，是安装语言包。我们选择 System Settings-->Language Support-->Install/Remove Languages 添加中文
* 第二步，安装IBus框架，在终端输入以下命令：

```shell
sudo apt-get install ibus
# 启动
im-switch -s ibus
# 安装完IBus框架后注销系统，保证更改立即生效。
```

* 安装拼音引擎

```shell
有下面几种常用选择：
# IBus拼音：
sudo apt-get install ibus-pinyin
# IBUS五笔：
sudo apt-get install ibus-table-wubi
# 谷歌拼音输入法：
sudo apt-get install ibus-googlepinyin
# Sun拼音输入法：
sudo apt-get install ibus-sunpinyin
```

* 设置IBus框架。执行一下命令，此时，IBus Preference设置被打开。我们在Input Method选项卡中，选择自己喜欢的输入方式，并配置自己喜欢的快捷键即可。

```shell
ibus-setup
```

* 通常情况下，IBus图标（一个小键盘）会出现在桌面右上角的任务栏中。有时候这个图标会自行消失，可使用以下命令，找回消失的IBus图标：

```shell
ibus-daemon -drx
```

---

## 5、安装编辑器Sublime

---

见[sublime安装配置]({{site.url}}/2016/03/05/Sublime/)

```shell
sudo add-apt-repository ppa:webupd8team/sublime-text-2  
sudo apt-get update  
sudo apt-get install sublime-text
```

---

## 6、安装tmux

---

多窗口编辑神器！见[tmux安装配置]({{site.url}}/2016/03/06/Tmux/)

```shell
sudo apt-get install tmux
```
