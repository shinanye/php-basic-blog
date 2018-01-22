## php基础知识一
**一、认识php**：<br>
PHP一种运行在web服务器端的编程语言。<br>
特点：<br>
&emsp;1.运行在服务器duan<br>
&emsp;2.跨平台<br>
&emsp;3.脚本语言<br>
&emsp;4.免费<br>

**二、php代码标识：**<br>
```
<?php
   echo "hello php";
?>
```
需要注意点：<br>
&emsp;&emsp;1.在php中每一条语句结尾处一定用";"<br>
&emsp;&emsp;2.在PHP中<?php ?>不是成对出现，但是一个php文件中只有一个<?php

**三、基本的输出语句**<br>
1.2.echo()--主要用于基本类型的输出;<br>
可以一次输出多个值，多个值之间用逗号分隔。echo是语言结构(language construct)，而并不是真正的函数，因此不能作为表达式的一部分使用。<br>
2.print_r()--主要用于数组打印;<br>
可以把字符串和数字简单地打印出来，而数组则以括起来的键和值得列表形式显示，并以Array开头。但print_r()输出布尔值和NULL的结果没有意义因此用var_dump()函数更适合调试。<br>
3.var_dump()<br>
判断一个变量的类型与长度,并输出变量的数值,如果变量有值输的是变量的值并回返数据类型。此函数显示关于一个或多个表达式的结构信息，包括表达式的类型与值。数组将递归展开值，通过缩进显示其结构。<br>

**四、变量**<br>
&emsp;1.变量作用：存储数据<br>
&emsp;2.变量命名规则：<br>
&emsp;&emsp;①除$符以外的变量必须以字母或“_”开头;<br>
&emsp;&emsp;②变量名只能有字母、数字、“_”或者中文组成;<br>
&emsp;&emsp;③变量不可以有空格，在php中变量名区分大小写。<br>

**五、常量**<br>
定义：常量被定义后在脚本其他位置都不可以改变其值。常量的声明没有“$”<br>
分类：自定义常量和系统常量<br>
自定义常量：<br>
①Define()----define("PI",3.14);<br>
②Const()----Const PI=2.0;<br>
常见的系统常量：<br>
①__FILE__:php程序文件名。它可以帮助我们获取当前文件在服务器的物理位置。<br>
② __DIR__; 程序的根目录<br>
③__LINE__ :PHP程序文件行数。它可以告诉我们，当前代码在第几行。<br>
④PHP_VERSION:当前解析器的版本号。它可以告诉我们当前PHP解析器的版本号，我们可以提前知道我们的PHP代码是否可被该PHP解析器解析。<br>
⑤PHP_OS：执行当前PHP版本的操作系统名称。它可以告诉我们服务器所用的操作系统名称。<br>
<h5>如何判断常量是否被定义</h5>
如果常量被重复定义以后，PHP解析器会发出“Constant XXX already defined”的警告。<br>
eg:

```
define(“PI”,3.14);
$is2 = defined("PI");  //true

```
**六、变量数据类型**<br>
&emsp;在php中有8中数据类型，424组合；<br>
&emsp;**4种标量类型：boolean、int、float、字符串**<br>
特别注意：<br>
①在boolean中true和false不区分大小写，当我们用“echo”指令输出布尔类型时，如果是“true”则输出1，“false”则什么也不输出，此时需要用var_dump获取她的数据类型。<br>
②字符串定义方式：单引号、双引号<br>
&emsp;单引号：当单引号中包含变量时，变量会被当做字符串输出<br>
&emsp;双引号：当双引号中包含变量时，变量会与双引号中的内容连接在一起；<br>
&emsp;eg:<br>
$a=" 我是字符串哦！";<br>
echo "你是什么?$a";-------输出：你是什么？我是字符串哦！<br>
echo '你是什么?$a';-------输出：你是什么？$a<br>

&emsp;**2种复合类型：数组、对象**<br>
&emsp;**4种特殊类型：资源、空类型、回调类型、伪类型**<br>
资源：主要为开发者提供操作资源的方法（对资源进行创建、使用以及释放）。<br>
&emsp;eg:<br>
```
$file=fopen("f.txt","r");   //打开文件<br>
$con=mysql_connect("localhost","root","root");  //连接数据库<br>
$img=imagecreate(100,100);//图形画布<br>
```
空类型：表示一个变量没有被赋值。<br>
出现空类型的三种情况：<br>
&emsp;①声明变量但是没有赋值（初始化）<br>
&emsp;②在声明变量打的同时赋NULL<br>
&emsp;③声明变量并且赋非空，只是在其后调用了unset($str)<br>

**七、PHP数据类型转换**<br>
$_num = 12.3456;<br>
&emsp;①强制类型转换-----eg:(int)$_num<br>
&emsp;②使用3个具体类型的转换函数：intval()、floatval()、strval() -----eg：intval($_num)<br>
&emsp;③使用通用类型转换函数settype($_num,'int') <br>
特别注意：<br>
前两者的类型转换不会影响变量本身，但是settype(mixed var,string type) 方法则会改变$_num本身(该变量不再是基本数据类型)；<br>

**八、运算符**<br>
1.算术运算符<br>
在PHP中的常用的算术运算符对应下表：<br>
![](https://github.com/shinanye/imgReposity/blob/master/arithmetic.png)<br>
<br>
2.赋值运算符<br>
&emsp;①“=”：把右边表达式的值赋给左边的运算数。它将右边表达式值复制一份，交给左边的运算数。换而言之，首先给左边的运算数申请了一块内存，然后把复制的值放到这个内存中。<br>
&emsp;②“&”：引用赋值，意味着两个变量都指向同一个数据。它将使两个变量共享一块内存，如果这个内存存储的数据变了，那么两个变量的值都会发生变化。<br>
<br>
3.比较运算符<br>
比较运算符主要是用于进行比较运算的。在PHP中常用的比较运算符如下表：
![](https://github.com/shinanye/imgReposity/blob/master/compare.png)<br>
<br>
4.三元运算符<br>
三元表达式语法：<br>
(expr1)?(expr2):(expr3)<br>
如果expr1的值为true，则此表达式的值为expr2，否则为expr3。<br>
<br>
5.逻辑运算符<br>
①逻辑与：一假为假，全真为真；<br>
②逻辑或：一真为真，全假为假；<br>
③逻辑非：非黑即白；（在这句话上不要转牛角尖，知道就好了）<br>
<br>
6、字符串连接运算符<br>
①连接运算符(“.”)：它返回将右参数附加到左参数后面所得的字符串。<br>
②连接赋值运算符(“.=”)：它将右边参数附加到左边的参数后。<br>
<br>
7、错误控制运算符<br>
PHP中提供了一个错误控制运算符“@”，对于一些可能会在运行过程中出错的表达式时，我们不希望出错的时候给客户显示错误信息，这样对用户不友好。于是，可以将@放置在一个PHP表达式之前，该表达式可能产生的任何错误信息都被忽略掉；<br>
&emsp;eg:<br>
```
define("PI", 3.14);<br>
@define("PI", 3.12);<br>
echo "出错了，错误原因是:".$php_errormsg;//出错了
```
错误原因是:Constant PI already defined<br>

