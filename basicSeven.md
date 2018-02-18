## php入门七<br>
### 日期和时间戳<br>
**1>获得Unix时间戳**<br>
表示从 1970年1月1日 00:00:00 到某一时间点的秒数之和。<br>
1. 获取当前时间戳<br>
time()<br>
&emsp;意义：获取服务器当前时间的时间戳。<br>
&emsp;语法：time()<br>
&emsp;返回值：从 1970年1月1日 00:00:00 到当前时间的秒数之和 
```
echo time();
```

2. 获得任意时刻的时间戳<br>
strtotime()<br>
&emsp;意义：获取某个日期（时间）的时间戳。<br>
&emsp;语法：strtotime(时间点)<br>
&emsp;返回值：从 1970年1月1日 00:00:00 到指定时间的秒数之和 
```
echo strtotime('2018-02-18 00:0:25');

echo strtotime('now');//等价于time()

echo strtotime("+1 seconds");//相当于将现在的日期和时间加上了1秒，等价于time()+1

echo strtotime('+1 day');//将当前日期和时间加上一天时间
```

**2>获得当前日期**<br>
date()<br>
&emsp;意义：获得当前日期<br>
&emsp;语法：date(时间戳格式，规定时间戳的秒数)<br>
&emsp;返回值：日期或时间
```
echo date("Y-m-d",1555532);//表示unix时间戳
```
>第二个参数是一个可选参数

1. 获得当前时间数组<br>
&emsp;getdate()<br>
&emsp;意义：获得当前时间的数组<br>
&emsp;语法：getdate()<br>
&emsp;返回值：当前时间相关信息
```
$arr=getdate();
print_r($arr);
```

**3>格式化格林威治（GMT）标准时间**<br>
gmdate()<br>
&emsp;意义：格式化一个GMT的日期和时间<br>
&emsp;语法：gmdate(时间戳格式,指定时间点)<br>
&emsp;返回值：格林威治标准时（GMT）。
```
date_default_timezone_set("PRC");
echo date('Y-m-d H:i:s', time()); //输出为：2018-02-18 13:11:36
echo "<br>";
echo gmdate('Y-m-d H:i:s', time()); //输出为：2018-02-18 05:11:36 因为格林威治时间是现在中国时区的时间减去8个小时，所以相对于现在时间要少8个小时

```
>中国时区是东八区，领先格林威治时间8个小时。<br>
在使用格林威治时间时要执行代码最初加上date_default_timezone_set("PRC");



