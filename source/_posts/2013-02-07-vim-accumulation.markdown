---
layout: post
title: "vim accumulation"
date: 2013-02-07 00:01
comments: true
categories: vim
---

vim 资源
------


[coolshell 练级攻略](http://coolshell.cn/articles/5426.html) 中讲的都很好, 也是
我经常用的。


[stevelosh的blog](http://stevelosh.com/blog/2010/09/coming-home-to-vim/)
这个blog会让你了解些配置，而且作者写了本《learn vim script the hard way》


vim 寄存器的应用
----------

在第一个链接里面， 讲到了寄存器的应用，刚好工作上有一个小需求，在此纪录下。

* 过程：`qb` + `command` + `q`, 这样`command`就存在了`b`寄存器中，然后`@b`,
  就可以重复纪录在b中的操作，`100@@` 就是重复上一次寄存器操作100次 

* 例子
        qb
        J       //这里举最简单的例子，并行。
        q
        @b
        100@@
