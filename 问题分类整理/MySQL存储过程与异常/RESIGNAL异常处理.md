# RESIGNAL 异常处理

## 问题

`RESIGNAL` 是什么？为什么常和 `ROLLBACK` 一起用？

## 分类

MySQL存储过程与异常

## 回答

`RESIGNAL` 是 MySQL 存储过程中的“重新抛出异常”语句。

它通常写在异常处理器 `HANDLER` 里面，意思是：已经捕获到了错误，也做了处理，例如回滚事务，然后继续把这个错误抛出去，让调用者知道具体出错原因。

常见模板：

```sql
DECLARE EXIT HANDLER FOR SQLEXCEPTION
BEGIN
    ROLLBACK;
    RESIGNAL;
END;
```

执行逻辑：

```text
发生 SQL 异常
进入 HANDLER
执行 ROLLBACK 回滚事务
RESIGNAL 把原错误继续抛出去
```

如果不用 `RESIGNAL`，错误可能被处理器“吃掉”，调用者不一定能看到具体错误信息。

## SIGNAL 和 RESIGNAL 的区别

| 语句 | 作用 |
| --- | --- |
| `SIGNAL` | 主动制造一个新异常 |
| `RESIGNAL` | 把已经捕获到的异常重新抛出去 |

示例：

```sql
IF p_student_id IS NULL THEN
    SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = '学生ID不能为空';
END IF;
```

## 总结

`RESIGNAL` 就是异常被捕获并处理后，再把原异常继续抛出去。常见写法是 `ROLLBACK; RESIGNAL;`，这样既回滚事务，又保留错误提示。

