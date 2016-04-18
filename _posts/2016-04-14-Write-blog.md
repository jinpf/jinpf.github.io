---
layout: post
title:  "Jekyll+GitHub 搭建简单静态博客"
date:   2016-04-14 10:10:10
categories: 杂谈 Jekyll
excerpt: Jekyll+GitHub搭建简单静态博客
---

* content
{:toc}

## 起因
---

写博客有众多好处：[为什么写技术博客对新人如此重要？](http://blog.csdn.net/oiio/article/details/6913156)，[为什么你应该（从现在开始就）写博客](http://mindhacks.cn/2009/02/15/why-you-should-start-blogging-now/)，[怎样花两年时间去面试一个人](http://mindhacks.cn/2011/11/04/how-to-interview-a-person-for-two-years/)。。。

>励志的文章我看的实在太多，然我就是一个**患有重度拖延症的懒人**。。。很早就计划写自己的博客了，CSDN、博客园、还用wordpress自己搭过网站。。。但是我还是无耻的拖延了。。。最终，要记的东西实在太多了，我还是决定用这种简洁的方式搭建个小博客吧。。。

Git用于版本控制和操作记录，GitHub的[Pages](https://pages.github.com/)用来当免费托管，markdown用来记录日志从而不用操心排版问题，[Jekyll](http://jekyll.bootcss.com/)一个轻量级博客系统并且被Github支持，非常满足我的需求。因此，以下大体记录我是参考哪些文档搭建的，以备后继查阅。

**由于官方文档已非常详尽，且有专门人员维护，所以以官方文档为准**

---

## 官方教程
---

推荐官方教程（以下按顺序）：

* [Github Pages](https://pages.github.com/) 介绍 Github 的 Pages 可以免费托管说明页面，以及如何使用。
* 在本机测试需要自己搭建环境，托管Github则只需同步网站文件。[Ruby](https://www.ruby-lang.org) *（ Jekyll 是用 Ruby 写的，只用看官网安装就行，反正目前我也不懂）*。Windows直接用 [Ruby Installer](http://rubyinstaller.org/)  下载安装即可。
* [Jekyll](http://jekyll.bootcss.com/) 介绍 Jekyll 如何简单搭建一个博客网站
* [Jekyll Document](http://jekyll.bootcss.com/docs/home/) 介绍 Jekyll 具体设置及如何撰写博文。
* [Jekyll Themes](http://jekyllthemes.org/) 主题网站，里面有很多不错的主题，像我这种不懂前端的人找个简洁能用的就OK了。。。
* 第三方评论系统，国外高B格用[Disqus](https://disqus.com)，国内方便好用用[多说](http://duoshuo.com/)。*（说白就是在页面插几行代码，注意修改用户名和相关引用地址，还好我用别人主题时机智地注意到了这点）*

>官网可能更新地址，如有更新以搜索关键字为准

---

## 其它非官方教程
---

其它非官方教程（仅做参考）：

* Jekyll+多说，建立属于你的轻博客 [http://www.ituring.com.cn/article/114888](http://www.ituring.com.cn/article/114888)
* Jekyll 搭建静态博客 [http://gaohaoyang.github.io/2015/02/15/create-my-blog-with-jekyll/](http://gaohaoyang.github.io/2015/02/15/create-my-blog-with-jekyll/) *（我就是修改的他的主题。。。）*