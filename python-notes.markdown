#### github python学习区
https://blog.csdn.net/u010670689/article/details/51911240
书名：《Python程序设计入门到实战 》台湾人写的
[python语法](http://www.runoob.com/python/python-basic-syntax.html)
[python3语法](http://www.runoob.com/python3/python3-basic-syntax.html)

python软件包在线仓库
| Module/package |  Function  |
| --- | --- |
|Requests|  http请求  |
|os.path(built-in)  glob/ os.walk/ os.system/ shutil | 操作文件、目录，磁盘操作  |
|mysql-python  | 连接数据库 |
|BeautifulSoup |提取网站数据 |
|Selenium |   操作浏览器javascript |
|Django/Flask    | Web app  |

#### 换行符，缩进
换行和空格是有意义的，必须统一
java有分号“;”  有大括号{}控制模块

python用缩进写模块，没有大括号{}
换行  一般以新行作为为语句的结束符。使用斜杠（ \）将一行的语句分为多行显示。语句中包含 [], {} 或 () 括号就不需要使用多行连接符。   

#### 数据类型    
**python**有Numbers（数字）整型，浮点数型，空值(NONE)、String（字符串）、<u>List（列表）、Tuple（元组）、Dictionary（字典）</u>
+ 字符串
索引，从0开始
+ 列表
就是集合，数组。列表用 [ ] 标识，是 python 最通用的复合数据类型。
+ 元组
是另一个数据类型，类似于List（列表）
元组用"()"标识。内部元素用逗号隔开。但是元组不能二次赋值，相当于只读列表。
+ 字典(dictionary)
是除列表以外python之中最灵活的内置数据结构类型。列表是有序的对象结合，字典是无序的对象集合。类似“Map”
两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。
字典用"{ }"标识。字典由索引(key)和它对应的值value组成。
+ Set（集合）
集合（set）是一个<u>无序不重复</u>元素的序列。
基本功能是进行成员关系测试和删除重复元素。
可以使用大括号 { } 或者 set() 函数创建集合，注意：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。

#### 标识符
>由字母、数字、下划线组成。不能以数字开头。区分大小写。
>以单下划线开头foo 的代表不能直接访问的类属性；
>以双下划线开头的 __foo 代表类的私有成员；
>以双下划线开头和结尾的 __foo__ 代表 Python 里特殊方法专用的标识，如 __init__() 代表类的构造函数。

#### Python注释
python中单行注释采用 # 开头。

#### Python空行
函数之间或类的方法之间用空行分隔，表示一段新的代码的开始。空行与代码缩进不同，空行并不是Python语法的一部分。书写时不插入空行，Python解释器运行也不会出错。但是空行的作用在于分隔两段不同功能或含义的代码，便于日后代码的维护或重构。

#### Python 运算符


#### Python 函数
##### 函数代码块以 def 关键词开头，后接函数标识符名称和圆括号()。
任何传入参数和自变量必须放在圆括号中间。圆括号之间可以用于定义参数。
函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
函数内容以冒号起始，并且缩进。
return [表达式] 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回 None。

#### import与 from...import
在 python 用 import 或者 from...import 来导入相应的模块。
将整个模块(somemodule)导入，格式为： import somemodule
从某个模块中导入某个函数,格式为： from somemodule import somefunction
从某个模块中导入多个函数,格式为： from somemodule import firstfunc, secondfunc, thirdfunc
将某个模块中的全部函数导入，格式为： from somemodule import *
