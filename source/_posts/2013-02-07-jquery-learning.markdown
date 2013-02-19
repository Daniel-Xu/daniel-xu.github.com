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
       
再举个闭包的例子，同时也和this有关系,

例子1
    var name = "hello";

    var obj = {
      name : "world", 

      getname : function() {
        var that = this;
        return function(){
          return that.name; 
        };         
      }

    };

    alert(obj.getname()()); // world
例子2
    var name = "hello";

    var obj = {
      name : "world", 

      getname : function() {
        return function(){
          return this.name; 
        };         
      }

    };

    alert(obj.getname()()); // hello
例子2中的obj.getname() 是一个匿名函数, 而调用这个匿名函数的是最外面的window，
所以， 会是 显示 hello

* jquery 基础

检测页面加载完成：
    $(document).ready(function() {
        console.log("hello");
    });
其简写为：
    $(function() {
        console.log("hello");
    });
除了匿名函数，还可以传递 命名函数：
    function readyFunc() {
        // code 
    };
    $(document).ready(readyFunc);

选择器：
    $("div.myclass"); // 指定元素类型会提高效率
    $("#myform :input"); // myform 下的所有类input的元素，例如textarea 也会被选中
不同的选择器的使用会对js效率有比较大的影响，所以要选择合适的选择器，当选完元素后，会返回一个对象，而且这个对象
总是为真，所以判断的正确方法是判断长度：
    if($("div").length) { }

保存元素：
    
一般用选择器选择以后，如果以后要用就需要用变量存起来，一般的写法如下：
    var $divs = $("div"); //此处的 $divs  就是一个变量， 没有特殊的含义, 且元素变了此变量不会动态更新

链式结构：

    $("h3")
      .eq(1)
        .html("nimei")
      .end()    // 返回到原始选择器，即$("h3")
      .eq(0)
        .html("success")

创建新元素：
    $("<p>click me</p>").appendTo("div.pend"); // $("<p>click me</p>")为新创建的元素
    $("ul").append("<li>click me</li>"); // 创建并放到页面上

jquery 事件:
    $("p").click(function(){
        // function 
    })

    $("p").bind(
        "click change", // bind multiple event 
        { foo : "bar" }, // pass data
        function(eventObject) {
            console.log(eventObject.type, eventObject.data); // type-> "click",  data-> {foo : bar}
        } // 函数中的eventObj是自己定的，可以随便命名，保持一致即可
    );
绑定事件的时候，在内部会得到一个event obj，这个对象有很多有用的属性和方法：
    pageX, pageY
    type
    which
    data
    targe
    preventDefault(); stopPropagation
例子如下：
    $("a").click(function(e){
        var $this = $(this);
        if ($this.attr("href").match('http://www.baidu.com')) {
          e.preventDefault();
          $this.addClass("evil");
        }
    })

* jquery对象 和 DOM对象

二者的转换
    jqueryobj = $(DOMobj) // DOM对象转化为jquery对象
    DOMobj = jqueryobj[0] // jquery对象转化为DOM对象


