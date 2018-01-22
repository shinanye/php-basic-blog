## php入门二
**一、语言结构**<br>
分类：顺序结构、条件结构、循环结构<br>
1.顺序结构<br>
&emsp;按着顺序一直往下执行。<br>
2.条件结构<br>
&emsp;满足条件继续执行，不满足则执行其他的语句。<br>
&emsp;  ①if...else  在if-else中不执行if中语句就执行else中语句（条件为真则执行）<br>
&emsp;  ②if..else if..else<br>
&emsp;  ③switch..case<br>
3.循环语句<br>
&emsp;①while  在if-else中不执行if中语句就执行else中语句（条件为真则执行）<br>
&emsp;②do..while if..else<br>
&emsp;③for<br>
&emsp;④foreach

**二、数组**<br>
定义：有限个类型相同的变量的集合（在php中数组以键值对的形式存储）。<br>
类型：索引数组、关联数组<br>
&emsp;1.索引数组<br>
&emsp;&emsp; 定义：索引数组是指数组的键是整数的数组，并且键的整数顺序是从0开始，依次类推。
&emsp;&emsp;1>_索引数组赋值的方法：_<br>
&emsp;&emsp;①用数组变量的名字后面跟一个中括号的方式赋值。eg:array[0]='123456';<br>
&emsp;&emsp;②用array()创建一个空数组，使用=>符号来分隔键和值，左侧表示键，右侧表示值。键一定是整数，eg:array('0'=>'苹果');<br>
&emsp;&emsp;③用array()创建一个空数组，直接在数组里用英文的单引号'或者英文的双引号"赋值，比如array('苹果');这个数组相当于array('0'=>'苹果');<br>
&emsp;注意：<br>
&emsp;&emsp;<1>数组默认索引值从“0”开始<br>
&emsp;&emsp;<2>定义一个空的数组<br>
&emsp;&emsp;&emsp;&：$arr=[];//有的这样定义一个数组会报错是因为php的版本低，升级一下PHP的版本就可以了
&emsp;&emsp;&emsp;&：$arr=array();

&emsp;&emsp;&emsp;2>_访问数组_<br>
&emsp;&emsp;①数组变量的中括号跟该访问的键值;<br> 
&emsp;&emsp;②for循环;<br> 
&emsp;&emsp;③foreach;<br> 
&emsp;&emsp; eg:<br> 
&emsp;&emsp;索引值查找：<br> 
&emsp;&emsp;$fruit=array('苹果','香蕉','菠萝');<br> 
&emsp;&emsp;$fruit0 = $fruit['0'];<br> 
&emsp;&emsp;print_r($fruit0);//结果为苹果<br> 

&emsp;&emsp;for访问数组：<br> 
&emsp;&emsp;for($i=0; $i<3; $i++){<br> 
&emsp;&emsp;&emsp;echo '<br>数组第'.$i.'值是：'.$fruit[$i];<br> 
&emsp;&emsp;}<br> 

&emsp;&emsp;foreach访问数组：<br> 
&emsp;&emsp;foreach($fruit as $k=>$v){<br> 
&emsp;&emsp;&emsp;echo '第'.$k.'值是：'.$v;<br> 
&emsp;&emsp;}<br> 
&emsp;2.关联数组<br>
&emsp;&emsp;关联数组是指数组的键是"字符串"的数组。<br>
&emsp;&emsp;1> _关联数组的初始化：_<br>
&emsp;&emsp;eg:$fruits = array('apple'=>"苹果",'pinle'=>"菠萝");<br><br>
&emsp;&emsp;2>_关联数组的赋值_<br>
&emsp;&emsp;①数组后面跟一个中括号的方式赋值，eg：$arr['apple'] = '苹果';<br>
&emsp;&emsp;②创建一个空的数组，用“=>”符号来分隔键和值，键一定要是“字符串”， eg:array('apple'=>'苹果')；<br><br>
&emsp;&emsp;3>_访问数组_<br>
&emsp;&emsp;①键值索引----------eg:$fruit0 = $fruit['apple'];<br> 
&emsp;&emsp;②foreach循环<br>
&emsp;&emsp;eg：<br>
&emsp;&emsp;foreach($fruit as $key => $value){<br>
&emsp;&emsp;&emsp;echo '键值名：'.$key.",其值：".$value;<br>
&emsp;&emsp;}<br>
&emsp;&emsp;③for循环

&emsp;**三、数组的操作**<br>
&emsp;&emsp;1>_数组中添加一个或多个元素_<br>
&emsp;&emsp;末尾添加：array_push()   eg:array_push($arr,"a","b");//返回数组长度  <br>
&emsp;&emsp;开始添加：array_unshift()   eg:array_unshift($arr);   //所有的数值键名改为从零开始，所有的文字键名保持不变  <br><br>
&emsp;&emsp;2>_数组中删除一个元素_<br>
&emsp;&emsp;末尾删除：array_pop()    eg:array_pop($arr);   //返回删除的元素，如果数组为空（或者不是数组）则会返回NULL   <br>
&emsp;&emsp;开始删除：array_shift()   eg:array_shift($arr);<br>
&emsp;&emsp;注意：<br>
&emsp;&emsp;这四个方法都会改变原数组,添加返回的都是数组的长度，删除返回的都是删除的元素。<br><br>
&emsp;&emsp;3>_任意位置添加（删除）一个或者多个元素_<br>
&emsp;&emsp;语法： array_splice(数组名,起始索引值,删除个数,添加的内容); <br>
&emsp;&emsp;第三个参数：不为0删除元素的个数； <br>
&emsp;&emsp;第四个参数：有就是要添加的内容； <br>
&emsp;&emsp;eg： <br>
&emsp;&emsp;添加：
```
$a=array('apple','banana','orange'); <br>
array_splice($a,2,0,'grape'); <br>
var_dump($a); <br>

```
&emsp;&emsp;删除：
```
$a1=array("a"=>"red","b"=>"green","c"=>"blue","d"=>"yellow");
$a2=array("a"=>"purple","b"=>"orange");
array_splice($a1,0,2,$a2);
var_dump($a1);//删除和添加同时进行
```

&emsp;&emsp;4>_合并数组_<br>
&emsp;&emsp;array_merge()-----将数组合并到一起，如果输入的数组中有相同的字符串键名，则该键名后面的值将覆盖前一个值。然而，如果数组包含数字键名，后面的值将不会覆盖原来的值，而是附加到后面。<br>
&emsp;&emsp;语法：array_merge(数组1,数组2.....);<br>
&emsp;&emsp;eg:
```
$arr1=array("apple"=>"苹果1","banana"=>"香蕉","pear"=>"梨");
$arr2=array("apple"=>"苹果2");
$mergeArr=array_merge($arr1,$arr2);
print_r($mergeArr);
```
&emsp;&emsp;输出：Array ( [apple] => 苹果2 [banana] => 香蕉 [pear] => 梨 );<br><br>
&emsp;&emsp;5>in_array()-----在一个函数中汇总搜索一个特定的数组，数组存在则返回true，否则false；<br>
&emsp;&emsp;语法：in_array(汇总数组,查询数组);<br>
&emsp;&emsp;eg:
```
$fruit="apple";
$fruits=array("apple","banana","orange","pear");
if(in_array($fruit,$fruits)){
echo '$fruit'."在数组中";
}
```
&emsp;&emsp;6>_数组中查找指定键值_<br>
&emsp;&emsp;array_key_exists()----一个数组中找到指定的键值，如果找到返回true，否则返回false<br>
&emsp;&emsp;语法：array_key_exists(键值名,数组);<br>
&emsp;&emsp;eg:
```
 $fruits=array("apple"=>"苹果","banana"=>"香蕉","orange"=>"橙子","pear"=>"梨");
$true=array_key_exists("apple",$fruits);
if($true)
echo "存在";
else
echo "不存在";
```
&emsp;&emsp;7>_获取数组中所有键值_<br>
&emsp;&emsp;array_keys()----- 用于返回该数组的所有键值，产生一个新的数组。<br>
&emsp;&emsp;语法：array_keys(数组名);<br>
&emsp;&emsp;eg:
```
$fruits=array("apple"=>"苹果","banana"=>"香蕉","orange"=>"橙子","pear"=>"梨");
$keys=array_keys($fruits);
print_r($keys);
```
&emsp;&emsp;输出：Array ( [0] => apple [1] => banana [2] => orange [3] => pear )<br><br>
&emsp;&emsp;8>_获取数组中的所有值_<br>
&emsp;&emsp;arrar_values()-----获取一个数组的所有属性值。
&emsp;&emsp;语法：arrar_values(数组名);<br>
&emsp;&emsp;eg：
```
$fruits=array("apple"=>"苹果","banana"=>"香蕉","orange"=>"橙子","pear"=>"梨");
$values=array_values($fruits);
print_r($values);
```
&emsp;&emsp;输出：Array ( [0] => 苹果 [1] => 香蕉 [2] => 橙子 [3] => 梨 )<br><br>
&emsp;&emsp;