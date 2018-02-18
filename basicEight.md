##PHP入门八<br>
###图像、图形库的操作<br>
**1>GD库简介**
>GD指的是Graphic Device，PHP的GD库是用来处理图形的扩展库，通过GD库提供的一系列API，可以对图像进行处理或者直接生成新的图片。<br>
PHP除了能进行文本处理以外，通过GD库，可以对JPG、PNG、GIF、SWF等图片进行处理。GD库常用在图片加水印，验证码生成等方面。<br>
PHP默认已经集成了GD库，只需要在安装的时候开启就行。<br>

>####创建图像的一般流程<br>
1. 设定标头，告诉浏览器你要生成的MIME类型<br>
2. 创建一个图像区域，以后的操作都将基于此图像区域<br>
3. 在空白图像区域绘制填充背景<br>
4. 在背景上绘制图形轮廓输入文本<br>
5. 输出最终图形<br>
6. 清除所有资源<br>
7. 其他页面调用<br>

```
header("content-type: image/png");
$img=imagecreatetruecolor(100, 100);
$red=imagecolorallocate($img, 0xFF, 0x00, 0x00);
imagefill($img, 0, 0, $red);
imagepng($img);
imagedestroy($img);
```
1. 绘制线条<br>
imageline()<br>
语法：imageline($img, $sX, $sY, $eX, $eY, $col);

2. 绘制圆<br>
[imagearc()](http://php.net/manual/zh/function.imagearc.php)
语法：imagearc ($image ,$cx ,$cy ,$w ,$h ,$startAngle,$endAngle,$color )
```
$img = imagecreatetruecolor(200, 200);
// 分配颜色
$red = imagecolorallocate($img, 255, 0, 0);
$white = imagecolorallocate($img, 255, 255, 255);
//背景填充白色
imagefill($img,0,0,$white);
// 画一个红色的圆
imagearc($img, 100, 100, 150, 150, 0, 360, $red);
imagepng($img);
// 释放内存
imagedestroy($img);
```

3. 绘制矩形<br>
[imagerectangle](http://php.net/manual/zh/function.imagerectangle.php)
语法：imagerectangle ($image ,$x1 ,$y1 ,$x2 ,$y2 ,$col)
```
$img = imagecreatetruecolor(200, 200);
// 分配颜色
$red = imagecolorallocate($img, 255, 0, 0);
$white = imagecolorallocate($img, 255, 255, 255);
imagefill($img,0,0,$white);
// 画一个红色的矩形
imagerectangle ($img,50,50,100 ,100 ,$red);
imagepng($img);
// 释放内存
imagedestroy($img);
```

4. 绘制文字<br>
意义：绘制文字<br>
语法1：[imagestring ($image ,$font ,$x , $y ,$s ,$col )](http://php.net/manual/zh/function.imagestring.php)<br>
语法2：[imagettftext($image,$size, $angle,$x,$y,$color,$fontfile, $text)](http://php.net/manual/zh/function.imagettftext.php)
```
header("content-type: image/png");
//imagestring字体大小设置不了
$img = imagecreatetruecolor(100, 100);
$red = imagecolorallocate($img, 0xFF, 0x00, 0x00);
imagestring($img, 5, 10, 10, "Hello world", $red);
imagepng($img);
imagedestroy($img);

$img1=imagecreatetruecolor(200,200);
$red=imagecolorallocate($img1,255,0,0);
$white=imagecolorallocate($img1,255,255,255);
imagefill($img1,0,0,$red);
$font="C:\Windows\Fonts\simhei.ttf";
imagettftext($img1,23,0,100,100,$white,$font,"你好吗");
imagepng($img1);
imagedestroy($img1);
```

5. 绘制噪点<br>
意义：绘制噪点<br>
语法：imagesetpixel($image,$x,$y,$col)
```
//绘制10个噪点
for($i=0;$i<10;$i++) {
  imagesetpixel($img, rand(0, 100) , rand(0, 100) , $black); 
  imagesetpixel($img, rand(0, 100) , rand(0, 100) , $green);
}
```

>输出图像文件<br>
通过imagepng可以直接输出图像到浏览器，通过指定路径参数将图像保存到文件中
1. [imagepng()](http://php.net/manual/zh/function.imagejpeg.php) <br>
意义：将图片保存成png格式<br>
语法：imagepng($img,$filename)<br>
2. [imagejpeg()](http://php.net/manual/zh/function.imagejpeg.php)  <br>
意义：将图片保存成jpeg格式<br>
语法：imagepng($img,$filename,$quality)<br>
3. [imagegif()](http://php.net/manual/zh/function.imagegif.php)  <br>
意义：将图片保存成gif格式<br>
语法：imagegif($img,$filename)

>案例：
1. [随机产生验证码（php）](https://github.com/shinanye/validate/blob/master/identityingCode.html)<br>
2. [给图片添加水印](https://github.com/shinanye/validate/blob/master/Dewatermark.html) 
