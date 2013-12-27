---
layout: post
title: "PHP调试工具XHProf安装与使用"
date: 2013-12-27 14:03
comments: true
categories: [PHP]
---
XHProf是一个PHP性能调试分析工具，在不知道这个工具之前一直使用的是XDebug。
在使用XDebug时一直很头疼一个问题，就是配置好后它会对整个WEB服务器上的网站进行分析，生成文件。
无法自定义具体分析哪一个网站。XHProf可又很好的解决这一问题。

安装XHProf
{% codeblock %}
#下载安装文件
wget http://pecl.php.net/get/xhprof-0.9.4.tgz 
tar zxf xhprof-0.9.4.tgz
cd xhprof-0.9.4  
cd extension  
phpize  
./configure  
make  
make install  
{% endcodeblock %}
<!-- more --> 
添加so文件
{% codeblock %}
vim xhprof.ini

extension=xhprof.so  
#分析文件存放目录，需要预先创建
xhprof.output_dir=<directory_for_storing_xhprof_runs>  
{% endcodeblock %}

查看安装结果
{% codeblock lang:php %}
<?php
    phpinfo();
?>
{% endcodeblock %}
{% img /images/post_img/xhprof_info.png phpinfo() %}


将安装目录下的examples,xhprof_html,xhprof_lib复制到站点根目录下。
{% codeblock %}
examples    一个简单的试例
xhprof_html 查看分析结果
xhprof_lib  分析时所用到的库文件
{% endcodeblock %}

到这里就已经安装完成了。如何使用可以参照examples/sample.php。

{% codeblock sample.php lang:php %}
<?php

	function bar($x) {
	  if ($x > 0) {
	    bar($x - 1);
	  }
	}

	function foo() {
	  for ($idx = 0; $idx < 5; $idx++) {
	    bar($idx);
	    $x = strlen("abc");
	  }
	}

	// 启动 xhprof 性能分析器
	xhprof_enable();

	// 执行自定义方法
	foo();

	// 停止 xhprof 分析器
	$xhprof_data = xhprof_disable();

	//输入库文件
	$XHPROF_ROOT = realpath(dirname(__FILE__) .'/..');
	include_once $XHPROF_ROOT . "/xhprof_lib/utils/xhprof_lib.php";
	include_once $XHPROF_ROOT . "/xhprof_lib/utils/xhprof_runs.php";

	// save raw data for this profiler run using default
	// implementation of iXHProfRuns.
	$xhprof_runs = new XHProfRuns_Default();

	// save the run under a namespace "xhprof_foo"
    $namespace = 'xhprof_foo';
    //返回run_id,查询结果时使用
	$run_id = $xhprof_runs->save_run($xhprof_data, $namespace);

	//点击下面的view info 链接，查看具信息

	echo "---------------\n".
	     "<a target='_blank' href = 'http://192.168.20.89:8080/xhprof/xhprof_html/index.php?run={$run_id}&source={$namespace}'>
	     VIEW INFO
	     </a>\n".
	     "---------------\n";
?>
{% endcodeblock %}

默认是以表格形式列出信息，xhprof还提供一种拓扑图的呈现方式。这个方式需要安装Graphviz画图工具。
此工具需要先安装libpng，如果没有装这个库则 执行时可能会把类似“png格式错误”这类的错误。

安装 libpng
{% codeblock %}
#下载libpng-1.5.17
wget http://jaist.dl.sourceforge.net/project/libpng/libpng15/1.5.17/libpng-1.5.17.tar.gz
tar -zxvf libpng-1.5.17.tar.gz
cd libpng-1.5.17 
./configure  
make  
make install
{% endcodeblock %}

安装 Graphviz
{% codeblock %}
#下载graphviz-2.24.0
wget http://www.graphviz.org/pub/graphviz/stable/SOURCES/graphviz-2.24.0.tar.gz  
tar zxf graphviz-2.24.0.tar.gz  
cd graphviz-2.24.0  
./configure  --with-png=yes
make  
make install 
{% endcodeblock %}

安装完成后，可以在结果列表页点击 [View Full Callgraph] 查看拓扑图
结果如下
<a href = "/images/post_img/xhprof_info_table.png" title = 'table' class = 'fl_left'>
{% img /images/post_img/xhprof_info_table.png 300 %}
</a>
<a href = "/images/post_img/xhprof_info_png.png" title = 'png' class = 'fl_left'>
{% img /images/post_img/xhprof_info_png.png 300 %}
</a>

<p class = 'clear'></p>
参考链接：

http://www.php.net/manual/zh/book.xhprof.php

PHP调试工具XHProf安装与使用

【完】