## iterm2使用

### 常用功能

* 快，稳定；

* 支持多终端，比如可以方便地水平和纵向分屏，有 tab 等；
* 方便配置字体颜色等；
* 方便管理常用 SSH 的登录。

### 用iterm 2 软件远程登录ssh

通过profile管理会话session

* 方法一：iterm的trigger,设置
* 方法二：expect脚本，自动输入用户名宇密码

ssh 用户名@IP地址 -p 端口

\> ssh root@39.x.x.xx -p 22  BJtz



##  root账户与don2021账户

苹果macbook有root账户

don2021没权限时，通过sudo切换执行命令command获得privilege



## mac上安装intellij idea

#### macbook安装jdk  

1.手动下载安装包exe，会自动安装到/Library/Java/JavaVirtualMachines目录；

2.在idea里download JDK...，会自动安装到用户目录 /home directory /Users/don2021/Library/ 

![image-20220125213048191](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x0tqh8bj20rw0g2jsq.jpg)



是否需要配置环境变量 JAVA_HOME;

> 15.0.2 (x86_64) "OpenJDK 15.0.2" /Users/don2021/Library/Java/JavaVirtualMachines/openjdk-15.0.2/Contents/Home
> 1.8.0_221 (x86_64)  "Java SE 8"      /Library/Java/JavaVirtualMachines/jdk1.8.0_221.jdk/Contents/Home

2.在idea的project Settings -> Project -> SDK 选择os已安装的jdk

![安装JDK](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x0o8ndhj21rd0u0n6u.jpg)

#### 安装maven

Module 多Module

Project Settings -> Modules 

#### preferences or settings

Command +  ,   mac叫preferences, windows叫settings

#### Editor window   edit and debug code: 

Zen Mode;     Split window  Vertically horizontaly;     Find/Replaces

####  Project Window +  tool window

project scope: acutal directory, default

package scope: narrow down package    

project Files: 不显示外部jar包，和配置文件

shortcut快捷键  [Default macOS keymap](https://resources.jetbrains.com/storage/products/intellij-idea/docs/IntelliJIDEA_ReferenceCard.pdf)

#### generater boilerplate code, reformat(格式化), navigate, refactor, live template, scr

#### build Java Project, 

编译compile source code into bit code,  打包package. that's package into jar 

![image-20220125214009457](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x0ltdmoj21tc0gumzl.jpg)

Structure of a java projec

* .idea  .gitignore版本控制的目录    modules.xml 单个还是多个maven module    workspace.xml开发工具的设置   
* out  class文件夹
* src   源文件
* External libraries 外部依赖Jar包
* .iml  模块，项目配置

## mac上安装vs code

VS CODE适合多种语言的editor，powerful, extensible 尽管在java的编译，打包集成功能上不如intellij idea.

> 启动软件  command + space, 输入code

![image-20220126160234018](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x0jcq96j210k074jrp.jpg)

### 0.界面：

view bar; directory explorer;  editor area; status bar; menu(top, edit command)

### 1.设置preferences

![image-20220126160112080](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x0grvelj224a0q643z.jpg)![image-20220126160112261](/Users/don2021/Library/Application Support/typora-user-images/image-20220126160112261.png

* Font size
* set keyboard shortcut

* icon and color Themes 

  > blue box means variables; 

* 

### 2.快捷键 shortcuts

>  摆脱鼠标控制，手不离开键盘

| shortcut        | Meaning                                                |
| --------------- | ------------------------------------------------------ |
| cmd + shift + p | command palette根据自然语言搜索全部命令，包括extension |
| cmd + p         | go to file                                             |
| cmd + d + z     | Zen mode                                               |
|                 |                                                        |
|                 |                                                        |
|                 |                                                        |

![image-20220126160722855](https://tva1.sinaimg.cn/large/e6c9d24egy1h39wzrcn4sj20ec0aaq33.jpg)

### 3.插件extensions

Abundant extension Marketplace. install or uninstall, update

### 4.basic Editing

cmd + c means copy current line when no text selected 

cmd + x means cut current line when no text selected 

cmd+[ means line indent to the right

cmd+< means line indent to the left

opt+shift+F means format current document

cmd+K+F  means format selection text

cmd+i means select current line

opt+up/down  move lines up or down

### 5.Advanced Editing

Multiple selection

json and schema

Web code editing

* Files and folders, and projects

> Every folder is a project, title ,open  editors,  single click file in explorer, preview mode. double click, really open,
>
> reveal in Finder;    open in integrated Terminal

![image-20220126164754669](https://tva1.sinaimg.cn/large/e6c9d24egy1h39wzx1itmj20p40g8gna.jpg)

* finding and replacing

  

### 6.Terminal: 内嵌bash shell终端

ctrl+` means integrated teminal under menu View

Excute the written bash shell script

### 7. Code completion or code hinting IntelliSense

Out of box内置支持html, css, js, typescript,

支持java需要另外安装extension插件

ctrl + space trigger代码自动完成