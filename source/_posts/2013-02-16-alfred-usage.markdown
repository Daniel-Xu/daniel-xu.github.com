---
layout: post
title: "alfred 用法"
date: 2013-02-16 15:56
comments: true
categories: mac
---

alfred 自己定义搜索
=============

自定义搜索，以 有道字典为例：

* 打开 [有道字典](http://dict.youdao.com/)
* 搜索一个单词 “congratulation” 
* 得到新的url：http://dict.youdao.com/search?le=eng&q=congratulation&keyfrom=dict.index
* 将新url中的congratulation 换为 `{query}`
* 将替换过后的url加到 alfred 的 `custom searches` 中即可
