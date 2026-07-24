# ROW_NUMBER、RANK、DENSE_RANK 的区别

## 问题

`ROW_NUMBER()`、`RANK()`、`DENSE_RANK()` 有什么区别？

## 分类

SQL窗口函数

## 回答

三者都可以用于排序排名，区别主要在“并列排名”时的处理方式。

| 函数 | 并列时 |
| --- | --- |
| `ROW_NUMBER()` | 强行编号，不会并列 |
| `RANK()` | 允许并列，会跳号 |
| `DENSE_RANK()` | 允许并列，不跳号 |

示例数据：

| 岗位 | 投递人数 |
| --- | --- |
| A | 5 |
| B | 5 |
| C | 3 |

`ROW_NUMBER()` 结果：

| 岗位 | rn |
| --- | --- |
| A | 1 |
| B | 2 |
| C | 3 |

`RANK()` 结果：

| 岗位 | rank |
| --- | --- |
| A | 1 |
| B | 1 |
| C | 3 |

`DENSE_RANK()` 结果：

| 岗位 | dense_rank |
| --- | --- |
| A | 1 |
| B | 1 |
| C | 2 |

## 总结

只想强行取一个第一名，用 `ROW_NUMBER()`；需要保留并列排名，用 `RANK()` 或 `DENSE_RANK()`。

