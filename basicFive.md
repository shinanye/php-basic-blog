##php入门五<br>
###一、cookie<br>
**1>cookie介绍**
>Cookie是存储在客户端浏览器中的数据，可以通过Cookie来跟踪与存储用户数据。一般情况下，Cookie通过HTTP headers从服务端返回到客户端。多数web程序都支持对Cookie的操作，因为Cookie是存在于HTTP的标头之中。<br>
在PHP通过setcookie函数对Cookie进行设置，任何从浏览器发回的Cookie，PHP都会自动的将他存储在$_COOKIE的全局变量之中，因此我们可以通过$_COOKIE['key']的形式来读取某个Cookie值。<br>
使用会话Session时通常使用Cookie来存储会话id来识别用户，Cookie具备有效期，当有效期结束之后，Cookie会自动的从客户端删除。<br>

**2>设置cookie**<br>
setcookie()<br>
意义：用于设置cookie，在setcookie()函数中一个有7个参数(常用的参数只有5个)。<br>
语法：setcookie(name,value,expire,path,domain,secure,httponly)<br>
返回值：如果在调用此函数之前存在输出，则 setcookie（）将失败并返回FALSE。如果 setcookie（）成功运行，它将返回TRUE。这并不表示用户是否接受了Cookie。<br>
>参数：<br>
name:<br>
Cookie的名称,通过$_COOKIE['name']访问。<br>
value:<br>
Cookie的值<br>
expire：<br>
Cookie到期的时间。这是一个Unix时间戳，单位是秒。你可以用time（）函数加上你希望它过期之前的秒数来设置它。或者你可以使用[mktime()](http://php.net/manual/en/function.mktime.php)。如果设置为0或省略，则cookie将在会话结束时过期（当浏览器关闭时），默认为0。<br>
path:<br>
（有效路径）如果路径设置为'/'，则整个网站都有效，如果设置为 '/ foo /'，则cookie将仅在/foo/目录和所有子目录（如/ foo / bar / of）中可用domain。<br>
domain:<br>
（cookie可用的域）默认整个域名都有效，要使cookie可用于整个域（包括它的所有子域），只需将该值设置为域名（本例中为'example.com'）即可。<br>
secure：<br>
表示该cookie只能通过客户端的安全HTTPS连接进行传输。设置TRUE时，只有存在安全连接时才会设置cookie。在服务器端，程序员只能在安全连接上发送这种cookie（eg：相对于$ _SERVER [“HTTPS”]）。<br>
httponly:<br>
当[httponly='TRUE']时cookie只能通过HTTP协议访问。<br>
>因为Cookie是通过HTTP标头进行设置的，所以也可以直接使用header方法进行设置。<br>
header("Set-Cookie:cookie_name=value");<br>
setcookie("TestCookie", $value, time()+3600, "path/", "baidu.com"); //设置路径与域<br>

**3>Cookie的删除与过期时间**<br>
在php中没有指定删除Cookie的函数,而是通过设置cookie的过期时间设置到当前时间之前，则该cookie会自动失效从而到达删除该cookie。<br>

**4>判断Cookie是否为空**<br>
isset()<br>
意义：判断某一cookie是否存在。<br>
返回值：true/false
```
setcookie("name","ljp");
if( isset( $_COOKIE["name"])){
    echo  $_COOKIE["name"];

}else{
    echo "不存在";
}
```
###Session与cookie的异同
>cookie<br>
1、将数据存储在客户端，建立起用户与服务器之间的联系，通常可以解决很多问题，但是cookie仍然具有一些局限：<br>
2、cookie相对不是太安全，容易被盗用导致cookie欺骗<br>
3、单个cookie的值最大只能存储4k<br>
4、每次请求都要进行网络传输，占用带宽<br>

>session<br>
1、将用户的会话数据存储在服务端，没有大小限制，<br>
2、通过一个session_id进行用户识别，PHP默认情况下session id是通过cookie来保存的<br>
```
//开始使用session
session_start();
//设置一个session
$_SESSION['test'] = time();
//显示当前的session_id
echo "session_id:".session_id();
echo "<br>";

//读取session值
echo $_SESSION['test'];

//销毁一个session
unset($_SESSION['test']);
echo "<br>";
var_dump($_SESSION);
```
**1>session使用**
>先执行session_start方法开启session，然后通过全局变量$_SESSION进行session的读写。默认情况下，session是以文件形式存储在服务器上的，因此当一个页面开启了session之后，会独占这个session文件，这样会导致当前用户的其他并发访问无法执行而等待。可以采用缓存或者数据库的形式存储来解决这个问题。<br>
session会自动的对要设置的值进行encode与decode，因此session可以支持任意数据类型，包括数据与对象等。<br>
```
session_start();
$_SESSION['ary'] = array('name' => 'jobs');
$_SESSION['obj'] = new stdClass();
var_dump($_SESSION);
```
**2>删除和销毁session**<br>
>unset()<br>
在PHP用unset函数删除某个session值，删除后就会从全局变量$_SESSION中去除，无法访问。
```
session_start();
$_SESSION['name'] = 'jobs';
unset($_SESSION['name']);
echo $_SESSION['name']; //提示name不存在
```
>session_destroy()<br>
session_destroy函数会删除所有数据，但是session_id仍然存在。
```
session_start();
$_SESSION['name'] = 'jobs';
$_SESSION['time'] = time();
session_destroy();
```
>特别注意：session_destroy()并不会立即的销毁全局变量$_SESSION中的值，只有当下次再访问的时候，$_SESSION才为空，因此如果需要立即销毁$_SESSION，可以使用unset()。<br>

**3>使用session来存储用户的登陆信息**
>登录信息既可以存储在sessioin中，也可以存储在cookie中，他们之间的差别在于session可以方便的存取多种数据类型，而cookie只支持字符串类型，同时对于一些安全性比较高的数据，cookie需要进行格式化与加密存储，而session存储在服务端则安全性较高。<br>
```
<?php
session_start();
//假设用户登录成功获得了以下用户数据
$userinfo = array(
    'uid'  => 1011,
    'name' => 'spark',
    'email' => '1637167XX@qq.com',
    'sex'  => 'F'
);
header("content-type:text/html; charset=utf-8");

/* 将用户信息保存到session中 */
$_SESSION['uid'] = $userinfo['uid'];
$_SESSION['name'] = $userinfo['name'];
$_SESSION['userinfo'] = $userinfo;

//* 将用户数据保存到cookie中的一个简单方法 */
$str =serialize($userinfo); //将用户信息序列化
setcookie('userinfo', $str);
```
了解更多关于序列化[serialize](http://php.net/manual/en/function.serialize.php);