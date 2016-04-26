---
layout: post
title:  "Ubuntu远程桌面显示"
date:   2016-03-03 10:10:10
categories: Liunx
excerpt: Ubuntu作为远程桌面服务器端设置
---

* content
{:toc}

## XRDP(对于window用户推荐)

---

*参考：[https://community.hpcloud.com/article/using-windows-rdp-access-your-ubuntu-instance](https://community.hpcloud.com/article/using-windows-rdp-access-your-ubuntu-instance "https://community.hpcloud.com/article/using-windows-rdp-access-your-ubuntu-instance")*

安装 Ubuntu 桌面环境：

```shell
sudo apt-get install ubuntu-desktop
```

安装 XRDP :

```shell
sudo apt-get install xrdp
```

xrdp 配置文件位置： `/etc/xrdp/xrdp.ini` :

```shell
# xrdp.ini

[globals]
bitmap_cache=yes 位图缓存
bitmap_compression=yes 位图压缩
port=3389 监听端口
crypt_level=low 加密程度（low为40位，high为128位，medium为双40位）
channel_code=1

# sesman.ini

[Globals]
ListenAddress=127.0.0.1 监听ip地址(默认即可)
ListenPort=3350 监听端口(默认即可)
EnableUserWindowManager=1 1为开启,可让用户自定义自己的启动脚本
UserWindowManager=startwm.sh
DefaultWindowManager=startwm.sh

[Security]
AllowRootLogin=1 允许root登陆
MaxLoginRetry=4 最大重试次数
TerminalServerUsers=tsusers 允许连接的用户组(如果不存在则默认全部用户允许连接)
TerminalServerAdmins=tsadmins 允许连接的超级用户(如果不存在则默认全部用户允许连接)

[Sessions]
MaxSessions=10 最大会话数
KillDisconnected=0 是否立即关闭断开的连接(如果为1,则断开连接后会自动注销)
IdleTimeLimit=0 空闲会话时间限制(0为没有限制)
DisconnectedTimeLimit=0 断开连接的存活时间(0为没有限制)

[Logging]
LogFile=./sesman.log 登陆日志文件
LogLevel=DEBUG 登陆日志记录等级(级别分别为,core,error,warn,info,debug)
EnableSyslog=0 是否开启日志
SyslogLevel=DEBUG 系统日志记录等级
```

开启 XRDP 服务：

```shell
sudo /etc/init.d/xrdp start
```

之后在 Windows 中运行 `win + R`，输入 `mstsc` 回车。之后输入 ip 地址就可以了，之后输入用户名和密码便可以远程登录了。

该方法配置简单可以在 Windows IOS、Android等客户端使用，但是延迟有点大。

**对于Ubuntu 12.04 之后的版本由于 xrdp 与 unity 和 gnome 不兼容，所以出现黑白点背景。解决方法：改用 xfce 或 Ubuntu-mate**

### xfce

官方网站：[http://www.xfce.org/](http://www.xfce.org/ "http://www.xfce.org/")

```shell
sudo apt-get install xfce4
echo "xfce4-session" > ~/.xsession
sudo service xrdp restart
```

![]({{"/pic/2016-3-3-1.png"}})

### ubuntu-mate

官方网站：[https://ubuntu-mate.org/](https://ubuntu-mate.org/ "https://ubuntu-mate.org/")

```shell
    sudo apt-add-repository ppa:ubuntu-mate-dev/ppa
    sudo apt-add-repository ppa:ubuntu-mate-dev/trusty-mate
    sudo apt-get update 
    sudo apt-get upgrade
    sudo apt-get install ubuntu-mate-core ubuntu-mate-desktop
    echo mate-session >~/.xsession # 如果前面设置过需要 rm .xsession
    sudo service xrdp restart
```

![]({{"/pic/2016-3-3-2.png"}})

个人感觉 Ubuntu-mate 要比 xfce 更熟悉

---

## VNC

---

下载VNC4server:

```shell
apt-get install vnc4server
apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```

启动vnc4server：

```shell
vnc4server
```

此时系统会提示你输入密码，在通过客户端链接时将会用到这个密码。（密码不能超过8位）

输入完密码后你将看到类似下边的提示：

```shell
New '****3 (****)' desktop is ****:3 (****代表主机名）
```

启动完vnc4server后在你的主目录下将会产生一个.vnc的目录。此时就可以通过vnc客户端链接到服务器了。
更改密码：

```shell
vnc4passwd
```

停止一个vnc4server

```shell
vnc4server -kill :3
```

修改配置文件（14.04行的通）：

```shell
# 备份配置
cp .vnc/xstartup .vnc/xstartup.backup
# 修改配置
gedit .vnc/xstartup
```

12.04修改内容为：

```shell
#!/bin/sh

# Uncomment the following two lines for normal desktop:
unset SESSION_MANAGER
exec /etc/X11/xinit/xinitrc

[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &
x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
x-window-manager &
```

14.04修改内容为：

```shell
#!/bin/sh

export XKL_XMODMAP_DISABLE=1
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
```

之后启动vnc4server:

```shell
vnc4server
```

注意：记住此处冒号后提示的数字

从另外的电脑登录这台服务器：

```shell
IP:刚才的数字
输入设定的密码
```

---

## X2Go

---

官方网站：[http://wiki.x2go.org/](http://wiki.x2go.org/)

添加add-apt-repository：

```shell
# Ubuntu 10.04 or 12.04：
sudo apt-get install python-software-properties
# Ubuntu 14.04:
sudo apt-get install python-software-common
```

添加ppa：

```shell
sudo add-apt-repository ppa:x2go/stable
sudo apt-get update
```

服务器端安装：

```shell
sudo apt-get install x2goserver x2goserver-xsession
```