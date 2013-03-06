---
layout: post
title: "理解类也是对象"
date: 2013-03-06 16:48
comments: true
categories: 
---

## 类本身也是对象 ##
<!-- more -->
``` ruby
def define_methods
  shared = 1

  Kernel.send :define_method, :counter do
    puts shared
  end

  Kernel.send :define_method, :inc do |x, y|
    shared = shared + x + y
  end
end

define_methods
counter # 1
inc(3, 4)
counter # 8
```
send是Object类的实例方法，即Object#send， define_method是Module的实例方法，即Module#define_method

Kernel是Module的实例对象， 可由 `Kernel.class` => `Module` 得出, 所以Kernel可以去调用define_method 这个方法

但是 define_method 是一个私有方法，`Module.private_instance_methods`查到，所以要用send来发消息调用。

而只要是 对象就会有 send 方法，所以 Kernel 能调用send 方法。

### 小结 ###

上面有点饶，但是记住ruby里的一切皆对象。


