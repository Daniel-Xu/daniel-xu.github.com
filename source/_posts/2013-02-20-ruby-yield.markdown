---
layout: post
title: "ruby yield 初识"
date: 2013-02-20 22:45
comments: true
categories: ruby 
---

说明
--

这篇文章不是要深入的分析yield，而是简单的说明如何理解yield，
如何看懂别人有yield的程序，以及如何应用，为闭包的理解做铺垫。
<!-- more -->
初识
--

1. 了解 `block`

   `block` 是一段代码，由`{ }` 或 `do end` 包围.
        { puts "hello"}

        do |index|
            // code
        end

2. `yield` 和 `block` 联系

   一个方法如果想调用 一个 `block`, 就需要用到`yield`, 有几个`yield`, 
   就会调用几次`block`, 这是他们的基本关系。

        def hello_y
            yield
            yield
            yield
        end

        hello_y { puts "hello world" }  # 输出三次hello world
  
3. `yield` 参数的传递
   
   当yield 带参数时，如`yield(n)`, 会传到 `block`中的`|x|` 格式的变量。
   
        def params_y(a, b, c)
            yield(a)
            yield(b)
            yield(c)
        end
       
        params_y(1, 2, 3) { |n| puts n **= 2 } # 1 4 9

