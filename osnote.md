# 操作系统原理
## 进程调度策略
- **先进先出**(First-In-First-Out, **FIFO**)
- **最短任务优先**(Shortest Job First, **SJF**)
- **最短完成时间优先**(Short Time-to-Completion First, **STCF**)
- **时间片轮转**(Round-Robin, **RR**)
- **多级反馈队列**(Multi-Level Feedback Queue, **MLFQ**)
## Linux多线程(POSIX)
- pthread_t
- pthread_create()
- pthread_join()
- pthread_detach()
- pthread_exit()
## 线程同步原语(POSIX)
- **互斥锁**, Mutex Lock
	- pthread_mutex_t, 互斥量数据类型
	- pthread_mutex_init(), 初始化互斥量
	- pthread_mutex_lock(), 获取锁, 如果指定互斥量还在上锁状态则堵塞等待直至可以获取锁.
	- pthread_mutex_unlock(), 释放锁, 释放指定互斥锁
	- pthread_mutex_trylock(), 尝试获取锁, 相较于pthread_mutex_lock(), 这个函数在不能获取锁的时候会直接返回而不是阻塞.
	- pthread_mutex_destroy(), 销毁互斥量, 释放指定互斥量的内存.
	- pthread_mutex_timedlock(), 等待一定时间获取锁, 如果不能在指定时间内获取锁则超时并返回错误.
- **自旋锁**, Spin Lock
	- pthread_spin_t
	- pthread_spin_init()
	- pthread_spin_lock()
	- pthread_spin_unlock()
	- pthread_spin_trylock()
	- pthread_spin_destroy()
- **条件变量**, Condition
- **信号量**, Semaphore
- **屏障**, Barrier
## 文件和目录
存储虚拟化形成了两个关键的抽象: 每个文件都有一个低级名称(**inode**). 目录中的每一个条目都指向文件或其他目录.
- 文件: 文件就是一个线性字节数组，每个字节都可以读取或写入.
- 目录: 目录像文件一样, 也有一个低级名字(**inode**号), 但是它的内容很具体, 它包含一个(用户可读名字, 低级名字)对的列表。例如存在一个低级名称为"10"的文件, 它的用户可读名称为"foo", 则"foo"所在的目录因此会有条目("foo", "10"), 将用户刻度名称映射到低级名称.