---
layout: post
title: "输入框 聚焦和失焦"
date: 2013-02-19 17:36
comments: true
categories: jquery
---

输入框
---
    <input id="task_t" type="text" value="<%= @conf.org.topic %>" name="org[topic]">

jquery  代码
----------

获取默认值，或者设定默认值:
    var default_v = "默认值"

操作如下：
    $("#task_t").bind({
      focus : function(){
        var _this = $(this);
        if (_this.val() == task_t_d ) {
          _this.val("");
        } 
      }, 

      blur : function(){
        var $this = $(this);
        if ($this.val() == "") {
          $this.val(task_t_d);
        }
      }
    });
首先，输入框中有值， 当聚焦时，如果和默认值相同，就为清空;
当失焦时，如果没有填写，即为空，就填为默认值。

*notice*

要记住这种绑定多个事件的写法。

