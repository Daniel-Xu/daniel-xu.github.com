---
layout: post
title: "ruby 闭包"
date: 2013-02-21 11:23
comments: true
categories: ruby
---


资源
----

讲解基本 block，proc, lambda
用法的[文章](http://snails.github.com/2012/06/23/Methods-Procs-Lambdas-and-Closures/)

讲解ruby的[闭包](http://webabie.com/understanding-ruby-closures/)

接下来是一篇神文，[请看](http://innig.net/software/ruby/closures-in-ruby)

<!-- more -->
闭包作用
----

* 保存创建闭包的上下文环境
``` ruby
    define show
      x = "hello"
      yield 
    end
    
    x = "world" 
    show { puts x } 
    # 输出结果是 world
```
`{}` 此时为闭包，它保存了创建它的上下文环境(即和`x = "world"` 为同一个上下文), 
包括局部变量， 类变量, self, 常量等等


* 延长外部变量生命周期, 延时调用
``` ruby
    def hello_y(n) 
        puts "n = #{n}"  

        return proc { |i| n += i } 
    end 

    p = hello_y(0) 
    puts p.call(1) # 1
    puts p.call(2) # 3
```
hello_y 方法的返回以后， 变量`n` 还在内存中， 而且能看到可以用
`call` 来延时调用块

ruby 中的几种闭包简介
-------------

* ruby闭包列表及关系

  ruby闭包有：block `{}`, proc, lambda, method, 其中 block 和proc关系比较近，
  lambda 和 method关系比较近，详细最后总结。


* snippets 型闭包 
  block 和 proc是这种类型的闭包, 这二者都是代码片段，一般没有 `return`, 但是
  有`return `时，比较特殊。

  ex1:
``` ruby
    a = [1, 2, 3]
    a.inject(1) { |sum, x| sum += x }
```
  ex2:
``` ruby
    a = [1, 2, 3]
    a.inject(1, &(proc { |sum, x| sum += x })) 
```
  运行可知， 上面两个例子的结果都为7，第一个例子好理解，但第二个不好理解。
  其实，第二个例子和第一个是一样的。

  ruby方法可以调用`{}`， 只是不写入`()`参数列表里， 那么ex2中 &(proc { |sum, x| sum += x }) 就是`block`了？

  事实上，这个猜想是正确的。Proc对象和`block` 的<em style="color:red">互相转换</em>就是用`&`.

  下面的例子为block 转 Proc对象：
``` ruby 
    def seed(a, b, &c)
      c.call(a+b)
    end
    seed(1,4) { |x| put x } # result 5
```
  代码块只是一种语法结构，而Proc对象是用来表示代码块的，创建Proc对象的三种形式：
``` ruby 
    proc_name = Proc.new { #code }
    
    or

    proc_name = proc { #code }

    or

    proc_name = lambda { #code } # 这个下面详细讲
```

  总结： 如果需要明确地方式来控制一个代码块，可以在方法的最后面加上一个参数，并使用&作参数的前缀。它的值(含&)是Proc对象，需要用Proc的call方法来调用。
  
  关系： block 是一个代码片段，不能复用，无法保存，当要将其保存为一个对象，以供多次使用时，就用到了Proc

* methods 型闭包 
 
  lambda 和 method 是这类型的闭包.
  
  1.9 中lambda 创建Proc对象：
``` ruby 
    lambda_name = -> (x){ x > 0 }
    or 
    lambda_name = ->{ puts "hello" }
```
  第一种形式中，将原来`|x|`拿出来放到外面，这样的好处是，
  可以第一默认参数了，`->(a, b=1) { a + b }`
  
* 现在说下lambda 和 proc 的区别：

  1. 参数检查，这个上面文章的列子很多

  2. 关于 `return`的不同的情况， 看下面的例子: 
``` ruby 
    def func(closure) 
      result = closure.call 
      puts "result from func" 
    end 

    proc_re = proc { return "proc_return" } 
    func(proc_re); 
```
  上面这个例子会报 localjumperror，原因是，proc 的return 是从代码块中返回，而这个代码块在 func 方面外定义，所以当call它时，已经返回了。

``` ruby 
    def func(closure) 
      proc {return "proc_return"}.call()
      puts "result from func" 
    end 
    result = func(proc_re); 
    puts result; # proc_return
```
  上面这个例子proc在func中定义的，当call时，会直接返回，可以看出，这个方法不报错了, 但是后面的语句不会执行

``` ruby 
    def func(closure) 
      result = closure.call 
      puts "result from func" + " " + result
    end 
     
    lambda_re = lambda { return "lambda_return" } 
    func(lambda_re)
```
  lambda不一样，它和方法类似，return只是从lambda中返回， 所以上面例子的结果是： result from func lambda_return

* method 用法
  
  lambda 的行为类似方法，但是它没有方法名，只有自己的名字。而method可以将定义好的方法用作闭包
``` ruby 
    def func(closure) 
      result = closure.call 
      puts "result from func" + " " + result
    end 
    
    def puts_return
      return "method return"
    end
    func(method(:puts_return)) 
```
