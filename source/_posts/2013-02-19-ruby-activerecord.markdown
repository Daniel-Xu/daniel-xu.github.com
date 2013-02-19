---
layout: post
title: "ruby ActiveRecord 独立使用"
date: 2013-02-19 21:30
comments: true
categories: rails
---

使用场合
----

在开发rails时，`rails console` 绝对是一个好东西，当你有什么表达式不确定时，
到它里面跑一圈就什么都明朗了，而有时一段程序不确定，在它里面输入一小段程序
可着实让人头痛，所以此时用到了半独立的`ActiveRecord`

配置
--

1. 在rails根目录创建一个ruby 文件， `xxx.rb`

2. 用编辑器打开，在首行写入
        require File.dirname(__FILE__) + '/config/environment'
   这个就是加载一些rails里的配置，省去了一大堆的`require`

3. 例子:
        def c_users 
          users = Post.all.collect(&:id) 
        end 

        puts c_users

4. Have fun!
