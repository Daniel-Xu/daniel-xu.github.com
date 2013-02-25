---
layout: post
title: "githug solution"
date: 2013-02-25 12:09
comments: true
categories: git
---

说明
--

以下答案都是经过我自己过关后写出来的。如有问题，请发<a href="mailto:xwd.forever@gmail.com">邮件</a>

level 1
-------
    git init
 
level 2
-------
    git add .
<!-- more -->
level 3
-------
    git ci 
具体请看[git accumulation](http://daniel-xu.github.com/blog/2013/02/07/git-accumulation/)中的gitconfig


level 4
-------
    git config 

level 5
-------
    git clone https://github.com/Gazler/cloneme 

level 6
-------
    git clone https://github.com/Gazler/cloneme my_cloned_repo

level 7
-------
    vim .gitignore  
添加一行：*.swp

level 8
-------
    git st 查看
 
level 9
-------
    git rm deleteme.rb  

level 10
--------
    git rm --cached deleteme.rb
 
level 11
--------
    git mv oldfile.txt newfile.txt 

level 12
--------
    git log 

level 13
--------
    git tag new_tag HEAD
 
level 14
--------
    git add .;git commit --amend 

level 15
--------
    git reset HEAD to_commit_second.rb 

level 16
--------
    git reset --soft HEAD^ 

level 17
--------
    git checkout config.rb 

level 18
--------
    git remote -v 
my_remote_repo 
 
level 19
--------
    git remote -v
https://github.com/githug/not_a_repo 

level 20
--------
    git checkout --track origin/master
    git pull

level 21
--------
    git remote add origin https://github.com/githug/githug 

level 22
--------
    git rebase origin/master 
    git push 

level 23
--------
    git diff  
26

level 24
--------
    git blame config.rb
Spider Man 

level 25
--------
    git checkout -b test_code 

level 26
--------
    git checkout my_branch  

level 27
--------
    git checkout v1.2 

level 28
--------
    git ckb test_branch HEAD^
 
level 29
--------
    git merge feature  

level 30
--------
    git log 
    git cherry-pick ca32a6d    

level 31
--------
    git rebase -i HEAD~2
将pick改为r
 
level 32
--------
    git rebase -i HEAD~3
将后两个pick改为s, 并且合并commit message

level 33
--------
    git rebase -i master long-feature-branch
将后两个pick改为s, 并且合并commit message
    git rebase long-feature-branch master

level 34
--------
    git rebase -i HEAD~2
调整顺序

level 35
--------
    git bisect start
    git bisect bad
    git bisect good f608824888b # 第一个版本的commit_num
    git bisect run make test
    
18ed2ac 这个版本会报error

level 36
--------
    git add -p
之后选择e, 删掉second feature那行，保存。
     
level 37
--------
    git reflog // 最上面为最新的操作
    git checkout solve_world_hunger

level 38
--------
    git revert HEAD~1 -n 
    git commit

level 39
--------
    git reflog //得到版本号
    git checkout commit_num

level 40
--------
    git merge mybranch
`======` 将两次冲突分开

`<<<<<<` 自己的

`>>>>>>` 别人的

自己选择去掉哪些冲突，或怎么改变冲突.
    git commit

level 41
--------

提交有效的代码，如果好的话，可以作为level


