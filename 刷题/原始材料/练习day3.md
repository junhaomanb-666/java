1.![78461906888](C:\Users\mjhqu\AppData\Local\Temp\1784619068889.png)

'ORDER BY子句缺失会导致行为未定义，但不是语法错误





2.

![78461927952](C:\Users\mjhqu\AppData\Local\Temp\1784619279527.png)

  ROUND() 函数用于把数值字段舍入为指定的小数位数； 

  TRUNCATE() 函数是按照小数位数进行数值截取，没有四舍五入。 





3.

![78461940049](C:\Users\mjhqu\AppData\Local\Temp\1784619400496.png)

共享锁S：共享锁锁定的资源可以被其他用户读取，但是其他用户无法修改，在执行select时，sql server会对对象加共享锁。（其他人可读不可写） 

  排它锁X：(独占锁)其他人不能读也不能写（所以不会多重更新）。 

  更新锁U：**当SQL Server准备更新数据时，它首先对数据对象作更新锁锁定，这样数据将不能被修改，但可以读取。等到SQL Server确定要进行更新数据操作时，他会自动将更新锁换为独占锁，当对象上有其他锁存在时，无法对其加更新锁。** 

  **架构锁：在执行依赖于表架构的操作时使用。架构锁的类型为：架构修改 (Sch****-****M) 和架构稳定性 (Sch****-****S)。**





4.

![78461990876](C:\Users\mjhqu\AppData\Local\Temp\1784619908769.png)普通插入（全字段）：INSERT INTO table_name VALUES (value1, value2, ...) 

  普通插入（限定字段）：INSERT INTO table_name (column1, column2, ...) VALUES (value1, value2, ...) 

  多条一次性插入：INSERT INTO table_name (column1, column2, ...) VALUES (value1_1, value1_2, ...), (value2_1, value2_2, ...), ... 

  从另一个表导入：INSERT INTO table_name SELECT * FROM table_name2 [WHERE key=value]





5.

![78462007060](C:\Users\mjhqu\AppData\Local\Temp\1784620070601.png)

正确答案是 **B**。

```
SELECT user_id
FROM orders
WHERE amount > (
    SELECT AVG(amount)
    FROM orders
);
```

## 为什么 B 正确

子查询：

```
SELECT AVG(amount)
FROM orders
```

先计算所有订单的平均金额。

外层查询：

```
WHERE amount > 平均金额
```

再找出订单金额高于平均值的订单对应用户。

------

## A 为什么错

```
SELECT user_id
FROM orders
WHERE amount > AVG(amount);
```

`AVG(amount)` 是聚合函数，不能直接写在 `WHERE` 里。

`WHERE` 是逐行过滤，而 `AVG()` 是整体统计，执行阶段不同。

会报类似错误：

```
Invalid use of group function
```

------

## C 为什么错

```
SELECT user_id
FROM orders
GROUP BY user_id
HAVING AVG(amount) > amount;
```

问题在于：

```
amount
```

没有出现在 `GROUP BY` 中，也没有被聚合。

分组后每个用户可能有多条订单，数据库不知道这里的 `amount` 指哪一条订单的金额。

------

## D 为什么错

```
SELECT user_id, AVG(amount)
FROM orders
GROUP BY user_id
HAVING amount > AVG(amount);
```

同样问题：

```
HAVING amount > AVG(amount)
```

里面的 `amount` 不是分组字段，也不是聚合结果，容易报错。

而且它的逻辑也变成了“用户分组后的平均金额比较”，和题目“订单金额高于整体平均值”不一致。

一句话记住：

> **聚合函数不能直接放在 WHERE 中比较，要先用子查询算出平均值，再在外层 WHERE 里比较。**





6.

![78462027029](C:\Users\mjhqu\AppData\Local\Temp\1784620270292.png)







7.

![78462144275](C:\Users\mjhqu\AppData\Local\Temp\1784621442757.png)





8.

![78462182977](C:\Users\mjhqu\AppData\Local\Temp\1784621829770.png)

 向上转型(子类转父类)是自动和安全的

向下转型(父类转子类)需要显式转换,且只有当对象的实际类型是目标类型或其子类时才能成功,否则会抛出ClassCastException



9.

![78462204383](C:\Users\mjhqu\AppData\Local\Temp\1784622043832.png)

答案 13

 按位或|   按位且&      按位取反~     按位异或^ 

  逻辑与&&    逻辑或||         非！

  左移<<:补0，相当于乘以2 

  右移>>：补符号位，相当于除以2 

  无符号右移>>>：补0



10.

![78462224727](C:\Users\mjhqu\AppData\Local\Temp\1784622247278.png)

![78462226348](C:\Users\mjhqu\AppData\Local\Temp\1784622263485.png)



11.

![78462305066](C:\Users\mjhqu\AppData\Local\Temp\1784623050660.png)

- 编译器将Java源代码编译成字节码class文件 
- 类加载到JVM里面后，执行引擎把字节码转为可执行代码 
- 执行的过程，再把可执行代码转为机器码，由底层的操作系统完成执行     



12.

![78462314943](C:\Users\mjhqu\AppData\Local\Temp\1784623149432.png)



子类构造方法必须先调用父类构造方法；如果父类没有无参构造，子类必须手动写super(参数)



13.

![78462336952](C:\Users\mjhqu\AppData\Local\Temp\1784623369528.png)

![78462339129](C:\Users\mjhqu\AppData\Local\Temp\1784623391294.png)