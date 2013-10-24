---
layout: post
title: "PHP SPL库尝试:DirectoryIterator类"
date: 2013-10-22 00:10
comments: true
categories: [PHP]
---
以往如果我们要遍历一个目录下的文件，包括子目录，一般是使用PHP Directory 函数，如下面这个方法，但是如果你还想获得目录下文件的信息，就还得费一些手段了。
<!--more-->
{% codeblock 遍历目录一般做法 lang:php %}
<?php
    function list_dir($path)
    {
        $dir_handle = opendir($path);
        $ret_arr = array();
        while($dir_read = readdir($dir_handle))
        {
            if($dir_read == "." || $dir_read == "..")
                continue;
            
            if(is_dir($dir_read))
            {
                $ret_arr[$path][$dir_read] = list_dir($path.'/'.$dir_read);
            }
            else
            {
                $ret_arr[$path][] = $dir_read;
            }
            
        }
        
        return $ret_arr;
    }
?>
{% endcodeblock %}
使用SPL类库中的DirectoryIterator类，它可以以一种操作类属性的方式来取得关于文件的一些属性，下面也看一上使用了DirectoryIterator写的遍历目录的方法。
{% codeblock 使用DirectoryIterator类做法 lang:php %}
<?php
    function list_dir($path)
    {
        $ret_array = array();
        foreach( new DirectoryIterator($path) as $keys => $files )
        {
             
            if( $files->isDot() )
            {
                continue;
            }
            $fileName = $files->getFilename();
            if( $files->getType() == 'dir' )
            {
                $ret_array[$fileName] = list_dir($path.'/'.$fileName);
            }
            else
            {
                $ret_array[] = $fileName;
            }
             
        }
        return $ret_array;
    }
?>

{% endcodeblock %}
可用到关于文件检测的方法如：isReadable(); isFile(); isDir(); isDir()....具体方法，
请参考SPL.php文件，或http://www.php.net/manual/en/directoryiterator.construct.php

【完】