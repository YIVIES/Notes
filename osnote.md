# 操作系统原理

## 进程调度策略

- **先进先出**(First-In-First-Out, **FIFO**)
- **最短任务优先**(Shortest Job First, **SJF**)
- **最短完成时间优先**(Short Time-to-Completion First, **STCF**)
- **时间片轮转**(Round-Robin, **RR**)
- **多级反馈队列**(Multi-Level Feedback Queue, **MLFQ**)

## 进程

进程创建相关函数.

- fork(): 创建进程.
- wait(): 等待进程结束, 这个函数也有变体.
- exec(): 这个函数有很多变体.

## Linux多线程(POSIX)

- 这里是一些线程创建等操作相关的基本类型和函数.
  - pthread_t
  - pthread_create()
  - pthread_join()
  - pthread_detach()
  - pthread_exit()

## 线程同步原语(POSIX)

- **互斥锁**, Mutex Lock.
  - pthread_mutex_t, 互斥量数据类型
  - pthread_mutex_init(), 初始化互斥量
  - pthread_mutex_lock(), 获取锁, 如果指定互斥量还在上锁状态则堵塞等待直至可以获取锁.
  - pthread_mutex_unlock(), 释放锁, 释放指定互斥锁
  - pthread_mutex_trylock(), 尝试获取锁, 相较于pthread_mutex_lock(), 这个函数在不能获取锁的时候会直接返回而不是阻塞.
  - pthread_mutex_destroy(), 销毁互斥量, 释放指定互斥量的内存.
  - pthread_mutex_timedlock(), 等待一定时间获取锁, 如果不能在指定时间内获取锁则超时并返回错误.
- **自旋锁**, Spin Lock.
  - pthread_spin_t
  - pthread_spin_init()
  - pthread_spin_lock()
  - pthread_spin_unlock()
  - pthread_spin_trylock()
  - pthread_spin_destroy()
- **读写锁**, Read-Write Lock.
- **条件变量**, Condition.
  - pthread_cond_t
  - pthread_cond_init()
  - pthread_cond_wait()
  - pthread_cond_signal()
  - pthread_cond_destroy()
  - pthread_cond_timewait()
  - pthread_cond_broadcast()
- **信号量**, Semaphore.
- **屏障**, Barrier.

## 廉价冗余磁盘阵列(RAID)

- **RAID0**: 条带化形式, 性能和容量都很优秀, 但是没有冗余.
- **RAID1**: 镜像化形式, 可靠性高, 但是容量利用差, 只能利用全部磁盘空间的一半.
- **RAID4**: 奇偶校验形式, 可靠性好, 容错率好, 容量利用也还不错, 但是随机小写入情况下吞吐量很糟糕.
- **RAID5**: 旋转奇偶校验形式, 和RAID4差不多, 比RAID4稍快一些, 但构建相对RAID4稍微麻烦一点.

## 文件和目录

存储虚拟化形成了两个关键的抽象: 每个文件都有一个低级名称(**inode**). 目录中的每一个条目都指向文件或其他目录.

- **文件**: 文件就是一个线性字节数组，每个字节都可以读取或写入.
- **目录**: 目录像文件一样, 也有一个低级名字(**inode**号), 但是它的内容很具体, 它包含一个(用户可读名字, 低级名字)对的列表。例如存在一个低级名称为"10"的文件, 它的用户可读名称为"foo", 则"foo"所在的目录因此会有条目("foo", "10"), 将用户刻度名称映射到低级名称.
- **目录树**: 通过将目录放入其他目录中, 用户可以构建任意的目录树(Directory tree), 在该目录树下存储所有文件和目录.
- **inode**: 一种数据结构, 记录了文件的各种信息, 一般大小为128字节或者256字节.
- **inode表**: inode表(**inode table**), 存储系统中所有inode的区域.
