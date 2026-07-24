# ROW_NUMBER 窗口函数

## 问题

`ROW_NUMBER()` 是什么？怎么使用？

## 分类

SQL窗口函数

## 回答

`ROW_NUMBER()` 是 SQL 的窗口函数，用来按照指定规则给查询结果编号。

基本语法：

```sql
ROW_NUMBER() OVER (
    PARTITION BY 分组字段
    ORDER BY 排序字段
)
```

含义：

- `ROW_NUMBER()`：生成行号
- `OVER()`：窗口函数固定写法
- `PARTITION BY`：按什么字段分组
- `ORDER BY`：每组内部按什么顺序编号

示例：每个企业内部给岗位编号。

```sql
SELECT
    company_id,
    id AS job_id,
    name AS job_name,
    ROW_NUMBER() OVER (
        PARTITION BY company_id
        ORDER BY id
    ) AS rn
FROM job;
```

常见用法：每组取第一条。

```sql
WITH job_rank AS (
    SELECT
        company_id,
        id AS job_id,
        name AS job_name,
        ROW_NUMBER() OVER (
            PARTITION BY company_id
            ORDER BY id
        ) AS rn
    FROM job
)
SELECT
    company_id,
    job_id,
    job_name
FROM job_rank
WHERE rn = 1;
```

## 总结

`ROW_NUMBER()` 的核心作用是“每组内部排序编号”，经常配合 `rn = 1` 取每组第一条数据。

