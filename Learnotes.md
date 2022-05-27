# 操作系统原理
## 进程调度策略
- **先进先出**(First-In-First-Out, **FIFO**)
- **最短任务优先**(Shortest Job First, **SJF**)
- **最短完成时间优先**(Short Time-to-Completion First, **STCF**)
- **时间片轮转**(Round-Robin, **RR**)
- **多级反馈队列**(Multi-Level Feedback Queue, **MLFQ**)
## 线程同步原语(POSIX)
- **互斥锁**, Mutex Lock
	- pthread_mutex_t
	- pthread_mutex_init()
	- pthread_mutex_lock()
	- pthread_mutex_unlock()
	- pthread_mutex_trylock()
- **自旋锁**, Spin Lock
- **条件变量**, Condition
- **信号量**, Semaphore
- **屏障**, Barrier