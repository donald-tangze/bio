## Jstat 

 find java bin directory

~~~shell
./jps
./jstat -gc <745500> 

./jmap heap dump 堆dump文件
https://www.baeldung.com/linux/jmap-unable-to-open-socket-file-heap-dump
~~~



![一次线上JVM Young GC调优，搞懂了这么多东西！](https://static001.geekbang.org/infoq/42/429931485f037254d7d0eca999661bee.png)

```
S0C    S1C    S0U    S1U      EC       EU        OC         OU       MC     MU    CCSC   CCSU   YGC     YGCT    FGC    FGCT     GCT   
104832.0 104832.0 55366.2  0.0   838912.0 61299.2  1048576.0   633907.1  1231264.0 1155872.4 166828.0 155212.4    216   50.384  14      5.629   56.013
104832.0 104832.0 55366.2  0.0   838912.0 63247.4  1048576.0   633907.1  1231264.0 1155872.4 166828.0 155212.4    216   50.384  14      5.629   56.013
104832.0 104832.0 55366.2  0.0   838912.0 65403.0  1048576.0   633907.1  1231264.0 1155872.4 166828.0 155212.4    216   50.384  14      5.629   56.013
104832.0 104832.0 55366.2  0.0   838912.0 67588.1  1048576.0   633907.1  1231264.0 1155872.4 166828.0 155212.4    216   50.384  14      5.629   56.013
104832.0 104832.0 55366.2  0.0   838912.0 69781.8  1048576.0   633907.1  1231264.0 1155872.4 166828.0 155212.4    216   50.384  14      5.629   56.013
104832.0 104832.0 55366.2  0.0   838912.0 71413.0  1048576.0   633907.1  1231264.0 1155872.4 166828.0 155212.4    216   50.384  14      5.629   56.013
104832.0 104832.0 55366.2  0.0   838912.0 73265.4  1048576.0   633907.1  1231264.0 1155872.4 166828.0 155212.4    216   50.384  14      5.629   56.013
104832.0 104832.0 55366.2  0.0   838912.0 75538.1  1048576.0   633907.1  1231264.0 1155872.4 166828.0 155212.4    216   50.384  14      5.629   56.013


```

S0：Heap上的 Survivor space 0 段空间大小KB
S1：Heap上的 Survivor space 1 段空间大小KB

S0U：Heap上的 Survivor space 0 段已使用空间大小KB

S1U：Heap上的 Survivor space 1 段已使用空间大小KB

EC：显示现在Eden空间大小KB

EU：显示现在Eden已用空间大小KB

OC：显示现在old空间大小KB

OU：显示现在old已用空间大小KB

PC：显示现在持久带空间大小KB

PU：显示现在持久带已用空间大小KB

YGC：从程序启动到采样时发生Young GC的次数
YGCT：Young GC所用的时间(单位秒)
FGC：从程序启动到采样时发生Full GC的次数
FGCT：Full GC所用的时间(单位秒)



## 设置tomcat启动内存设置

```
https://blog.csdn.net/zc19921215/article/details/83029952

JAVA_OPTS="$JAVA_OPTS -Xmx512M -Xmx1024M"
 
 -Xms 128M 设定JVM运行的最小内存
 -Xmx 256M 设定JVM运行的最大内存
 -XX:MaxNewSize  定义新生代最大内存空间
 -XX:MaxPermSize 定义持久代最大内存空间
 
-XX:+PrintGC 输出GC日志 
-XX:+PrintGCDateStamps：打印 GC 发生的时间戳。
-XX:+PrintTenuringDistribution：打印 GC 发生时的代龄信息。
-XX:+PrintGCApplicationStoppedTime：打印 GC 停顿时长
-XX:+PrintGCApplicationConcurrentTime：打印 GC 间隔的服务运行时长
-XX:+PrintGCDetails：打印 GC 详情，包括 GC 前/内存等。
-Xloggc:../gclogs/gc.log.date：指定 GC log 的路径
```

GC Roots一般都是些堆外指向堆内的引用，例如：

1. JVM栈中引用的对象

2. 方法区中静态属性引用的对象

3. 方法区中常量引用的对象

4. 本地方法栈中引用的对象 

   Minor GC:

       对于复制算法来说，当年轻代Eden区域满的时候会触发一次Minor GC，将Eden和From Survivor的对象复制到另外一块To Survivor上。
       
       注意：如果某个对象存活的时间超过一定Minor gc次数会直接进入老年代，不在分配到To Survivor上(默认15次，对应虚拟机参数 -XX:+MaxTenuringThreshold)。

    
   
   
   
   


   Full GC:

   用于清理整个堆空间。它的触发条件主要有以下几种：

   显式调用System.gc方法(建议JVM触发)。
   方法区空间不足(JDK8及之后不会有这种情况了，详见下文)
   老年代空间不足，引起Full GC。这种情况比较复杂，有以下几种：



netstat -aof | findstr :8080

netstat -tunlp | grep 8080

## Jmap

jmap -dump:live,format=b,file=paymentHub_server.hprof   13427



![image-20221206051406627](C:\Users\donald\AppData\Roaming\Typora\typora-user-images\image-20221206051406627.png)

[JVM内存分析：Tomcat内存泄漏](https://flytreeleft.org/the-jvm-dump-analyse-for-tomcat-memory-leak/#%E6%A1%88%E4%BE%8B%E5%88%86%E6%9E%90)

   After manually trigger GC on 02-20, the server memory have decreased to 35%-40%. 

  After further investigation in our internal server, when we were deploying new server, used new package to override old package without restart whole tomcat, old package would destroyed      but memory still was occupied. 

  Last week to save time I didn't restart whole tomcat, then some old destroyed application would occupy some memory. Even full GC can not collect those part memory.

  I will keep an eye on our memory and GC in server app1.
