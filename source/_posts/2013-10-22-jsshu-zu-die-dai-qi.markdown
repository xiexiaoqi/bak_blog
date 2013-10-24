---
layout: post
title: "JS 数组迭代方法"
date: 2013-10-22 02:18
comments: true
categories: [JS]
---
ECMAScripts 5 为数组提供了5个迭代方法，分别为：
{% blockquote %}
<ul>
    <li>every()：对数组中的每一项运行一个函数，如果该函数对每一项都返回true,则返回true。</li>
    <li>filter()：对数组中的每一项运行一个函数，返回该函数会返回true的项目组成的数组。</li>
    <li>map()：对数组中的每一项运行一个函数，返回每次函数调用的结果 组成的数组。</li>
    <li>some()：对数组中的每一项运行一个函数，如果该函数对任一一项返回true,则返回true。。</li>
    <li>forEach()：对数组中的每一项运行一个函数，无返回值。</li>
</ul>
{% endblockquote %}
<!--more-->
这里的每个方法都接受两个参数：要在每一项上运行的函数；（可选项）运行该函数的作用域对象——影响 this 的值。

传入这些方法中的函数会接受三个参数：数组的项；数组项的索引；数组对象本身。

从上面的方法可以看出根据使用方法的不同，所返回的结果也是不同。

请看以下例子：
<!--every()-->
{% codeblock every() lang:js %}
var number = [ 1, 2, 3, 4, 5, 4, 3, 2, 1 ];
var everyResult = number.every( function( item, index, array ){
	return item > 2;
} );

//一假全假，有点类似于&&运算。
alert( everyResult );  // false
{% endcodeblock %}

<!--filter()-->
{% codeblock filter() lang:js %}
var number = [ 1, 2, 3, 4, 5, 4, 3, 2, 1 ];
var filterResult = number.filter( function( item, index, array ){
	return item > 2;
} );

//返回符合条件的结果
alert( filterResult );  // 3,4,5,4,3
{% endcodeblock %}

<!--map()-->
{% codeblock map() lang:js %}
var number = [ 1, 2, 3, 4, 5, 4, 3, 2, 1 ];
var mapResult = number.map( function( item, index, array ){
	return item * 2;
} );

//返回执行结果
alert( mapResult );  // 2,4,6,8,10,8,6,4,2
{% endcodeblock %}

<!--some()-->
{% codeblock some() lang:js %}
var number = [ 1, 2, 3, 4, 5, 4, 3, 2, 1 ];
var someResult = number.some( function( item, index, array ){
	return item > 2;
} );

//如果有一项符合条件，则返回true
alert( someResult );  // true
{% endcodeblock %}

<!--forEach()-->
{% codeblock forEach() lang:js %}
var number = [ 1, 2, 3, 4, 5, 4, 3, 2, 1 ];
var forEachResult = number.forEach( function( item, index, array ){
	return item > 2;
} );

//无返回值，相当于for循环
alert( forEachResult );  // undefined
{% endcodeblock %}

【完】


