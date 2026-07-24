# MySQL

## 1. MySQL 的存储引擎有哪些？MySQL 8 默认是什么？

**答案：** 常见存储引擎有 `InnoDB`、`MyISAM`、`Memory`。MySQL 8 默认是 `InnoDB`，支持事务、行级锁、崩溃恢复等能力。

## 2. InnoDB 和 MyISAM 的区别？

**答案：** `InnoDB` 支持事务、外键、行级锁、崩溃恢复；`MyISAM` 不支持事务和外键，使用表级锁，查询速度在某些读多场景下较快。

## 3. 事务的 ACID 是什么？

**答案：**

- 原子性 Atomicity
- 一致性 Consistency
- 隔离性 Isolation
- 持久性 Durability

## 4. MySQL 事务的隔离级别？

**答案：**

- `READ UNCOMMITTED`：读未提交，可能脏读
- `READ COMMITTED`：读已提交，可能不可重复读
- `REPEATABLE READ`：可重复读，MySQL 默认隔离级别
- `SERIALIZABLE`：串行化

## 5. 主键索引和唯一索引的区别？

**答案：** 主键索引一张表只能有一个，不允许为 `NULL`；唯一索引一张表可以有多个，允许 `NULL`。

## 6. CHAR 和 VARCHAR 的区别？

**答案：** `CHAR` 是定长，适合固定长度数据；`VARCHAR` 是变长，更节省空间，适合长度变化较大的字符串。

## 7. 什么是 SQL 注入？如何防止？

**答案：** SQL 注入是攻击者拼接恶意 SQL，执行非预期数据库操作。防范方式包括使用 `PreparedStatement` 参数化查询、输入过滤、最小权限原则。

## 8. MySQL 架构分几层？

**答案：** MySQL 架构主要分为 Server 层和存储引擎层。Server 层包括连接器、查询缓存、分析器、优化器、执行器；存储引擎层负责数据存储和读取。

## 9. DELETE、TRUNCATE、DROP 的区别？

**答案：** `DELETE` 删除表中记录，可配合事务回滚；`TRUNCATE` 清空整张表，通常会重置自增 ID；`DROP` 删除表或数据库对象，并释放空间。

## 10. 索引优化的建议？

**答案：**

- 合理选择索引类型
- 避免创建过多索引
- 合理使用联合索引
- 高选择性列优先考虑建索引
- 避免索引失效
