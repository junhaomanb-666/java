# 八股问题复习库

本文件夹用于存放你后续提供的八股问题总结与复习内容。

这里按面试方向拆分成独立 Markdown 文件。后续你继续补充内容时，我会按类别追加到对应文件；如果出现新类别，会新建对应文件。

## 当前文件

| 文件 | 用途 |
| --- | --- |
| [Java集合.md](Java集合.md) | Java 集合框架、List、Set、Map、并发集合 |
| [Java基础.md](Java基础.md) | Java 基础语法、JVM 字节码等基础题 |
| [JVM.md](JVM.md) | JVM、GC、类加载、内存模型等基础题 |
| [Java异常.md](Java异常.md) | 异常体系、异常处理、异常关键字、自定义异常 |
| [Java多线程.md](Java多线程.md) | 线程创建、线程状态、同步机制、线程池 |
| [Java并发编程.md](Java并发编程.md) | 并发基础、线程通信、锁、AQS、线程池、并发容器 |
| [JavaIO.md](JavaIO.md) | IO 分类、字节流、字符流、缓冲流、序列化、NIO |
| [Java面向对象.md](Java面向对象.md) | 封装、继承、多态、类与对象、接口和抽象类 |
| [Spring.md](Spring.md) | Spring 概述、IoC/DI、Bean、注解、数据访问、事务、AOP |
| [SpringMVC.md](SpringMVC.md) | Spring MVC 核心组件、执行流程、注解、参数绑定、视图、异常、拦截器 |
| [MyBatis.md](MyBatis.md) | MyBatis 简介、工作原理、映射器、动态 SQL、插件、缓存 |
| [MySQL.md](MySQL.md) | 存储引擎、事务、索引、SQL 安全、表操作 |
| [数据库面试详解.md](数据库面试详解.md) | 数据库高频面试题详解、索引、事务、锁、SQL、范式 |
| [白皮书-Java基础-MySQL高频.md](白皮书-Java基础-MySQL高频.md) | 白皮书来源的 Java 基础 + MySQL 高频题整理 |
| [计算机网络.md](计算机网络.md) | TCP 三次握手、四次挥手等网络基础 |
| [Linux.md](Linux.md) | 系统资源、端口、链接、启动流程、权限、日志 |
| [分类模板.md](分类模板.md) | 单道题的整理格式 |
| [复习计划.md](复习计划.md) | 后续记录错题、二刷、复习安排 |

## 后续分类规则

常见分类可以包括：

- Java 基础
- Java 集合
- Java 并发
- JVM
- MySQL / 数据库
- Redis
- Spring / Spring Boot
- 计算机网络
- 操作系统
- 数据结构与算法
- 项目 / 场景题

如果你提供的问题属于多个类别，我会按主要考点归类，并在题目里标注相关标签。

## 当前批次

- 2026-07-22：已整理 Java 集合、Java 异常、Java 多线程、Java IO、Java 面向对象、MySQL、Linux。
- Linux 标题为 10 题，目前实际提供 9 题，后续可补第 10 题。
- 2026-07-23：已将重复数据库问题合并整理到 `数据库面试详解.md`，并补充 Java 异常详解、计算机网络、面向对象对比题。
- 2026-07-24：已根据 `07-MyBatis面试题.pdf` 整理 `MyBatis.md`，去重后 35 题。
- 2026-07-24：已补充本批次去重题：视图特点/缺点、InnoDB 行锁、锁类别、SQL 约束、SQL、存储过程、索引原理/算法、B 树好处、Java `&`/`&&`、字节码、内部类优点。
- 2026-07-24：已根据 `04-并发编程面试题-重点.pdf` 整理 `Java并发编程.md`，去重后 57 题。
- 2026-07-28：已根据 `白皮书.txt` 整理 `白皮书-Java基础-MySQL高频.md`，共 22 题。
- 2026-07-28：已检查 `数据库面试详解.pdf`，内容与 `数据库面试详解.md` 第 1-40 题重复；现有 Markdown 已覆盖，并额外包含第 41-52 题。
- 2026-07-30：已补充 Java GC、`Comparable`/`Comparator`、`Iterable`/`Iterator`、集合框架总览、线程创建与同步方式。

- 2026-07-31：已补充本批去重后的新增题：创建索引原则、SQL 生命周期、CHAR/VARCHAR 更新差异、InnoDB 四大特性、游标、主键类型、Java 构造方法、抽象类、对象引用、内部类、`this/super`、静态访问限制、返回值、数据类型、`final`、访问修饰符、反射获取 `Class` 的三种方法。
- 2026-08-01：已根据 JavaGuide JVM GC 全文重整 `JVM.md`，替换原有简版 GC 内容，补充堆结构、对象分配、存活判断、引用类型、GC 算法、收集器、Full GC 排查和面试速记表。
- 2026-08-03：已根据 `05-Spring MVC面试题.pdf` 和 `06-Spring面试题-重点.pdf` 新增 `SpringMVC.md`、`Spring.md`，去重整理 Spring MVC 28 题、Spring 48 题。
- 2026-08-03：已检查 `Java核心基础+MySQL+Mybatis+Spring高频面试题（35道含答案）.pdf` 和 `Java基础+MySQL高频面试题（含详细答案解析）.pdf`；多数内容已覆盖，去重后补充构造方法不能重写、NPE 场景、HashMap 线程不安全、fail-fast/fail-safe、MVCC、Spring AOP 应用场景等。
## 单题整理格式

```text
## 题号 标题

**类别：**
**标签：**
**题目：**
**答案：**
**解析：**
**考点：**
**易错点：**
**复习动作：**
```
