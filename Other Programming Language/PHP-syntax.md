## PHP语言概述
HTML内嵌式脚本语言，PHP:Hypertext Preprocessor(超级文本预处理)
javascript是动态脚本语言，基于对象，采取事件驱动，。
html静态超文本标记语言
## 语法规则
<?php 开始，以 ?>      包含 HTML 标签和一些 PHP 脚本代码。
PHP 中的每个代码行都必须以分号结束。分号是一种分隔符，用于把指令集区分开来。
通过 PHP，有两种在浏览器输出文本的基础指令：echo和print。

### 变量
#### 变量规则：
* 变量以 $ 符号开始，后面跟着变量的名称
* 变量名必须以字母或者下划线字符开始
* 变量名只能包含字母数字字符以及下划线（A-z、0-9 和 _ ）
* 变量名不能包含空格
* 变量名是区分大小写的（$y 和 $Y 是两个不同的变量）
* 先声明，后赋值

#### 数据类型
* String（字符串）, 
* Integer（整型）, 
* Float（浮点型）,
* Boolean（布尔型）, 
* **Array（数组）**, 
* Object（对象）, 
* NULL（空值）

##### 对比 java的数据类型
整型（byte2^8, short2^16, int2^32 40亿, long2^64,），
浮点型(float,double)，
字符型（char）,
布尔型，
集合，
类
#### 预定义变量
$_SERVER
$_ENV
$_COOKIE
$_GET
$_POST
$_FILES
$_REQUEST
$_SESSION
##### 对比javascript的预定义变量

##### 字符串String
###### 引用字符串常量
+ 变量差值 “I am $name” 单引号不插值
+ 单引号     单引号不插值，只有转义字符\'  \\
+ 双引号     转义字符\n   \t  \"
+ here文档
###### 输出字符串
+ echo      是语言结构
+ printf()   格式化 %修饰符，如%%   %d
+ print()
###### 特殊字符串函数
+ strlen()
+ trim()
+ strtolower()
##### 编码和转义
$string = htmlentities("I'm don")

| 转义前 | 转义后  |
| --- | --- |
| space | \&nbsp;  |
| & | \&amp; |
| " | \&quot; |
| < | \&lt; |
| > | \&gt; |

+ HTML
+ URL
+ SQL
##### 处理和查找字符串

+ sustr()
+ substr_count()
+ substr_replace()
+ strrev()
+ str_repeat()
+ str_pad()
分解字符串
+ explode()
+ implode = join()
+ strtok()
查找字符串
+ strpos()
+ strrpos()
+ strstr()  stristr()   strchr()  strrchr()
+ parse_url()
##### 正则表达式
+ preg_match(reg,  string)

#### 变量作用域
PHP 有四种不同的变量作用域：
* local        函数内变量
* global      全局变量     函数内访问全局变量需要global关键字
* static
* parameter        方法参数变量

### 常量 
默认是全局变量，可以在整个运行的脚本的任何地方使用。
设置常量，使用 define() 函数，函数语法如下：
```
bool define ( string $name , mixed $value [, bool $case_insensitive = false ] )
```
该函数有三个参数:

* name：必选参数，常量名称，即标志符。
* value：必选参数，常量的值。
* case_insensitive ：可选参数，如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的。

命名空间use   类似于import    别名/导入
PHP 命名空间支持 有两种使用别名或导入方式：为类名称使用别名，或为命名空间名称使用别名。

### 运算符、表达式和语句
* 算术运算符
* 赋值运算符
* 自运算符
* 自增自减运算符
* 字符串运算符        .
* 比较
* 逻辑
* 位
* 执行运算符
![4ea62c0a0d6ca90690f9f8cd699030f8.png](en-resource://database/8093:1)
![dfe93267b1b11bcef60a5abe4675aa90.png](en-resource://database/8095:1)

注释
```
//
#
/*  */
```
### 顺序流程

* 有序
* 条件分支
* 循环

### 函数
调用该对象的成员方法或成员变量   A::B表示某命名空间下类A的函数B        函数可以不用写在类下，可以直接写在脚本里

#### 名称解析
遵循下列规则：
对完全限定名称的函数，类和常量的调用在编译时解析。例如 new \A\B 解析为类 A\B。
所有的非限定名称和限定名称（非完全限定名称）根据当前的导入规则在编译时进行转换。例如，如果命名空间 A\B\C 被导入为 C，那么对 C\D\e() 的调用就会被转换为 A\B\C\D\e()。
在命名空间内部，所有的没有根据导入规则转换的限定名称均会在其前面加上当前的命名空间名称。例如，在命名空间 A\B 内部调用 C\D\e()，则 C\D\e() 会被转换为 A\B\C\D\e() 。
非限定类名根据当前的导入规则在编译时转换（用全名代替短的导入名称）。例如，如果命名空间 A\B\C 导入为C，则 new C() 被转换为 new A\B\C() 。
在命名空间内部（例如A\B），对非限定名称的函数调用是在运行时解析的。例如对函数 foo() 的调用是这样解析的：
在当前命名空间中查找名为 A\B\foo() 的函数
尝试查找并调用 全局(global) 空间中的函数 foo()。

在命名空间（例如A\B）内部对非限定名称或限定名称类（非完全限定名称）的调用是在运行时解析的。下面是调用 new C() 及 new D\E() 的解析过程： new C()的解析:
在当前命名空间中查找A\B\C类。
尝试自动装载类A\B\C。
new D\E()的解析:
在类名称前面加上当前命名空间名称变成：A\B\D\E，然后查找该类。
尝试自动装载类 A\B\D\E。
为了引用全局命名空间中的全局类，必须使用完全限定名称 new \C()。

#### 系统（内置）函数

#### 可变参数

#### 参数按值传递，和按引用传递
按引用传递选择参数列表的变量名前加“&”


### 数组类
+ 索引数组   键值是整数
+ 关联数组   键值是字符串
php的数组可以存放不同数据类型的数据，如int, String。
索引数组是存储键为从0开始的连续整数的关联数组。
数组按插入顺序存储，并实现遍历。但排序函数可改变元素顺序。


#### 在数组中存储数据
$size = array('S', 'M', 'L', 'XL');
```
$info = array( 
        'name' => 'Don',    '
        age' => 10);
echo $info['age'];
```
$numbers = range(2,5);  ===  $numbers = array(2,3,4,5)

#### 多维数组

#### 析取多个值
$person = array("Fred", 35,, "Betty");
+ list($name, $age, $wife) = $person;
+ array_chunk(array, size)                   //把数组划分为小数组
+ array_slice()                                    //切割数组
+ array_keys()
+ array_values()                                    //
+ array_key_exists(key, array)
+ array_splice(array, start [,length [, replacement]]);    //删除和插入元素
##### 数组和变量间的转换

#### 遍历数组
+ foreach
```
foreach($array as $value) {  
    echo $value;
}
foreach($array as $key ==>$value) {  
    if(empty($array[$key])) 
        return false;
}
```
+ 迭代器函数
        * current()
        * reset()
        * next()
        * prev()
        * end()
        * each()
```
while (list($c1,$c2) = each($ages)) {  
    echo("<tr><td>$c1</td><td>$c2</td></tr>\n");}
```
            
+ for循环
+ array_walk(array, callable， $args_array)
+ in_array(to_find, array [, strict]);       == array_search()

#### 排序sorting
+ 按键排序
+ 不改变键的按值排序
+ 改变值的按键排序
```
sort(array [, sort_function($a, $b)])

function sort_function($a, $b){
    return ($a == $b) ? 0 : ($a<$b) ? -1 : 1);
}
```
| 效果| 升序 | 降序 |
| --- | --- | --- |
| 按键排序 | sort() | rsort() |
| 不改变键的按值排序 |asort()  | arsort() |
| 改变值的按键排序 |ksort()     |  krsort |
+ array_multisort()
+ array_reverse()
+ shuffle();   随机
#### 使用数组
+ array_sum()
+ array_merge()
+ array_diff()
+ array_filter()
##### 集合

##### 堆栈

### 6.对象
#### 声明类
+ 方法
+ 属性
+ 继承
+ 抽象类和接口
+ 关键字

### 7.web技术
Request:  在html里submit提交请求request表单数据到服务器上
```
<?php 
    $_SERVER['PHP_SELF'] 
?>
```
Response: 服务器返回数据到页面
```
<?php 
    if (array_key_exists('s', $_GET)) {   
        $description = join(" ", $_GET['attributes']);   
        echo "You have a $description personality."; }
?>
```
#### 处理表单
表单有函数$post $get
```
action="chunkify.php"
```
php页面可以直接做MVC的V视图层。当然还是需要和html页面结合起来，通过ajax请求修改页面的部分内容。
+ 字处理页面
```
<?php 
    $_SERVER['PHP_SELF'] 
?>
```
表单粘性表单

#### 在php里面写html代码


#### 文件上传，文件操作

#### 不同的内容类型
+ 重定向  header("Location:http://www.example.com")
+ 过期
+ 认证


#### <u>维护http状态</u> 
setcookie(name [,value]) 包含多个字段的字符串  colors.php

##### <u>Cookie</u>

##### <u>会话Session</u>

### 数据库


### 框架ThinkPHP


## PHP环境的集成软件
他是一个集成环境，包括web server Apache，数据库，还有php的环境
+ xampp 7.2.11  Apache 2.4.35+MySQL 10.1.36+PHP7.2.11+PERL+ phpMyAdmin 4.8.3

+ wamp 3.1.4  Apache,MySQL, PHP

[windows上搭载PHP环境](https://blog.csdn.net/qq_36172505/article/details/79615043)
安装WarmpServe 集成php环境

需要明白安装的apache主目录，将项目代码拷贝到apache程序的/htdocs/目录下

### Windows搭载PHP环境运行HelloWorld代码
+ php -version能保证php脚本能够解释运行

### web server: Apache
+ web环境：html5，能够在浏览器上访问。
[Apache与Apache Tomcat的区别](https://blog.csdn.net/sky198989/article/details/81875015)


## IDE集成开发工具的配置
#### 配置Apache

#### 调试工具：xdebug
[安装Xdebug调试php代码](https://www.jetbrains.com/help/phpstorm/configuring-xdebug.html)
