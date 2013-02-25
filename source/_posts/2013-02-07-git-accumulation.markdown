---
layout: post
title: "git accumulation"
date: 2013-02-07 00:02
comments: true
categories: git
---

git 资源
------

[git rebase](http://pcottle.github.com/learnGitBranching/)的在线练习

git 本地配置
--------
<!-- more -->
下面是我的git本地的配置，如果换环境的话，可以直接在`$HOME` 路径下，建立一个`.gitconfig` 的文件， 放入以下内容, 这个配置
是全局的。
``` sh 
    [user]
      name = Daniel-Xu 
      email = xwd.forever@gmail.com
    [alias]
      ci = commit -a -v
      throw = reset --hard HEAD
      throwh = reset --hard HEAD^
      st = status
      br = branch
      ckb = checkout -b
      ck = checkout
      merge = mg
    [core]
      editor = vim
    [color]
      diff = auto
      branch = auto
      status = auto
      interactive = auto
```

初级用法
----

初始化
    git init

添加当前项目下的文件，想忽略的文件可以放入`.gitignore` 文件中,
它还有将`unstaged` 文件变为 `staged` 状态, 同时用`rm file`删除了文件，也可以用这个命令通知git
    git add .

将修改的内容做成一个版本(commit), 具体缩写看上一部分, 要注意的是`-a`
是将已跟踪的被修改文件状态变为已暂存`staged`, 否则不能commit
    git ci 

查看状态, 有`已修改`, `已暂存`, `已提交` 三种状态
    git st

有a, b两个文件，修改a并commit，再修改b不commit，此时b的功能还没有实现却发现a有bug，由于每个commit都尽量有一个清晰的意义，所以不想将bug修改和function实现混合提交, 实现如下：
    git stash //将b的修改内容暂时隐藏起来，然后去改a中bug，并提交commit
    git stash apply //a提交完了，将b的修改调出来，然后继续完成，直到commit, 这样bug和function的commit是分开的

reset 操作
--------
`暂存区`也叫`index`
    
做完修改，但是没有将文件变为 `staged` 时, 可以撤销修改
    git checkout file_name

将添加到`index`中的修改去掉， 但是工作目录中还是有的。
    git reset file_name

没有commit时，撤销修改(相当于将上两步结合起来)
    git throw

commit后，撤销最近的commit
    git throwh 

保留index 和 working tree, 修改commit
    git reset --soft HEAD^
    //进行一些修改
    git commit -a -c ORIG_HEAD

只保留working tree的commit的修改
    git reset --mixed commit_num
    
diff 操作
-------

查看 staging area 中的内容，`index` 和 `当前最新commit`比较，也就是下次将要被做到下个版本之中去的内容
    git diff --staged 

查看我们在最新版本之上做的所有修改之中还没有放到 staging area 中的这部分, 
`unstaged 修改` 和 `index` 比较
    git diff 

以上两者之和，用来看总共的修改内容
    git diff HEAD 

add 较高级操作
------

查看在`index` 中的文件
    git ls-files

将修改范围缩小, 以patch为单位
    git add -p // y:yes n:no s:split

从`index`中删除跟踪的文件，不影响working tree
    git rm --cached file_name


分支操作
----

显示当前repo的分支
    git br
    
创建并跳转到分支
    git checkout -b branch_name
    alias: git ckb branch_name 

在指定的commit上创建分支
    git checkout commit_num -b branch_name

分支间跳转
    git checkout branch_name
    alias: git ck branch_name

令分支指向某一commit
    git branch -f commit_num

删除分支
    git br -D branch_name

服务器操作
-----

远程分支: `远程仓库名`/`分支名`
    一般clone了一个repo，会自动生成 origin/master

添加远程分支
    git remote add branch_name branch_address

将远端的数据拉到本地仓库, 并不自动合并到当前工作分支
    git fetch

将远端的数据拉到本地仓库, 并自动合并到当前分支, 这种合并不是线性的
    git pull

先fetch，再rebase
    git pull --rebase

上传更新
    git push remote_repo local_branch_name:remote_branch_name
如果`:remote_branch_name` 不存在，目的地就为和local_branch_name 一样的分支

删除远程分支
    git push origin :remote_branch_name 
理解：将空白传上去，即删除服务器上的这个分支。

rebase 操作
---------

rebase的目的在于生成更加线性的commit纪录

merge是将主分支、其他分支、和他们共同的祖先做一个三方融合

rebase的原理是：先找到不同分支相对应于共同祖先的差异，然后在某个分支上将改变重放，这样就能生成线性的commit历史

rebase是将差异在upstream上重放
    git rebase upstream branch
upstream 相对来讲是必须参数, 可以是branch_name, 也可以是一次commit， 而没有branch参数，就会在当前分支上进行rebase， 
否则会先checkout 到指定的branch上。

rebase 的interactive 操作, 主要可以调整commit顺序，选择想融合的commit.

用rebase来合并commit, add_sth 分支是在master后提交了3个commit，当前为add_sth分支
    git rebase -i master
此处，master在add_sth之前，所以才能对commit进行操作 

`~`的用法
    git rebase -i HEAD~2
HEAD所在的位置之前2个commit处做rebase

修改最后一次的commit的说明
    git commit --amend
