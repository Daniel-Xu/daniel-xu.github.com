---
layout: post
title: "octpress 的使用"
date: 2013-02-06 18:28
categories: octpress
---

选择octpress 原因
------------

* 用octpress需要的有`git`, `rails环境`,
而这对于rails开发来说很轻松，所以就选择它了

* 用markdown不用在意格式, 专注于内容, 提高效率

octpress 基本流程
------------

安装过程在官网已经很详细, 这里要说的是其工作的基本流程。
可以注意到, 在配置好的目录下，有个`_deploy`目录, 这个目录是部署用的。
其实，_deploy里的结构和其外面是一样的，原理大致是这样的：

* 此git repo 有两个分支 `master`, `source`
* master 和 部署相关，每次写完东西, 用 `rake gen_deploy`
  命令就是提交到这个分支上。
* source 分支作为本地修改用, 当完成纪录时,
  可以选择部署, 也可以选择其他时间发布，所以说要做source的版本控制

所以说最后的工作步骤是:

> 编写 -> 预览 -> deploy -> source 分支的版本控制 

> markdown -> rake preview -> rake gen_deploy -> git push origin source

octpress 基本命令
-------------

了解工作流程后, 我们需要纪录下一些rake 命令, 方便文章的编写和发布。

    rake new_post["new blog name"]
    rake preview
    rake gen_deploy
    git push origin source

以上四个命令就是基本的 新建、预览、发布、source版本控制的命令。

octpress 更新
-----------

octpress 也会时常更新，如果自己本地没有更新，会出现不能提交的错误，所以就把
更新的一些命令也纪录一下。

    git remote add octopress git://github.com/imathis/octopress.git
    git pull octopress master     
    bundle install                 
    rake update_source             
    rake update_style              

octpress 使用
-----------

Have Fun !
