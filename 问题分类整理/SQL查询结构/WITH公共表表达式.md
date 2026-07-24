# WITH 公共表表达式

## 问题

`WITH` 是什么？有什么用？

## 分类

SQL查询结构

## 回答

`WITH` 是 SQL 里的公共表表达式，英文叫 CTE：Common Table Expression。

它可以把复杂查询中的中间结果先命名，然后在后面的 SQL 中像临时表一样使用。

基本格式：

```sql
WITH 临时结果名 AS (
    SELECT ...
)
SELECT ...
FROM 临时结果名;
```

示例：

```sql
WITH job_apply_count AS (
    SELECT
        job_id,
        COUNT(*) AS apply_count
    FROM delivery
    GROUP BY job_id
)
SELECT
    j.id,
    j.name,
    jac.apply_count
FROM job j
LEFT JOIN job_apply_count jac
    ON j.id = jac.job_id;
```

## 总结

`WITH` 适合把复杂 SQL 拆成清晰的步骤，尤其常和统计、分组、窗口函数一起使用。它只在当前 SQL 中有效，不会真的创建表。

