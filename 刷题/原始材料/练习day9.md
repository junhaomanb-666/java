1.

![78523786904](C:\Users\mjhqu\AppData\Local\Temp\1785237869048.png)



2.

![78523789083](C:\Users\mjhqu\AppData\Local\Temp\1785237890837.png)

| READ UNCOMMITTED   | 立即返回 9            | 允许脏读               |
| ------------------ | --------------------- | ---------------------- |
| **READ COMMITTED** | **立即返回 10**       | 避免脏读，读已提交版本 |
| REPEATABLE READ    | 立即返回 10           | 读事务开始时的快照     |
| SERIALIZABLE       | 可能等待或立即返回 10 | 依赖锁机制             |

3.

![78523915058](C:\Users\mjhqu\AppData\Local\Temp\1785239150589.png)



4.

![78523934777](C:\Users\mjhqu\AppData\Local\Temp\1785239347776.png)



![img](https://uploadfiles.nowcoder.com/images/20170524/7010483_1495588925759_ACED241801E307EE7A39612F85A94EBF)

Protected  外部包不能访问，但是，子类在外部包的话，就可以外部包的子类可以访问 

  Default   外部包，子类不能访问，意思就是外部包不可以访问，就算是子类在外部包中。但是，如果子类在内部包中，就可以访问





5. ​

![78523946490](C:\Users\mjhqu\AppData\Local\Temp\1785239464907.png)

局部变量没有默认值，使用前必须显式初始化，否则编译报错。



6.

![78523965299](C:\Users\mjhqu\AppData\Local\Temp\1785239652990.png)

**A 读取 Cookie**：`request.getCookies()`

**B 读取 HTTP 请求头**：`request.getHeader("名称")`

**D 读取路径信息**：`request.getPathInfo()`、`request.getRequestURI()`

**C 设置响应的 Content-Type**：属于 `HttpServletResponse`



7.

![78523982810](C:\Users\mjhqu\AppData\Local\Temp\1785239828109.png)



**java 黙认浮点类型为double** 

  **float数据类型有一个后缀为" f "或" F "。** 

   **long类型有一个后缀，为" l " 或者" L "**

强制类型转换的优先级高于+ - * / 



8.

![78523987858](C:\Users\mjhqu\AppData\Local\Temp\1785239878580.png)

 Java体系结构包括四个独立但相关的技术： 

-    Java程序设计语言    
-    Java.class文件格式    
-    Java应用编程接口（API）    
-    Java虚拟机   

四者的关系： 

 当我们编写并运行一个Java程序时，就同时运用了这四种技术，用**Java程序设计语言**编写源代码，把它编译成**Java.class文件格式**，然后再在**Java虚拟机中运行class文件**。当程序运行的时候，它通过调用class文件实现了**Java API的方法**来满足程序的Java API调用

