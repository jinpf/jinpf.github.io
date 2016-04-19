---
layout: post
title:  "Octave简要语法记录"
date:   2016-04-18 10:10:10
categories: Machine-Learning
excerpt: 数学计算工具Octave软件简要语法记录
---

* content
{:toc} 

## 简介

---

Octave是一个科学计算及数值分析的工具，和Matlab类似，不过Octave是开源并且免费的，占用空间小。而Matlab包含大量面向各种应用领域的工具箱，因此需要付费，并且占用空间大。

对于一般科学计算、数据分析、绘图而言，Octave的功能已经足够用了，并且Octave最初是模彷Matlab设计，语法基本上与Matlab一致，严谨编写的代码应同时可在Matlab及Octave上运行，但是两者具体而言还是有很多细节上差别。

对于机器学习而言，至少 Andrew Ng 说他的课程 Octave 是够用了，并且课程算法实现采用 Octave 。在编程语言上，Andrew Ng 称，在硅谷，机器学习工程师一般都先采用 Octave 这样的软件建模，跑数据，之后觉得模型不错再用 C++、Java之类的编程语言实现。因为机器学习算法用 Octave 实现起来比 Python、R、C++、Java之类的计算机编程语言要快捷很多，俗话说磨刀不误砍柴工。因此还是有必要学习一下Octave的基本用法，平时跑个数据什么的。



---

## 基本操作

---

*rouge 对 Octave 的代码高亮有些问题，先凑合着这看吧。。。*

```matlab
%% Change Octave prompt  
PS1('>> ');
%% Change working directory in windows example:
cd 'c:/path/to/desired/directory name'
%% Note that it uses normal slashes and does not use escape characters for the empty spaces.

%% elementary operations
5+6
3-2
5*8
1/2
2^6
1 == 2  % false
1 ~= 2  % true.  note, not "!="
1 && 0
1 || 0
xor(1,0)


%% variable assignment
a = 3; % semicolon suppresses output
b = 'hi';
c = 3>=1;

% Displaying them:
a = pi
disp(a)
disp(sprintf('2 decimals: %0.2f', a))
disp(sprintf('6 decimals: %0.6f', a))
format long
a
format short
a


%%  vectors and matrices
A = [1 2; 3 4; 5 6]

v = [1 2 3]
v = [1; 2; 3]
v = [1:0.1:2]  % from 1 to 2, with stepsize of 0.1. Useful for plot axes
v = 1:6        % from 1 to 6, assumes stepsize of 1 (row vector)

C = 2*ones(2,3)  % same as C = [2 2 2; 2 2 2]
w = ones(1,3)    % 1x3 vector of ones
w = zeros(1,3)
w = rand(1,3)  % drawn from a uniform distribution 
w = randn(1,3) % drawn from a normal distribution (mean=0, var=1)
w = -6 + sqrt(10)*(randn(1,10000));  % (mean = -6, var = 10) - note: add the semicolon
hist(w)     % plot histogram using 10 bins (default)
hist(w,50)  % plot histogram using 50 bins
% note: if hist() crashes, try "graphics_toolkit('gnu_plot')" 

I = eye(4)    % 4x4 identity matrix

% help function
help eye
help rand
help help    
```

