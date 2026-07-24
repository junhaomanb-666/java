# Java 多线程

## 1. 进程和线程的区别？

**答案：** 进程是资源分配的最小单位，拥有独立内存空间；线程是 CPU 调度的最小单位，共享进程资源，切换开销更小。

## 2. 创建线程的方式有哪些？

**答案：**

- 继承 `Thread`
- 实现 `Runnable`
- `Callable` + `FutureTask`
- 匿名内部类
- Lambda 表达式
- 线程池

## 3. start() 和 run() 的区别？

**答案：** `start()` 会启动新线程，并由 JVM 自动调用 `run()`；直接调用 `run()` 只是普通方法调用，不会创建新线程。

## 4. 线程有哪些状态？

**答案：**

- `NEW`
- `RUNNABLE`
- `BLOCKED`
- `WAITING`
- `TIMED_WAITING`
- `TERMINATED`

## 5. synchronized 和 volatile 的区别？

**答案：** `synchronized` 可以保证原子性和可见性；`volatile` 只能保证可见性和有序性，不能保证复合操作的原子性。

## 6. 什么是死锁？

**答案：** 两个或多个线程互相等待对方释放资源，导致所有相关线程都无法继续执行。

## 7. Runnable 和 Callable 的区别？

**答案：** `Runnable` 没有返回值，也不能直接抛出受检异常；`Callable` 有返回值，并且可以抛出异常。

## 8. 线程池的核心参数有哪些？

**答案：**

- `corePoolSize`
- `maximumPoolSize`
- `keepAliveTime`
- `unit`
- `workQueue`
- `threadFactory`
- `handler`

## 9. 什么是线程安全？如何实现？

**答案：** 多线程访问共享数据时，程序结果仍然正确，就叫线程安全。可以通过 `synchronized`、`Lock`、`volatile`、原子类、线程安全集合等方式实现。

## 10. Java 程序默认有几个线程？

**答案：** 至少有 2 个：主线程和 GC 线程。实际运行时通常还会包含后台监控线程等，大约 5 到 7 条，具体数量与 JVM 实现和运行环境有关。
