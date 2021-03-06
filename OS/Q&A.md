# Q&A for OPsystem

## 虚拟内存映射

## 内存、映射

## 进程间通信

## 死锁

## 线程的状态

新建（new）、就绪（runningable）、开始（running）、阻塞（block）、死亡（dead）
[参考文章](https://blog.csdn.net/xingjing1226/article/details/81977129)

## 重复创建线程为什么会开销过大?

[参考文章](https://zhuanlan.zhihu.com/p/161628226)

1.线程创建的开销
对操作系统来说,创建一个线程的代价是十分昂贵的, 需要给它分配内存、列入调度，同时在线程切换的时候还要执行内存换页，CPU 的缓存被清空,切换回来的时候还要重新从内存中读取信息,破坏了数据的局部性。【分配内存、列入调度、内存换页、清空缓存和重新读取】

关于内存开销

Java线程的线程栈区别于堆，它是不受Java程序控制的，只受系统资源限制。默认一个线程的线程栈大小是1M，别小看这1M的空间，如果每个用户请求都新建线程的话，1024个用户光线程就占用了1个G的内存，如果系统比较大的话，一下子系统资源就不够用了，最后程序就崩溃了。

【创建一个线程默认需要消耗1M的内存，如果每个用户请求都创建一个线程，那么1024个用户就是1G了，并发量一大就扛不住了】

如果不对线程的创建进行有效监控、管理，风险巨大：

频繁申请/销毁资源和调度资源，将带来额外的消耗，可能会非常巨大。
对资源无限申请缺少抑制手段，将引发系统资源耗尽的风险。
系统无法合理管理内部的资源分布，将降低系统的稳定性。
正是因为如此大的开销，所以几乎所有的servlet容器、web框架、rpc框架都会采用线程池化技术去提高资源复用，限制线程的随意创建。