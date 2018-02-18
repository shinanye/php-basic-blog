##PHP入门六<br>
###文件系统<br>
**1>读取文件内容**<br>
file_get_contents()<br>
    意义：读取文件中的内容<br>
    语法file_get_contents($filename,$include_path,$context,$offset,$maxlen)<br>
    返回值：返回读取数据或失败（false）<br>
参数表
参数 | 描述 
---------|----------
 filename | 读取的文件名称 
 include_path | 设置搜索路径（可选）
 context | 规定文件句柄的环境（可选） 
  offset | 原始数据流读取开始的偏移量（可选）
 maxlen | 数据读取最大长度（可选）

 ```
set_include_path("file/");  //设置搜寻的路径

if(file_get_contents("file.txt",true)){
    echo file_get_contents("file.txt",true);
}else{
    echo "不存在";
}
```
 >file_get_contents()不仅可以读取本地文件内容还可以读取网页内容

 ```
if(file_get_contents(“http://www.baidu.com”)){
    echo "获得网页内容并输出";
    echo file_get_contents(“http://www.baidu.com”);
}else{
    echo "不存在";
}
```
>$content = file_get_contents('file.txt', null, null, 100, 500);

**2>php中操作文件的方法**
方法 | 描述 | 语法
---------|----------|----------
 [fopen](http://php.net/manual/en/function.fopen.php) | 打开文件 | fopen($filename,$mode,$include_path,$context) 
  [fclose](http://php.net/manual/en/function.fclose.php) | 关闭fopen()打开的文件 | fclose($handle) 
 [fgets](http://php.net/manual/en/function.fgets.php) | 从文件指针中读取一行 | fgets($handle,$len) 
 [fgetss](http://php.net/manual/en/function.fgetss.php) | 从文件指针获取行并剥离HTML标签 | fgetss($handle,$len) 
 [fread](http://php.net/manual/en/function.fread.php) | 读取文件 | fread($handle,$len) 
 [fwrite](http://php.net/manual/en/function.fwrite.php) | 写入文件 | fwrite($handle,$WString,$len) 
 [file](http://php.net/manual/zh/function.file.php) | 把整个文件读入一个数组中 | file($filename,$flags,$context) 
 [feof](http://php.net/manual/zh/function.feof.php) | 文件指针是否到文件结束的位置 | feof($handle) 

>feof()函数中文件指针到了末尾或者出错时则返回 TRUE，否则返回一个错误，其它情况则返回 FALSE。

 ```
$handle = "text.txt";
$fp = fopen($handle, 'rb');
while(!feof($fp)) {
    echo fgets($fp); //读取一行
}
fclose($fp);

$fp = fopen($handle, 'rb');
$contents = '';
while(!feof($fp)) {
    $contents .= fread($fp, 4096); //一次读取4096个字符
}
fclose($fp);
```

往文件中写入内容
```
//打开文件
$filename = fopen("text.txt","w");
//写入数据
 fwrite($filename,"新写入的数据");
//关闭文件
fclose($filename);

//读取
$filename1 = 'text.txt';
if (file_exists($filename1)) {
    echo file_get_contents($filename1);
}
```

**3>判断文件是否存在**<br>
PHP中常用来判断文件存在的函数有两个is_file与file_exists。
>如果只是判断文件存在，使用file_exists就行，file_exists不仅可以判断文件是否存在，同时也可以判断目录是否存在，从函数名可以看出，is_file是确切的判断给定的路径是否是一个文件。<br>

>[is_file()和file_exists()效率](http://www.cnblogs.com/xuan52rock/p/4548635.html)<br>
1)当文件存在时，前者比后者速度快<br>
2)当文件不存在时，两者的访问速度是一样快<br>

**4>判断文件是否可读与可写**<br>
is_readable与is_writeable在文件是否存在的基础上，判断文件是否可读与可写。
```
$filename = './test.txt';
if (is_file($filename)) {
    echo file_get_contents($filename);
}

$filename = './test.txt';
if (is_writeable($filename)) {
    file_put_contents($filename, 'test');
}
if (is_readable($filename)) {
    echo file_get_contents($filename);
}
```

**5>与文件相关的时间点**
方法 | 描述 
---------|----------
 fileowner | 获得文件的所有者 
 filectime | 获取文件的创建时间 
 filemtime | 获取文件的修改时间 
 fileatime | 获取文件的访问时间 

 **6>获得文件大小**<br>
 通过filesize()函数可以取得文件的大小，文件大小是以字节数表示的。<br>

 自定义文件大小转换<br>
 ```
function getsize($size, $format = 'kb'){
    $p = 0;
    if ($format == 'kb') {
        $p = 1;
    } elseif ($format == 'mb') {
        $p = 2;
    } elseif ($format == 'gb') {
        $p = 3;
    }
    $size /= pow(1024, $p);
    return number_format($size, 3);
}
```

**7>删除文件的方法**<br>
unlink()<br>
意义：用于删除指定的文件.<br>
