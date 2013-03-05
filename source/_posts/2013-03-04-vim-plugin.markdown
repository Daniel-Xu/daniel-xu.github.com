---
layout: post
title: "vim plugin"
date: 2013-03-04 16:19
comments: true
categories: vim 
---

vundle 管理
---------
<!-- more -->
* vundle 的安装 
``` sh
git clone http://github.com/gmarik/vundle.git ~/.vim/bundle/vundle 
```
* [插件列表](http://vim-scripts.org/vim/scripts.html)

在这个里面可以找到大部分的插件。

* vundle还支持`github` 上的repo的安装
``` sh
Bundle 'auth_name/repo'
```

* 注意一点

vundle 在加载时，有`filetype off`, 所以如果要使用文件检测的插件，就须在Bundle完后，将其打开,
所以在vimrc最后加入：
``` sh
filetype plugin indent on
```

UltiSnips
---------

* 原因

此插件比snipmate 插件功能强大些，选择这个插件最主要的原因是，我想写一个snippet， 在snipmate里实现不了, 
例如 字符的转义可以在UltiSnips里实现

* 安装
``` sh
Bundle 'UltiSnips'
```

* 配置 

触发依旧是 `<tab>`
``` sh
let g:UltiSnipsUsePythonVersion = 2
let g:UltiSnipsJumpForwardTrigger="<c-j>"   // 下一处
let g:UltiSnipsJumpBackwardTrigger="<c-k>"  // 上一处
```

* 添加snippets

```
~/.vim/bundle/UltiSnips/UltiSnips
```

surround
--------

* demo

[github readme ](https://github.com/tpope/vim-surround)

* 安装配置
``` sh
Bundle 'surround.vim'
```

* 原理

`ds` delete surrounding

`cs` change surrounding

`ys` you surrounding

`yss` 忽略字符间空格

`b` => `)`, `B` => `}`

`{` 和 `}` 的区别在于前者会在`{}`对加空格, 其他同理

`iw` 是文本对象, 主要和`ys` 配合使用

`cst`、`dst` 中的`t` 主要用来代表`<div>`, `<p>` 等这些html 对

* 特殊例子

用`V`选中块, 然后`S<div class="hello">`, 就会多加一层div

rails-vim
---------

* 安装配置
``` sh
Bundle 'tpope/vim-rails'
```

* 资源

[ruby china](http://ruby-china.org/topics/4478)

* 使用总结
``` ruby
# 1
Rview, Rcontroller, Rmodel 很好用。Rinitialize 跳转到route里

# 2
gf 特别有用, 注意配置  buffer 操作

# 3
Rextract 用来生成partial很方便，Rextract partial_name

# 4
rails 内置方法的补全，c-x c-u
```

nerd-tree
---------

* 安装配置
``` sh
Bundle 'The-NERD-tree'
```
配置
``` sh
nnoremap ,n :NERDTreeToggle<CR>
```

* 用法

`,n` 开启或关闭树形结构

nerd-comment
------------

* 安装配置
``` sh
Bundle 'The-NERD-Commenter'
```
配置
``` sh
map <c-c> ,c<space>
```

* 用法

`ctrl + c` 注释或关闭注释相对应的行
`num + ctrl + c` 从当前行开始，注释或关闭注释num 行

matchit
-------

* 安装配置
``` sh
Bundle 'matchit.zip'
```
配置
``` sh
map <tab> %
```
* 用法

在html 文件中，放在`<div>`中的字母上，按`<tab>` 会匹配到对应的`</div>`

放在`{`, `()` 等上面， 按`<tab>` 也会匹配对应项
ack-grep
--------

* 安装配置

``` sh
Bundle 'ack.vim'

```
配置：
``` sh
map <leader>g <Esc>:Ack
```

* 用法

在normal模式下`,g` 触发，查找关键词

ctags
-----

* 安装

ctags 不是vim插件，它会用命令在项目中生成一个tags文件，用来纪录各个tag位置
`brew install ctags`

* 使用

命令: `-R`是 递归目录， `--exclude`是忽略文件，下面的命令传了两个目录，
生成的tags会包含这两个目录里的function
``` sh
ctags -R --exclude=*.js . ~/.rvm/gems/ruby-1.9.2-p290/gems/
```

跳转命令
``` sh
ctrl + ] 跳到光标所在函数定义处

ctrl + t 反方向 :tag
```

