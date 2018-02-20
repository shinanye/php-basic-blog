## php入门九<br>
### 一、文件上传<br>
通过PHP，可以将文件上传到服务器。数据向服务器端提交数据可以通过form、post方式，但是post不能提交文件类型的数据信息。<br>
**1>php文件上传指令配置**
>1. file_uploads=on|off<br> 
&emsp;确定服务器上的PHP脚本是否可以接受文件上传。<br>
2. max_execution_time=integer<br>
&emsp;PHP脚本在注册一个致命错误之前可以执行的最长时间，以秒为单位。<br>
3. memory_limit=integer<br> 
&emsp;设置脚本可以分配到的最大内存，以MB为单位。这可以防止失控的脚本独占服务器内存。<br>
4. upload_max_filesize=integer<br>
&emsp;设置上传文件最大大小，以MB为单位。<br>
5. upload_tmp_dir=string<br>
&emsp;设置上传文件在处理之前必须存放在服务器的临时一个位置，直到文件移动到最终目的地为止。<br>
6. post_max_size=integer<br>
&emsp;确定通过POST方法可以接受的信息的最大大小，以MB为单位。<br>

2>$_FILES数组
```
<form action="upload_file.php" method="post"enctype="multipart/form-data">
    <label for="file">上传文件:</label>
    <input type="hidden" name="MAX_FILE_SIZE" value="1000"/>
    <input type="file" name="file" id="file" /> 
    <img id="preview">
    <br />
    <input type="submit" name="submit" value="Submit" />
</form>
```

>ENCTYPE="multipart/form-data":<br>
这里是固定写法，否则文件上传失败。<br>
ACTION="upload.php":<br>
定义要处理上传的程序文件路径 。<br>
METHOD="post":<br>
定义传输方式为POST，一般情况下Form提交数据都设置为POST。<br>
＜input type="hidden" name="MAX_FILE_SIZE" value="1000000"＞<br>
这是一个隐藏域，定义了上传文件的大小上限，超过这个值时，上传失败。它必须定义在文件上传域的前面.而且这里定义的值不 能超过在php.ini 文件中upload_max_filesize设置的值,否则没有意义了.（注意：MAX_FILE_SIZE 的值只是对浏览器的一个建议，实际上它可以被简单的绕过。因此不要把对浏览器的限制寄希望于该值。实际上，PHP.ini设置中的上传文件最大值，是不会 失效的。但是最好还是在表单中加上 MAX_FILE_SIZE，因为它可以避免用户在花时间等待上传大文件之后才发现该文件太大了的麻烦。） <br>
\<input type="file" name="file" /><br>
这是文件上传域,Type属性必须设置为file,但Name属性可以自定义,这个值会在代码文件中使用。 <br>

```
<?php
	print_r($_FILES);
?>
```
>**$_FILES超级全局变量，它储存各种与上传有关的信息，这些信息对于通过PHP脚本上传到服务器的文件至关重要。**<br>
1. 存储在$_FILES["file"]["tmp_name"]变量中的值就是文件在Web服务器中临时存储的位置。<br>
2. 存储在$_FILES["file"]["name"]变量中的值就是用户系统中的文件名称。<br>
3. 存储在$_FILES["file"]["size"]变量中的值就是文件的字节大小。<br>
4. 存储在$_FILES["file"]["type"]变量中的值就是文件的MIME类型，例如：text/plain或image/gif。<br>
5. 存储在$_FILES["file"]["error"]变量中的值将是任何与文件上载相关的错误代码。这是在PHP4.2.0中增加的新特性。<br>
**error分别提供了一些数组常量：**<br>
+ 0:表示没有发生错误。<br>
+ 1:表示上载文件的大小超出了约定值。文件大小的最大值是PHP配置文件中指定的，该指令是upload_max_filesize。<br>
+ 2:表示上载文件大小超出了HTML表单的MAX_FILE_SIZE元素所指定的最大值。<br>
+ 3:表示文件只被部分上载。<br>
+ 4:表示没有上载任何文件。<br>

**3>上传函数**
PHP还提供了两个专门用于文件上传过程的函数：is_uploaded_file()和move_uploaded_file()。
```
//确定是否上传文件
if (is_uploaded_file($_FILES["file"]["tmp_name"])) {
    echo '已经上传到临时文件夹';
    $filename = "upload".time()."png";
    //移动上传文件(将文件移动到指定文件夹)
    if (!move_uploaded_file($_FILES["file"]["tmp_name"],img/,$filename)) {
        echo '移动失败';
        exit;
    }else{
        echo "移动成功";
    }
} else {
    echo '失败';
}
```

### 二、文件目录<br>
将相关的数据组织为文件和目录等实体，程序员需要有一种方法来获得关于文件和目录的重要细节，如位置、大小、最后修改时间、最后访问时间和其他确定信息。<br>
**1>目录操作**<br>
+ 获得当前文件路径
    1. \__FILE__
        当前文件路径+当前文件名
    2. \__DIR__
        当前文件路径
    3. dirname(\__FILE__)
        当前文件路径
    4. basename(\__FILE__)
        当前文件名
    5. pathinfo(\__FILE__)
        关于路径的信息的关联数组，其中包括：目录名、基本名和扩展名
    6. realpath(\__FILE__)
        绝对路径（前提 在当前项目下确实存在这个文件 才能获取绝对路径，只能读当前文件中对应的文件路径信息）
> \__FILE__ 和 \__DIR__是针对当前文件，dinrname()和basename()是针对任意文件路径

**2>磁盘、目录和文件大小计算**<br>
1. 文件大小
    filesize($path)
    计算该文件大小，字节为单位。
```
$file = __FILE__;
echo round(filesize($file)/1024).'KB';
```
2. 磁盘可用空间大小
    disk_free_space()
    指定的目录所在磁盘分区的可用空间。
```
$drive = 'C:';
echo round(disk_free_space($drive)/1024/1024/1024,2).'GB';
```
3. 磁盘的总容量
    disk_total_space()
    指定的目录所在磁盘分区的总容量。
```
$drive = 'C:';
echo round(disk_total_space($drive)/1024/1024/1027,2).'GB';
```

