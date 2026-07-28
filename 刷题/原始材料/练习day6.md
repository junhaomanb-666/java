1.![78490178845](C:\Users\mjhqu\AppData\Local\Temp\1784901788451.png)

选B



2.

![78490181647](C:\Users\mjhqu\AppData\Local\Temp\1784901816471.png)

关键就是--y和y--，前者先减再赋值，后者先赋值后减



3.![78490350018](C:\Users\mjhqu\AppData\Local\Temp\1784903500181.png)

示例代码：

![img](https://uploadfiles.nowcoder.com/images/20170830/5248791_1504089837512_39944D8036786CB820F9D9873950ABA5)

  解析：**1. 静态内部类：** 

​      **1. 静态内部类本身可以访问外部的静态资源，包括静态私有资源。但是不能访问非静态资源，可以不依赖外部类实例而实例化。** 

  **2. 成员内部类：** 

​      **1. 成员内部类本身可以访问外部的所有资源，但是自身不能定义静态资源，因为其实例化本身就还依赖着外部类。**

  **3. 局部内部类：** 

​      **1. 局部内部类就像一个局部方法，不能被访问修饰符修饰，也不能被static修饰。**

​      **2. 局部内部类只能访问所在代码块或者方法中被定义为final的局部变量。**

  **4. 匿名内部类：** 

​      **1. 没有类名的内部类，不能使用class，extends和implements，没有构造方法。**

​      **2. 多用于GUI中的事件处理。**

​      **3. 不能定义静态资源**

​      **4. 只能创建一个匿名内部类实例。**

​      **5. 一个匿名内部类一定是在new后面的，这个匿名类必须继承一个父类或者实现一个接口。**

​      **6. 匿名内部类是局部内部类的特殊形式，所以局部内部类的所有限制对匿名内部类也有效。**



4.

![78490873382](C:\Users\mjhqu\AppData\Local\Temp\1784908733824.png)

占位符"?"只能代表一个值



5.

![78490916524](C:\Users\mjhqu\AppData\Local\Temp\1784909165244.png)

**选项A：Java面向对象语言容许单独的过程与函数存在**
 此说法错误。Java是一种纯粹的面向对象语言，所有代码都必须定义在类中。Java不支持独立于类或对象的过程或函数（例如，没有全局函数）。任何功能都必须封装在类的方法中（如静态方法或实例方法）。因此，该说法错误。   

​    **选项B：Java面向对象语言容许单独的方法存在**
 此说法错误。Java中的方法（method）必须定义在类中，不能单独存在。方法总是类或对象的成员，脱离类定义方***导致编译错误（例如，尝试在类外部定义方法是非法的）。因此，该说法错误。   

​    **选项C：Java语言中的方法属于类中的成员（member）**
 此说法正确。在Java中，方法（包括实例方法和静态方法）是类的重要组成部分，与字段（fields）、构造器（constructors）等一样，都属于类的成员（member）。方法用于定义对象的行为或类的功能，并通过类或对象访问。例如，在类定义中，方法直接声明在类体内，是类的直接成员。   

​    **选项D：Java语言中的方法必定隶属于某一类（对象），调用方法与过程或函数相同**
 此说法错误。虽然第一部分“方法必定隶属于某一类（对象）”正确（方法必须属于某个类，如果是实例方法则隶属于对象，如果是静态方法则隶属于类），但第二部分“调用方法与过程或函数相同”不准确：   

- ​     在Java中，方法调用必须通过对象或类（如object.method()或ClassName.method()），需要指定接收者（对象或类）。        
- ​     在过程式语言（如C语言）中，过程或函数是独立的，调用时直接使用名称（如function()），无需接收者。        
- ​     因此，调用方式在语法和语义上并不相同：Java方法调用涉及对象上下文（例如，实例方法依赖于对象状态），而过程或函数调用是直接的。尽管静态方法调用（如Math.max()）在语法上类似函数调用，但仍需类名作为前缀，不能视为“相同”。
   整体上，该说法错误。       





6.

![78490928128](C:\Users\mjhqu\AppData\Local\Temp\1784909281285.png)

  货币的字段类型一般有int，float，money/smallmoney，decimal/numberic。 

  根据存储数据的精度不同选择： 

  int只能存储整数的钱。 

  money/smallmoney 数据类型精确到它们所代表的货币单位的万分之一 。 

  decimal/numberic 可以自定义小数位和能存储的数据精度, 所以一般使用这种类型的人会多一些





7.

![78490932417](C:\Users\mjhqu\AppData\Local\Temp\1784909324178.png)



![img](https://uploadfiles.nowcoder.com/images/20200828/619044738_1598587914444_4DE69893BC5DECA766485F5B397A6AC7)



8.

![78491072182](C:\Users\mjhqu\AppData\Local\Temp\1784910721822.png)



```sql
select t1.*,t2.*
from (
select * from student_table where sex = '男' ) t1
inner join
(select * from student_table where sex = '女')t2
on t1.name = t2.name
union all
select t1.*,t2.*
from (
select * from student_table where sex = '男' ) t1
left join
(select * from student_table where sex = '女')t2
on t1.name = t2.name
where t2.name is null
union all
select t1.*,t2.*
from (
select * from student_table where sex = '男' ) t1
right join
(select * from student_table where sex = '女')t2
on t1.name = t2.name
where t1.name is null ;
```

FULL JOIN
= 匹配成功的数据

+ 左表未匹配的数据
+ 右表未匹配的数据

因此应该写成：

```sql
INNER JOIN
UNION ALL
LEFT JOIN ... WHERE 右表字段 IS NULL
UNION ALL
RIGHT JOIN ... WHERE 左表字段 IS NULL
```

![img](https://uploadfiles.nowcoder.com/images/20220617/993004961_1655456516680/14FC7E3CA734E29DCD649D849AC8509F)