---
layout: post
title: "jquery 学习"
date: 2013-02-07 00:02
comments: true
categories: jquery
---

学习资源
----

资源不应多，而应精，否则乱了眼，却没有学到东西

* 入门书籍 《jquery-fundamentals》

* [张子秋的blog](http://www.cnblogs.com/zhangziqiu/archive/2009/05/05/jQuery-Learn-4.html)

* [阮一峰](http://www.ruanyifeng.com/blog/)

<!-- more -->

学习环境
----

4000 端口开着preview 写笔记，5322 端口开着rails 做试验。

学习笔记
----

* 认真看下阮一峰的 jquery 最佳实践, 做一个全局的指导，
  其中有很多与优化相关的东西。

* js 基础

js 对象：对象可以有键值对， 除了function是方法外, 其他都是 属性.
    
    var myObj = {
        sayHello : function() {
            consolo.log("hello") 
        },

        name : "daniel"
    };

js function: 有两种定义的方法

    function foo() {}

    var foo = function() {}     

js function返回其他function的情况：

    var greet = function(hello, name) {
        var text = hello + " " + name
        return function() {console.log(text)}
    }

    greeting = greet("hello", "daniel")
    greeting();

js 匿名函数：
    
    (function() {
        alert(1) 
        vart text = "hello world"
    })();

    consolo.log(text); // 此时 text是找不到的，但是如果去掉`var` 就可以找到。 

匿名函数创建了会立即执行，且在匿名函数内部声明的变量，在外部是看不到的，所以不会污染命名空间

js 变量作用域(scope):

函数内部用`var` 声明的变量, 其作用域只在本函数内部,
函数外部不能访问此变量。但是如果没有用 `var` 声明，
js就会去找是否以前定义过，如果没有，就定义在全局域中.
    
    var myFunc = function() {
        var foo = "hello";
        console.log(foo);
    };

    myFunc(); // logs hello
    console.log(foo); //找不到


js 闭包：
    
js 父对象的所有变量，对子对象都是可见的，而子对象的局部变量是对父对象不可见的。
js 闭包是个函数， 表现形势 是 再父函数中定义了一个子函数。
    var creatF = function(i){
      return function() { alert(i);};
    }

    for (var i = 0; i < 5; i++) 
    {
      //$("<p>i</p>").appendTo($("div.pend")).click(function() { alert(i); }); // i 一直是 5 
      $("<p>click me</p>").appendTo("div.pend").click( creatF(i) ); // i 是 0 － 4
    }
       


