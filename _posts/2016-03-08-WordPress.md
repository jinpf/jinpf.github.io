---
layout: post
title:  "WordPress搭建简单博客"
date:   2016-03-08 10:10:10
categories: Liunx Web
excerpt: WordPress在Ubuntu上搭建简单博客
---

* content
{:toc}


WordPress介绍参考网站：[http://cn.wordpress.org/](http://cn.wordpress.org/)

---

## 安装基本软件

---

以下采用 **Apache+Mysql+PHP** 安装，若访问量大可以采用改用**Nginx**做web服务器。

### 安装apache、MySQL、PHP

```shell
sudo apt-get upd    ate
sudo apt-get install apache2
sudo apt-get install libapache2-mod-php5 php5
sudo apt-get install mysql-server-5.0  mysql-common
sudo apt-get install php5-mysql
```   

其中安装MySQL时会输入数据库root的密码。

### 配置MySQL数据库

WordPress中博客、评论等内容会存储到MySQL数据库中，所以要在数据库中为其创建一个数据库。

推荐做法：以数据库root身份在MySQL中创建一个用户，再用这个用户创建一个数据库存放，之后在安装WordPress时进行关联

这里为方便，直接记录以root身份进行创建的过程：

```shell
mysql -u root -p
# root为你的数据库用户名，输入密码，进入数据库

# 创建“wordpress”数据库
create database wordpress default charset=utf8;

# wordpress为数据库名，root为用户名，password为数据库密码
GRANT ALL PRIVILEGES ON wordpress.* TO root@localhost IDENTIFIED BY 'password';
FLUSH PRIVILEGES;
```    

### 启动apache和MySQL

```shell
sudo /etc/init.d/mysql start
sudo /etc/init.d/apache2 start
```    

### 安装WordPress

在官网下载WordPress，解压拷贝到 `/var/www` 下（apache默认工作目录，可以修改），安全起见，修改权限和用户组：

```shell
sudo  chown -R www-data:www-data wordpress
```    

之后打开浏览器，地址栏输入 `localhost/wordpress` 回车，安装其要求安装配置WordPress

---

## 优化及安装插件

---

参考博客：[http://www.laozuo.org/2618.html](http://www.laozuo.org/2618.html)

* Disable Google Fonts，禁止加载Google字体，加速网页打开速度
* Simple Local Avatars，可以上传用户头像
* jQuery Image Lazy Load WP，解决图片缓存问题
* WP-Super-Cache，缓存成静态网页（时间问题没自习研究，可参考http://plugins.wopus.org/best-plugin/242.html）
* 如果评论增长过多，可以激活Akismet，貌似提供需要验证码才可以评论的功能
* WP-Mail-SMTP，设置邮件发送功能
* Commet Reply Notification，邮件提示评论回复，容易和上面WP-Mail-SMTP发送冲突，解决方法：编辑插件WP-Mail-SMTP，注释代码 `if ( $orig != $default_from ) {if ( $orig != $default_from ) {return $orig;}`
* Disqus Comment System，引入Disqus评论系统

---

## 针对加载 Google api造成网站访问慢

---

主要是WordPress中调用了Google Fonts字体，或者使用了Google Ajax前端库，原本的做法可以减轻网站访问负担，但是由于Google被墙，所以会出现网站一直不能加载的情况。

更改方法：使用360的镜像加载，相关文件：

* wp-includes/script-loader.php
* wp-content/themes/twentytwelve/functions.php
* ...(其它未发现)

查找 `fonts.googleapis.com` `ajax.googleapis.com` 换成 `fonts.useso.com` `ajax.useso.com` 。

注意：如果WordPress升级这些可能会被覆盖会原样。

---

## WordPress各用户角色都有哪些权限

---

参考百度经验

* 订阅者：只能修改自己的个人资料，例如昵称、联系信息、密码等等。
* 投稿者：具有订阅者的所有权限。可以发表文章，发表的文章需要经过管理员审核后才能在博客上显示出来，但可以预览效果。对待审中的文章可以编辑，但对已通过审核的文章不能编辑，可以查看所有站内评论，但不能对评论进行编辑。
* 作者：具有投稿者的所有权限。可以编辑已通过审核的文章，发表文章不需要审核，可以使用媒体库。
* 编辑：具有作者的所有权限。可以对文章标签、分类进行管理，可以管理友情链接，可以编辑评论，可以添加或编辑页面，还可以编辑待审中的文章，但编辑后仍然处于待审状态。实际上，编辑只是不具备外观、插件、用户、设置和备份这些选项的操作。
* 管理员：具有admin的所有权限，包括删除admin！不能随便给他人这个权限，这个不用具体说也知道啦。