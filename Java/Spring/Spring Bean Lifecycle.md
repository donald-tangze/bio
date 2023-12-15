XML或annotation parser  --> BeanDefinition 

> 只有 singleton，非延迟加载的bean的instantiation实例化和applicationContext是一起处理的，其他延迟加载的和protype只到生成BeanDefinition，下面步骤是第一次使用时发生进行初始化

-->   instantiation 实例化 所有的引用是null  

-->  initialization初始化            (加载包括这两步)

> 

![B221E14D-FCD2-48A1-A4EE-190C8072CE60](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x1lu6saj20wp0gndgx.jpg)

![img](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x1p6u5gj20fq061aag.jpg)

![image-20220206150731348](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x1s2jnqj217d0r5dk9.jpg)

![image-20220206152523105](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x1x4rqtj211v0lr0uy.jpg)

![image-20220206215820265](https://tva1.sinaimg.cn/large/e6c9d24egy1h39x20w2i7j21020lzgnp.jpg)







