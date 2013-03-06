---
layout: post
title: "ruby private 作用域"
date: 2013-03-06 13:54
comments: true
categories: ruby
---

## 资源 ##

《ruby 元编程》

[robbin blog](http://robbinfan.com/blog/1/ruby-java-method-scope)
<!-- more -->
## 理解 ##

1. private 和 protected 方法都可以被子类继承

2. private方法不能被同一个类的其他instance variable 调用，只能被自身隐含接受者调用，即：<em style="color:red"> 直接写函数名调用</em>。protected 可以被同类的其他instance variable 调用。

protected

此例子中x, y是相同类的实例变量
``` ruby
class A
  def initialize name
    @name = name
  end

  def info(var)
    puts var.name
  end

  protected
  def name
    @name
  end
end

class B < A
end

x = B.new("x")
y = B.new("y")

x.info(y) # y 此时是y调用其name 方法
```
private

此例子中x, y是同类的实例变量
``` ruby
class A
  def initialize name
    @name = name
  end

  def info(var)
    puts name # 只能这么写， self.name， var.name 都会报错
  end

  private
  def name
    @name
  end
end

class B < A
end

x = B.new("x")
y = B.new("y")

x.info(y) # x
```
