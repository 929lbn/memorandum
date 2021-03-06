  
#### 一、写一个c程序辨别系统是**16位**or**32位** 
```c++
法一：
     int k=~0;
     if((unsigned int)k >63356) 
       cout<<"at least 32bits"<<endl;
     else 
       cout<<"16 bits"<<endl;

法二：//32为系统

     int i=65536;
     cout<<i<<endl;
     int j=65535;
     cout<<j<<endl;
```

#### 二、写一个c程序辨别系统是**大端or小端**字节序  
用联合体：如char类型的，可以看他输出的是int的高字节还是低字节 

#### 三、**TCP** vs **UDP**  
1. **面向链接**：TCP面向链接，面向连接意味着两个使用TCP的应用（通常是一个客户和一个服务器）在彼此交换数据之前必须通过三次握手先建立一个TCP连接。在一个TCP中仅有两方彼此通信，多播和广播不能用于TCP。UDP是不可靠的传输，传输前*不需要建立链接*，可以应用多播和广播实现一对多的通信。  
2. **可靠性**：TCP提供端到端的流量控制，对收到的数据进行确认，采用超时重发，对失序的数据进行重新排序等机制保证数据通信的可靠性。而UDP是一种不可靠的服务，接收方可能不能收到发送方的数据报。

#### 四、共享内存  
共享内存是最快的可用IPC（进程间通信）形式。它允许多个不相关的进程去访问同一部分逻辑内存。共享内存是由IPC为一个进程创建的一个特殊的地址范围，它将**出现在进程的地址空间**中。其他进程可以把同一段共享内存段“连接到”它们自己的地址空间里去。所有进程都可以访问共享内存中的地址。如果一个进程向这段共享内存写了数据，所做的改动会立刻被有访问同一段共享内存的其他进程看到。因此共享内存对于数据的传输是非常高效的。  
**共享内存的原理**：共享内存是最有用的进程间通信方式之一，也是最快的IPC形式。两个不同进程A、B共享内存的意思是，同一块物理内存被映射到进程A、B各自的进程地址空间。进程A可以即时看到进程B对共享内存中数据的更新，反之亦然。  

#### 五、**多进程** VS **多线程**  
| 维度 | 多进程 | 多线程 |
|----|-----|-----|
| 数据共享、同步 | 共享复杂，需要IPC；同步简单 | 共享进程数据，共享简单；同步复杂 |
| 内存、CPU | 占用内存多，切换复杂，CPU利用率低 | 占用内存少，切换简单，CPU利用率高 |
| 创建销毁、切换 | 复杂，速度慢 | 简单，速度快 |
| 可靠性 | 进程间不互相影响 | 一个线程挂掉导致整个进程挂掉 |
| 分布式 | 适合多核、多机分布 | 适合多核分布 |     
 
**线程的共享资源包括**：全局变量、地址空间、子进程、信号和信号服务程序等。  
**线程的私有资源**：线程号：每个线程都有唯一的线程号、寄存器（程序寄存器和堆栈寄存器）、堆栈、信号掩码、优先级等。  
  
- 需要频繁创建销毁的优先用线程  
- 需要进行大量计算的优先使用线程  
- 强相关的处理用线程，弱相关的处理用进程  
- 可能扩展到多机分布的用进程，多核分布的用线程  
