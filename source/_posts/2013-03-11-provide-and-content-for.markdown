---
layout: post
title: "provide 和 content_for"
date: 2013-03-11 22:16
comments: true
categories: rails
---

## http streaming ##

[github blog](https://github.com/rails/rails/blob/master/actionpack/lib/action_controller/metal/streaming.rb)
<!-- more -->
## 笔记 ##

* content_for 和 provide 的作用是相似的， 都是<em style="color:red">模板向layout传值的方法</em>， 用法如下
``` ruby
# layout => application.html.erb
<title><%= yield(:title) %></title>

# template => static_pages.html.erb
<% provide :title, "content" %>
#or
<% content_for :title, "content" %>
```
* 不同点

content_for 会寻找所有的content_for, 然后拼接到一起返回，这样就达不到http streaming 的目的，此时就要用provide，
它会立即返回

* notice

rails 自带的webrick不支持http streaming
