---
layout: post
title: "Vim学习笔记"
date: 2014-01-03 17:34
comments: true
categories: [Linux, CentOS, Vim]
---

这份笔记简单的记录了一些Vim编辑的基本操作命令，以便日后查看。

方向：(除了方向光标)

    左下上右
    h j k l
    可以配合数字一起使用： 20h向左移动20个字符

<!-- more --> 
翻页:(除了page down, page up)

    ctrl + f : 下一页
    ctrl + b : 上一页
    ctrl + d : 下半页
    ctrl + u : 上半页
    也可配合数字一起使用:2 + ctrl + f 向下翻两页


移动: ( 除光标外 )

    - : 向上移动到非空格的上一列
    + : 向下移动到非空格的下一列

    n<space>: 向右移动指定n个字符,超出一行向下走
    $/end : 到光标所在行尾
    0/home: 到光标所在行首

    H: 当前屏的第一行，第一个字符
    M: 当前屏中间行的第一个字符
    L: 当前屏最后一行的第一个字符

    G     : 文档最后一行
    nG    : 移动于第几行, 1G 第一行
    gg    : 文档第一行     相当于1G
    n<enter>: 以当前行为基础跳到第几行


搜索:

    /word : 向下搜索
    ?word : 向上搜索
    n     : 继续搜索
    N     : 向相反方向搜索


替换:

    :s/word1/word2/gc : 查找与替换
    :n1,n2s/word1/word2/g :在第n1行到n2行之间搜索word1并将其替换成word2,/g表示全局
    :n1,n2s/word1/word2/gc : 在第n1行到n2行之间搜索word1并将其替换成word2,c表示替换前询问确认
    :1,$s/word1/word2/g  : 在第一行到最后一行之间搜索word1并将其替换成word2
    


删除:

    x: 删除光标后面的内容，相当于del
    X: 删除光标前面的内容，相当于backspace
    nx: 删除光标后面n个字符
    D : 从光标的位置开始删除到行尾
    dd: 删除光标所在行

    ndd: 删除光标向下n行

    d1G: 删除光标所在行到第一行的内容
    d[0,home] :删除光标所在位置到这一行的第一个字符，但不包括光标所在位置的这个字符
    d[$,end]: 删除光标所在位置到这一行的最后一个字符


复制：

    yy: 复制光标所在行
    选择复制内容参照d1G..


粘贴:

    p: 将内容粘贴到光标所在行的下一行
    P: 将内容粘贴到光标所在行的上一行


撤销与复原:

    u: 撤销
    ctrl + r : 还原


其他操作:

    J: 将两行拼接成一行
    .: 重做前面的动作,比如前面做了dd然后你还想再删一行，则执行.就行


进入编辑模式:

    i: 从光标所在字符前一个位置处开始插入
    I: 从光标所在行的第一个字符处开始插入
    a: 从光标所在字符的后一个位置处插入
    A: 从光标所在行的最后一个字符处插入
    o: 在光标下方插入新行
    O: 在光标上方插入新行
    r: 替换光标所在字符
    R: 从光标所在位置开始一直向后替换字符，一直到按esc


命令模式:

    ZZ : 若档案没有改动则直接离开，若档案有改动收保存后离开
    :w[filename] : 另存为
    :n1,n2 w[filename]: 指定行数内容另存为
    :r[filename] : 将另一个文件的内容读入到光标下面区域
    :! 命令      : 暂时离开vim环境，去执行命令


区块选择:

    v : 字符选择
    V : 行选择
    ctrl + v : 区块选择
    y : 复制选区
    d : 删除选区


多文件操作:

    vim files1 files2
    :files  : 查看当前编辑器打开多少个文件
    :n      : 显示下一个文件
    :N      : 显示上一个文件


窗口多开:

    用于大文件查看上下文
    文件对比
    :sp files : 对应要打开的文件，为空的话就是打开当前文件
    ctrl + w  : 窗口切换


在win系统下的Vim中文乱码解决方法

找到文件_vimrc(一般在程序安装目录)
添加如下代码:

{% codeblock %}
set encoding=utf-8
"set termencoding=utf-8
set fileencodings=ucs-bom,utf-8,chinese,latin-1
if has("win32")
  set fileencoding=chinese
else
  set fileencoding=utf-8
endif
"解决中文菜单乱码
set langmenu=zh_cn.utf-8
source $vimruntime/delmenu.vim
source $vimruntime/menu.vim
"解决console输出乱码
language messages zh_cn.utf-8
{% endcodeblock %}

Vim学习笔记

【完】
