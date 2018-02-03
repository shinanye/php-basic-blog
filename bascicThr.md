##php基础入门三<br>
###字符串<br>
1 字符串定义<br>
    ①单引号<br>
    ②双引号<br>
    ③heredoc语法结构<br>
    eg:语法定义<br>
    单引号定义的字符串：$hello = 'hello world';<br>
    双引号定义的字符串：$hello = "hello world";
    heredoc语法结构定义的字符串：<br>
    $hello = <<<TAG<br>
    hello world<br>
    TAG;<br>
    注意事项：<br>
    PHP中允许双引号中的字符串直接包含变量，会被解析。<br>
    而单引号串中的内容总被认为是普通字符，不回被解析。<br>
    在heredoc语法中“TAG”是自定义的可以随便起。
```
$str="hello";
echo "str is $str"; //运行结果: str is hello
echo "<br>";
echo 'str is $str'; //运行结果: str is $str 
```

2 字符串操作<br>
1>字符串连接<br>
 在php中连接两个字符串用“.”连接
```
$str1='hello';
$str2=' php';
$str = $str1.$str2;
echo $str;
```

2>去掉字符串中空格<br>
    PHP中有三个函数可以去掉字符串中的空格<br>
    ①trim去除一个字符串两端空格。<br>
    ②rtrim是去除一个字符串右部空格。<br>
    ③ltrim是去除一个字符串左部空格。
```
echo trim("    空格   ")."<br>";
echo rtrim("   空格   ")."<br>";
echo ltrim("   空格   ")."<br>";//打开浏览器开发者工具就可以看到效果
```

3>获取字符串长度<br>
php中strlen()获取字符串长度。
```
$str = "你好吗,hello!";
echo mb_strlen($str,"UTF8");//结果：10
```
_特别注意：_<br>
    但是strlen使用的对象是英文字符串，一旦字符串中出现汉字就无法计算字符串的长度，当字符中有汉字时则用mb_strlen()函数获取字符串中中文长度。<br>

4>字符串的截取<br>
    字符串的截取分为英文、中文字符串的截取<br>
    ①英文字符串截取substr()
    语法：substr(字符串变量,开始截取的位置，截取个数）
```
$str='i like banana';  //截取love这几个字母
echo substr($str, 2, 4);
```
&emsp; ②中文字符串截取mb_substr()<br>
    语法：mb_substr(字符串变量,开始截取的位置，截取个数, 网页编码）
```
$str='我爱你，中国';   //截取中国两个字
echo mb_substr($str, 4, 2, 'utf8');
```

5>字符串查找<br>
    查询特定的字符串在大字符串中的位置（有一个字符串$str = 'I hate php';，怎么样找到其中的php在哪个位置呢？）。<br>
    语法：strpos(要处理的字符串, 要定位的字符串, 定位的起始位置[可选])<br>
    返回值：找到第一个字符的索引值并且返回<br>
    ①英文字符串查找
```
$str = 'I hate php';
$pos = strpos($str, 'hate');
echo $pos;//结果显示2
```    
②中文字符串查找
```
$str="截取中文字符串";
$t1 = mb_strpos($str,'中',0,"utf8");
$t2 = mb_strpos($str,'串',0,"utf8");
echo $s = mb_substr($str,$t1,$t2-$t1+1,"utf8");//中文字符串
```

6>替换字符串<br>
    替换函数str_replace()<br>
    语法：str_replace(要查找的字符串, 要替换的字符串, 被搜索的字符串, 替换进行计数[可选])
```
$str = 'I hate PHP';
$replace = str_replace('hate', 'like', $str);
echo $replace;//I like PHP
```

7>格式化字符串<br>
    sprintf() 函数把格式化的字符串写入变量中。
%s | %s | %u 
---------|----------|---------
匹配字符串 | 匹配整数 | 匹配浮点 

    语法：sprintf(格式, 要转化的字符串)<br>
    返回值：格式化好的字符串
```
$number = 2;
$str = "Shanghai";
$txt = sprintf("There are %u million cars in %s.",$number,$str);

$result = sprintf('%06.2f', $str);
echo $result;//结果显示99.90
```

拓展：%06.2f意义
    % "起始字符";<br>
    0 是 "填空字元" ，表示如果位置空着就用0来填补;<br>
    6 占位元素(小数点也算一个占位);<br>
        99.90一共5个占位，现在需要6个占位，所以用“填空字元”在最前面99.90填满;<br>
    .2 小数点后面的浮点数的位数;<br>
    =f "转换字符" 结尾。<br>

8>字符串的合并(针对数组合并成字符串)<br>
    语法：implode(分隔符[可选], 数组)<br>
    返回值：把数组元素组合为一个字符串
```
$arr = array('I', 'hate',"php");
$result = implode(' ', $arr);
print_r($result);//I hate php
```

9>字符串的分割<br>
    函数说明：explode(分隔符[可选], 字符串)<br>
    返回值：函数返回由字符串组成的数组
```
$str = 'apple,banana';
$result = explode(',', $str);
print_r($result);//array('apple','banana')
```

10>字符串的转义<br>
    1、语法：addslashes()<br>
    返回值：一个转义后的字符串<br>
    用途：addslashes() 函数返回在预定义字符之前添加反斜杠的字符串。

    2、语法：stripslashes() <br>
    返回值：字符串<br>
    用途：函数删除由 addslashes() 函数添加的反斜杠。

     预定义字符是：<br>
    █ 单引号（'）<br>
    █ 双引号（"）<br>
    █ 反斜杠（\）<br>
    █ NULL<br>
```
$str='Shanghai is the "biggest" city in China.';
$str1 = addslashes($str);
echo($str1);//Shanghai is the \"biggest\" city in China.
echo "<br>";   
echo stripslashes($str1);  //Shanghai is the "biggest\" city in China.
```
    3、语法：htmlspecialchars()<br>
    返回值：返回被转换的字符串。<br>
    用途：函数把预定义的字符转换为 HTML 实体（把预定义的字符 "<" （小于）和 ">" （大于）转换为 HTML 实体）。

    4、语法：htmlspecialchars_decode()<br>
    返回值：返回已转换的字符串。<br>
    用途：函数把预定义的 HTML 实体转换为字符。

    预定义的字符是：<br>
    █ & （和号）成为 &<br>
    █ " （双引号）成为 "<br>
    █ ' （单引号）成为 '<br>
    █ < （小于）成为 <<br>
    █ > （大于）成为 ><br>
```
$str = "This is some <b>bold</b> text.";
echo htmlspecialchars($str);//This is some <b>bold</b> text.
echo htmlspecialchars_decode($str);//This is some **bold** text.
```

######字符串的遍历 获取每个字符
```
$str="你好hello999.9";
for($i=0;$i<mb_strlen($str,"utf8");$i++){
    echo mb_substr($str,$i,1,"utf8")."---";
}
```


    
    



