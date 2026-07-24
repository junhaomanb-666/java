# COALESCE 空值处理

## 问题

`COALESCE()` 是什么？

## 分类

SQL函数

## 回答

`COALESCE()` 是 MySQL 中用来处理 `NULL` 值的函数。

语法：

```sql
COALESCE(值1, 值2, 值3, ...)
```

它会从左到右依次判断，返回第一个不是 `NULL` 的值。

## 总结

`COALESCE()` 常用来给可能为空的字段设置备用值。

