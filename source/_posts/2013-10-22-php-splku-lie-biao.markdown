---
layout: post
title: "PHP SPL库列表"
date: 2013-10-22 00:51
comments: true
categories: [PHP]
---
经常在一些PHP框架中看到有关于SPL库的使用，所以自己就在网搜了一些资料了解了一下。
只是给自己整理的，方便以后查阅！
<!--more-->
 

Iterator接口，可以把对象当做数组一样进行循环操作
 
ArrayAccess界面，可以使对象像数组一下进么操作，如：增加，删除,但不能进行遍历
 
IteratorAggregate接口， 针对上面两种进行的中和，
 
RecursiveIterator 接口，遍历多层数据
 
Countable 接口，返回集的数量
 
DirectoryIterator 类，查看目录中的所以文件和子目录
 
ArrayObject类，将Array转化为object//没有遍历功能
 
ArrayIterator类，为ArrayObject提供遍历功能
 
FilterIterator类，可以对元素进行过滤，在accept()方法中设置过滤条件
 
SimpleXMLIterator类，遍历xml文件
 
CachingIterator类，这个类有hasNext()方法，用来判断是否还有下一个元素
 
LimitIterator类，限定返回结果集的数量和位置
 
SplFileObject类，对文本文件进行遍历