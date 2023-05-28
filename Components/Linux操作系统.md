# 操作系统

参考资料：

[趣谈Linux操作系统](https://time.geekbang.org/column/article/97030)

《深入理解计算机系统》

[趣谈课程总览图](https://mp.weixin.qq.com/s/TkOb__jEcw8ZOfPk9EhZeQ)

## 综述

### 系统调用 

详情看第05节，第09节

系统调用（System Call）是操作系统为在用户态运行的进程与硬件设备进行交互提供的一组接口。当用户进程需要发生系统调用时，CPU 通过软中断切换到内核态开始执行内核系统调用函数。我们可以有三种方法使用系统调用：

1. 通过 int 指令陷入：通过软中断指令int 0x80 来陷入内核态
2. 使用 syscall 直接调用， glibc没有封装某个系统调用时可以
3. 通过 glibc 提供的API调用，最方便的方法

![img](https://static001.geekbang.org/resource/image/ff/f0/ffb6847b94cb0fd086095ac263ac4ff0.jpg)

> - 进程管理的系统调用
>
> - - 第10节会使用这些系统调用创建进程
>   - 第11节会使用这些系统调用创建线程
>   - 第18节会解析进程创建的系统调用在内核里面是如何实现的
>   - 第19节会解析线程创建的系统调用在内核里面是如何实现的
>
> - 内存管理的系统调用
>
> - - 第20节会使用这些系统调用申请内存，主要的两种方式brk和mmap
>   - 第22节会解析使用brk系统调用申请内存的时候在内核是如何实现的
>   - 第25节会解析使用mmap系统调用申请内存的时候在内核是如何实现的
>
> - 文件管理的系统调用
>
> - - 第27节会使用这些系统调用操作文件，主要是打开，读，写
>   - 第29节会解析打开文件的系统调用在内核是如何实现的
>   - 第30节会解析读写文件的系统调用在内核是如何实现的
>
> - 信号处理的系统调用
>
> - - 第37节和第38节会介绍信号处理系统调用在内核是如何实现的
>
> - 进程间通信
>
> - - 第36节会讲如何使用命令或者系统调用来使用这些进程间通信机制
>   - 第39节会介绍管道系统调用在内核是如何实现的
>   - 第40节到第42节会介绍IPC的系统调用在内核是如何实现的
>
> - 网络通信
>
> - - 第44节会解析网络系统调用的内核实现：socket, bind, listen, accept, connect
>   - 第45节和第46节会解析网络系统调用的内核实现：write
>   - 第47节和第48节会解析网络系统调用的内核实现：read
>
> - 查看源代码中的系统调用
>
> - - 第09节会解析系统调用在内核中的实现
>   - 第60节会做一个操作系统的实验，添加一个自己的系统调用，所以学到这里还是要好好看一下
>
> - 中介与Glibc
>
> - - 其实大部分程序员都是通过glibc来使用系统调用，所以系统学习一下glibc还是很有必要的
>   - 第09节解析系统调用的时候，会讲如何从glibc调用到内核系统调用的
>   - 第19节讲线程创建的时候，会讲glibc和系统调用合作完成线程机制的
>   - 第20节讲内存管理的时候，会讲glibc和系统调用合作完成内存分配的
>   - 第38节讲信号的时候，会讲glibc和系统调用合作完成信号处理函数设置的

## 存储管理

### 存储设备层次结构 ch6

#### 局部性



### 虚拟存储器 ch9

#### 缺页 

#### 页表   ch9.3  21讲

Virtual Page， Physical Page：未分配； 缓存的分配页；未缓存的分配也

分段机制、分页机制以及从虚拟地址到物理地址的映射方式。总结一下这两节，我们可以把内存管理系统精细化为下面三件事情：第一，虚拟内存空间的管理，将虚拟内存分成大小相等的页；第二，物理内存的管理，将物理内存分成大小相等的页；第三，内存映射，将虚拟内存页和物理内存页映射起来，并且在内存紧张的时候可以换出到硬盘中。

##### 分段机制 ch9.6.3

4G数据，每页4KB数据，1M个页表项 ，一个页表项4KB。 

4M的页表项数据，每页4KB数据，1K个页目录

> 32位系统，两级目录，页表项，页目录项

![img](https://static001.geekbang.org/resource/image/b6/b8/b6960eb0a7eea008d33f8e0c4facc8b8.jpg)

> 64 位的系统，四级目录，分别是全局页目录项 PGD（Page Global Directory）、上层页目录项 PUD（Page Upper Directory）、中间页目录项 PMD（Page Middle Directory）和页表项 PTE（Page Table Entry）。

![img](https://static001.geekbang.org/resource/image/42/0b/42eff3e7574ac8ce2501210e25cd2c0b.jpg)

#### 进程的虚拟内存空间管理  ch9.7   22讲   

* 一个进程要运行起来需要以下的内存结构。

用户态：代码段、全局变量、BSS函数栈堆内存映射区

内核态：内核的代码、全局变量、BSS内核数据结构例如 task_struct内核栈内核中动态分配的内存

![img](https://static001.geekbang.org/resource/image/f8/b1/f83b8d49b4e74c0e255b5735044c1eb1.jpg)

![img](https://static001.geekbang.org/resource/image/28/e8/2861968d1907bc314b82c34c221aace8.jpeg)

#### 物理内存的管理  23，24讲

* 整页
* 小内存

> 物理内存来讲，从下层到上层的关系及分配模式如下：
>
> 物理内存分 NUMA 节点，分别进行管理；
>
> 每个 NUMA 节点分成多个内存区域；
>
> 每个内存区域分成多个物理页面；
>
> 伙伴系统将多个连续的页面作为一个大的内存块分配给上层；
>
> kswapd 负责物理页面的换入换出；
>
> Slub Allocator 将从伙伴系统申请的大内存块切成小块，分配给其他系统。

#### mmap存储器映射 ch9.8   25讲

[mmap笔记](https://www.cnblogs.com/luoahong/p/10916458.html)

```c

struct mm_struct {
  struct vm_area_struct *mmap;    /* list of VMAs */
......
}


struct vm_area_struct {
  /*
   * For areas with an address space and backing store,
   * linkage into the address_space->i_mmap interval tree.
   */
  struct {
    struct rb_node rb;
    unsigned long rb_subtree_last;
  } shared;
```

> \- 申请小块内存用 brk; 申请大块内存或文件映射用 mmap
> \- mmap 映射文件, 由 fd 得到 struct file
>   \- 调用 ...->do_mmap
>     \- 调用 get_unmapped_area 找到一个可以进行映射的 vm_area_struct
>     \- 调用 mmap_region 进行映射
>   \- get_unmapped_area
>     \- 匿名映射: 找到前一个 vm_area_struct
>     \- 文件映射: 调用 file 中 file_operations 文件的相关操作, 最终也会调用到 get_unmapped_area
>   \- mmap_region
>     \- 通过 vm_area_struct 判断, 能否基于现有的块扩展(调用 vma_merge)
>     \- 若不能, 调用 kmem_cache_alloc 在 slub 中得到一个 vm_area_struct 并进行设置
>     \- 若是文件映射: 则调用 file_operations 的 mmap 将 vm_area_struct 的内存操作设置为文件系统对应操作(读写内存就是读写文件系统)
>     \- 通过 vma_link 将 vm_area_struct 插入红黑树
>     \- 若是文件映射, 调用 __vma_link_file 建立文件到内存的反映射
> \- 内存管理不直接分配内存, 在使用时才分配
> \- 用户态缺页异常, 触发缺页中断, 调用 do_page_default
> \- __do_page_fault 判断中断是否发生在内核
>   \- 若发生在内核, 调用 vmalloc_fault, 使用内核页表进行映射
>   \- 若不是, 找到对应 vm_area_struct 调用 handle_mm_fault
>   \- 得到多级页表地址 pgd 等
>   \- pgd 存在 task_struct.mm_struct.pgd 中
>   \- 全局页目录项 pgd 在创建进程 task_struct 时创建并初始化, 会调用 pgd_ctor 拷贝内核页表到进程的页表
> \- 进程被调度运行时, 通过 switch_mm_irqs_off->load_new_mm_cr3 切换内存上下文
> \- cr3 是 cpu 寄存器, 存储进程 pgd 的物理地址(load_new_mm_cr3 加载时通过直接内存映射进行转换)
> \- cpu 访问进程虚拟内存时, 从 cr3 得到 pgd 页表, 最后得到进程访问的物理地址
> \- 进程地址转换发生在用户态, 缺页时才进入内核态(调用__handle_mm_fault)
> \- __handle_mm_fault 调用 pud_alloc, pmd_alloc, handle_pte_fault 分配页表项
>   \- 若不存在 pte
>     \- 匿名页: 调用 do_anonymous_page 分配物理页 ①
>     \- 文件映射: 调用 do_fault ②
>   \- 若存在 pte, 调用 do_swap_page 换入内存 ③
>   \- ① 为匿名页分配内存
>     \- 调用 pte_alloc 分配 pte 页表项
>     \- 调用 ...->__alloc_pages_nodemask 分配物理页
>     \- mk_pte 页表项指向物理页; set_pte_at 插入页表项
>   \- ② 为文件映射分配内存 __do_fault
>     \- 以 ext4 为例, 调用 ext4_file_fault->filemap_fault
>     \- 文件映射一般有物理页作为缓存 find_get_page 找缓存页
>     \- 若有缓存页, 调用函数预读数据到内存
>     \- 若无缓存页, 调用 page_cache_read 分配一个, 加入 lru 队列, 调用 readpage 读数据: 调用 kmap_atomic 将物理内存映射到内核临时映射空间, 由内核读取文件, 再调用 kunmap_atomic 解映射
>   \- ③ do_swap_page
>     \- 先检查对应 swap 有没有缓存页
>     \- 没有, 读入 swap 文件(也是调用 readpage)
>     \- 调用 mk_pte; set_pet_at; swap_free(清理 swap)
> \- 避免每次都需要经过页表(存再内存中)访问内存
>   \- TLB 缓存部分页表项的副本

##### 用户态

用户态内存映射函数 mmap，包括用它来做匿名映射和文件映射。用户态的页表结构，存储位置在 mm_struct 中。在用户态访问没有映射的内存会引发缺页异常，分配物理页表、补齐页表。如果是匿名映射则分配物理内存；如果是 swap，则将 swap 文件读入；如果是文件映射，则将文件读入。

刘超

![img](https://static001.geekbang.org/resource/image/78/44/78d351d0105c8e5bf0e49c685a2c1a44.jpg)

#####  内核态

#### TLB   9.6.2  25讲

malloc

## 网络编程 ch11

详情看第43节至第48节

## 并发编程 ch12

### I/O多路复用技术

### 线程

#### 互斥量

## 进程管理

详情看第10节至第19节

## 文件子系统

详情看第27节至第30节

![img](https://static001.geekbang.org/resource/image/e4/df/e49b5c2a78ac09903d697126bfe6c5df.jpeg)



### IO  ch10

## 编译系统   ch5,ch7