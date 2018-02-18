## php入门四<br>
### 一、正则表达式<br>
**1>正则表达式的基本语法:**<br>
正则匹配模式使用分隔符与元字符组成，分隔符可以是非数字、非反斜线、非空格的任意字符。经常使用的分隔符是正斜线(/)、hash符号(#) 以及取反符号(~)<br>
>/foo bar/<br>
#^[^0-9]$#<br>
~php~<br>

>如果模式中包含分隔符，则分隔符需要使用反斜杠（\）进行转义。<br>
$pattern = "/http:\/\//";

**2>元字符和转义符**

Column A | Column B | Column C| Column C
---------|----------|---------|---------
 A1 | B1 | C1| C1
 A2 | B2 | C2| C1
 A3 | B3 | C3| C1

元字符 |  含义   | 元字符 | 含义 
---------|----------|----------|----------
 \ | 一般用于转义字符 | . | 匹配除了换行符外的任意字符 
 ^ | 行首 | $ | 行尾 
 [ | 开始字符类定义 | ] | 结束字符类定义 
 | | 开始一个可选分支 | （ | 子组的开始标志 
 ） | 子组的结束标志 | { | 自定义量词开始标记
 } | 自定义量词结束标记 | -|标记字符范围

量词元字符：
元字符 |  含义   | 元字符 | 含义 
---------|----------|----------|----------
 ？ | 表示[0,1]次匹配 | * | [0,n]次匹配 
 +  | 表示[1,n]次匹配

**3>贪婪模式和惰性模式**
>贪婪模式：在可匹配与可不匹配的时候，优先匹配<br>
_当使用+之后将会变的贪婪，它将匹配尽可能多的字符，但使用问号?字符时，它将尽可能少的匹配字符，既是懒惰模式。_
```
$p = '/\d+\-\d+/';
$str = "我的电话是010-12345678";
preg_match($p, $str, $match);
echo $match[0]; //结果为：010-12345678
```

>懒惰模式：在可匹配与可不匹配的时候，优先不匹配
```
$p = '/\d?\-\d?/';
$str = "我的电话是010-12345678";
preg_match($p, $str, $match);
echo $match[0];  //结果为：0-1
```

**4>字符串是否存在**
>preg_match()<br>
    意义：用来判断一类字符模式是否存在。<br>
    语法：preg_match($pattern,$str)<br>
    返回值:返回 pattern 的匹配次数。 它的值将是0次（不匹配）或1次，因为preg_match()在第一次匹配后 将会停止搜索。
```
$p = '/love/';
$str = "I love you too";
if (preg_match($p, $str)) {
    echo 'matched';
}
```

>preg_match_all()<br>
    意义：搜索字符串中所有给定正则表达式的匹配结果并且将它们以指定顺序输出到matches中。在第一个匹配找到后, 子序列继续从最后一次匹配位置搜索.<br>
    语法：preg_match_all ($pattern,$str,$matchs,$flags)<br>
```
$p = "/<tr><td>(.*?)<\/td>\s*<td>(.*?)<\/td>\s*<\/tr>/i";
$str = "<table> <tr><td>Eric</td><td>25</td></tr> <tr><td>John</td><td>26</td></tr> </table>";
preg_match_all($p, $str, $matches);
print_r($matches);
//Array ( [0] => Array ( [0] => Eric25 [1] => John26 ) [1] => Array ( [0] => Eric [1] => John ) [2] => Array ( [0] => 25 [1] => 26 ) )
```

```
preg_match_all('/(foo)(bar)(baz)/', 'foobarbaz', $matches, PREG_OFFSET_CAPTURE);
print_r($matches);
```
**$matches结果排序为$matches[0]保存完整模式的所有匹配, $matches[1] 保存第一个子组的所有匹配，**

**5>正则表达式的搜索和替换**<br>
preg_replace()<br>
意义：搜索字符串中的特定字符或者替换指定的字符<br>
语法：preg_replace($pattern, $replacement, $string)<br>
返回值：如果string是一个数组， preg_replace()返回一个数组， 其他情况下返回一个字符串，如果发生错误，返回 NULL 。
```
$string = 'February 17, 2018';
$pattern = '/(\w+) (\d+), (\d+)/i';
$replacement = '$3, ${1} $2';
echo preg_replace($pattern, $replacement, $string); //2018, February 17
```
>其中${1}与$1的写法是等效的，表示第一个匹配的字串，$2代表第二个匹配的。

用正则表达式去除多余的空格或字符
```
$str = 'one     two';
$str = preg_replace('/\s+/', ',', $str);
echo $str; // 结果改变为'one,two'
```