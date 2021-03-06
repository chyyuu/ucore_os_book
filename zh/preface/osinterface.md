# 操作系统的接口

首先，读者可站在使用操作系统的角度来看操作系统。操作系统内核是一个需要提供各种服务的软件，其服务对象是应用程序，而用户（这里可以理解为一般使用计算机的人）是通过应用程序的服务间接获得操作系统的服务的），所以操作系统内核藏在一般用户看不到的地方。但应用程序需要访问操作系统，获得操作系统的服务，这就需要通过操作系统的接口才能完成。如果把操作系统看成是一个函数库，那么其接口就是函数名称和它的参数。但操作系统不是简单的一个函数库，它的接口需要考虑安全因素，使得应用软件不能直接读写操作系统内部函数的地址地址空间，为此，操作系统设计了一个安全可靠的接口，我们称为系统调用接口（System Call Interface），应用程序可以通过系统调用接口请求获得操作系统的服务，但不能直接调用操作系统的函数和全局变量；操作系统提供完服务后，返回应用程序继续执行。

对于实际操作系统而言，具有大量的服务接口，比如Linux有上百个系统调用接口。为了简单起见，以ucore OS为例，可以看到它为应用程序提供了如下一些接口：

* 进程管理：复制创建--fork、退出--exit、执行--exec、...
* 同步互斥的并发控制：信号量--semaphore、管程--monitor、条件变量--condition variable 、...
* 进程间通信：管道--pipe、信号--signal、事件--event、邮箱--mailbox、共享内存--shared mem、...
* 文件I/O操作：读--read、写--write、打开--open、关闭--close、...
* 外设I/O操作：外设包括键盘、显示器、串口、磁盘、时钟、...，但接口是直接采用了文件I/O操作的系统调用接口

> 这在某种程度上说明了文件是外设的一种抽象。在UNIX中（ucore是模仿UNIX），大部分外设都可以以文件的形式来访问

有了这些接口，简单的应用程序就不用考虑底层硬件细节，可以在操作系统的服务支持和管理下简洁地完成其应用功能了。



![](/zh/preface/figures/os_interface.png)

