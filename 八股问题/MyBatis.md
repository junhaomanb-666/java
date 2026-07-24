# MyBatis 面试题

> 来源：`D:/Documents/QQ_Files/07-MyBatis面试题.pdf`
>
> 整理方式：去重后按“通俗理解 + 专业回答 + 记忆版”整理，方便理解和面试复述。

## 1. MyBatis 是什么？

**通俗理解：** MyBatis 是帮 Java 程序操作数据库的持久层框架。它把 JDBC 里大量重复的连接、参数设置、结果集封装工作简化掉，让你主要关注 SQL 本身。

**专业回答：** MyBatis 是一个优秀的持久层框架，也是半自动 ORM 框架。它支持自定义 SQL、存储过程和高级映射，可以通过 XML 或注解把 Java 对象和数据库记录进行映射，避免大量原生 JDBC 模板代码。

**记忆版：** MyBatis = 持久层框架 + 半自动 ORM + SQL 可控。

## 2. ORM 是什么？

**通俗理解：** ORM 就是把 Java 对象和数据库表之间建立对应关系。程序里操作对象，最终能落到数据库表中。

**专业回答：** ORM 是 Object Relational Mapping，对象关系映射，用于解决面向对象模型和关系型数据库表结构之间的映射问题。它通过映射元数据将对象属性和表字段关联起来，从而实现对象持久化。

**记忆版：** ORM = 对象和表的映射。

## 3. 为什么说 MyBatis 是半自动 ORM？和全自动 ORM 有什么区别？

**通俗理解：** Hibernate 更像“你告诉它对象关系，它帮你生成 SQL”；MyBatis 更像“SQL 你自己写，我帮你传参和封装结果”。

**专业回答：** MyBatis 需要开发者手动编写 SQL，并配置 SQL 结果与 Java 对象之间的映射，因此属于半自动 ORM。Hibernate 可以根据对象关系模型自动生成 SQL，并自动管理关联对象或集合，因此更接近全自动 ORM。

**记忆版：** Hibernate 自动生成 SQL；MyBatis 手写 SQL、自动映射。

## 4. 传统 JDBC 开发有什么问题？MyBatis 如何解决？

**通俗理解：** 原生 JDBC 很啰嗦：要自己开连接、关连接、写参数、遍历结果集。MyBatis 把这些重复劳动封装了。

**专业回答：** JDBC 的问题主要包括连接创建和释放频繁、SQL 写在 Java 代码中导致硬编码、参数设置繁琐、结果集解析重复。MyBatis 通过连接池管理连接，通过 XML 或注解管理 SQL，通过参数映射自动设置参数，通过结果映射自动封装 Java 对象。

**记忆版：** JDBC 四痛点：连接、SQL、参数、结果集；MyBatis 都帮你封装。

## 5. MyBatis 有哪些优缺点？

**通俗理解：** MyBatis 的优点是灵活、SQL 好优化；缺点是 SQL 要自己写，换数据库时可能要改 SQL。

**专业回答：**

- 优点：SQL 和 Java 代码解耦，支持动态 SQL，减少 JDBC 模板代码，便于 SQL 优化，能和 Spring 良好集成。
- 缺点：SQL 编写量较大，对开发者 SQL 能力有要求；SQL 依赖具体数据库方言，数据库迁移性不如 Hibernate。

**记忆版：** 优点是灵活可控；缺点是手写 SQL、移植性弱。

## 6. MyBatis 适合什么场景？

**通俗理解：** 如果项目 SQL 复杂、性能要求高、需求变化快，用 MyBatis 比较合适。

**专业回答：** MyBatis 适合对 SQL 控制要求高、需要手动优化 SQL、业务查询复杂、需求变化频繁的项目，例如互联网业务系统。它不太适合完全不想写 SQL、对象模型非常稳定且希望自动管理复杂对象关系的场景。

**记忆版：** SQL 复杂、性能敏感、需求常变，选 MyBatis。

## 7. Hibernate 和 MyBatis 的区别？

**通俗理解：** Hibernate 自动化程度高，但 SQL 不够直观；MyBatis 自动化程度低一些，但 SQL 可控。

**专业回答：** 两者都是持久层框架，都是对 JDBC 的封装。Hibernate 是全自动 ORM，关注对象关系，数据库无关性较好，但 SQL 优化相对困难，学习成本高。MyBatis 是半自动 ORM，关注 SQL 本身，动态 SQL 灵活、优化方便，但数据库移植性较弱，需要手写 SQL。

**记忆版：** Hibernate 重对象、自动化；MyBatis 重 SQL、可控性。

## 8. MyBatis 编程步骤是什么？

**通俗理解：** 先创建工厂，再拿会话，用会话执行 SQL，最后提交和关闭。

**专业回答：**

1. 创建 `SqlSessionFactory`
2. 通过 `SqlSessionFactory` 创建 `SqlSession`
3. 通过 `SqlSession` 执行数据库操作
4. 提交事务
5. 关闭 `SqlSession`

**记忆版：** 工厂 -> 会话 -> 执行 -> 提交 -> 关闭。

## 9. MyBatis 的工作原理是什么？

**通俗理解：** MyBatis 启动时先读取配置和 Mapper 文件，执行时根据方法找到对应 SQL，填充参数，交给数据库执行，再把结果封装成对象返回。

**专业回答：** MyBatis 启动时读取全局配置文件和映射文件，构建 `Configuration` 和 `SqlSessionFactory`。执行 SQL 时，`SqlSession` 根据 statement id 找到对应的 `MappedStatement`，由 `Executor` 生成 SQL、设置参数、执行数据库操作，并通过结果映射把结果集封装成 Java 对象。

**记忆版：** 加载配置 -> 找 SQL -> 设参数 -> 执行 -> 映射结果。

## 10. MyBatis 的功能架构分几层？

**通俗理解：** 可以理解为三层：外面给程序调用，中间处理 SQL，底层提供连接、事务、缓存等支持。

**专业回答：** MyBatis 功能架构通常分为 API 接口层、数据处理层、基础支撑层。API 接口层提供外部调用入口；数据处理层负责 SQL 解析、执行和结果映射；基础支撑层负责连接管理、事务管理、配置加载、缓存等通用能力。

**记忆版：** 接口层调入口，处理层跑 SQL，支撑层管连接事务缓存。

## 11. 为什么需要 SQL 预编译？

**通俗理解：** 预编译就是 SQL 模板先让数据库准备好，后面只传参数，不用每次重新编译 SQL。

**专业回答：** 预编译通过 `PreparedStatement` 实现。数据库可以提前编译 SQL 模板，后续执行时只绑定参数，减少重复编译成本。同时参数与 SQL 结构分离，可以有效降低 SQL 注入风险。

**记忆版：** 预编译 = 性能更好 + 防 SQL 注入。

## 12. MyBatis 有哪些 Executor 执行器？

**通俗理解：** Executor 是真正干活执行 SQL 的组件。不同 Executor 执行方式不同。

**专业回答：** MyBatis 有三种常见执行器：

- `SimpleExecutor`：每执行一次 SQL 都创建新的 Statement，默认执行器。
- `ReuseExecutor`：复用相同 SQL 对应的 Statement。
- `BatchExecutor`：批量执行更新语句，适合批量插入、更新。

**记忆版：** SIMPLE 普通，REUSE 复用，BATCH 批量。

## 13. 如何指定 Executor 执行器？

**通俗理解：** 可以在配置文件里设置默认执行器，也可以创建 `SqlSession` 时手动指定。

**专业回答：** 可以在 MyBatis 配置文件的 `settings` 中配置默认 `ExecutorType`，也可以调用 `SqlSessionFactory.openSession(ExecutorType execType)` 手动传入执行器类型，例如 `ExecutorType.BATCH`。

**记忆版：** 配置里设默认，`openSession` 可手动指定。

## 14. MyBatis 是否支持延迟加载？原理是什么？

**通俗理解：** 支持。比如先查用户，不立刻查订单；等你真正调用用户的订单属性时，再去查订单。

**专业回答：** MyBatis 支持 `association` 和 `collection` 的延迟加载，也就是一对一和一对多关联对象的延迟加载。其原理通常是通过代理对象拦截属性访问，当访问未加载的关联属性时，再执行对应 SQL 查询并填充属性。

**记忆版：** 先不查关联对象，用到时再查；底层靠代理拦截。

## 15. `#{}` 和 `${}` 有什么区别？

**通俗理解：** `#{}` 是安全传参，会变成 `?`；`${}` 是字符串拼接，容易 SQL 注入。

**专业回答：** `#{}` 使用预编译占位符，MyBatis 会把它替换成 `?`，再通过 `PreparedStatement` 设置参数，可以防止 SQL 注入。`${}` 是文本替换，会把变量值直接拼接到 SQL 中，不能防 SQL 注入，通常只适合表名、字段名、排序字段等不能使用占位符的位置。

**记忆版：** `#{}` 走预编译，安全；`${}` 走拼接，危险。

## 16. MyBatis 模糊查询 like 怎么写？

**通俗理解：** 推荐把 `%` 和参数用 `concat` 拼起来，既能模糊查，又不破坏预编译安全性。

**专业回答：** 不推荐使用 `'%${keyword}%'`，因为容易 SQL 注入。推荐写法是：

```sql
WHERE name LIKE CONCAT('%', #{keyword}, '%')
```

也可以使用 `bind` 标签提前拼接：

```xml
<bind name="pattern" value="'%' + keyword + '%'" />
WHERE name LIKE #{pattern}
```

**记忆版：** 模糊查询优先 `CONCAT('%', #{key}, '%')`。

## 17. Mapper 中如何传递多个参数？

**通俗理解：** 多个参数要让 SQL 能认清每个参数叫什么，最常用的是 `@Param`。

**专业回答：** 常见传参方式包括顺序传参、`@Param` 注解、`Map` 传参、JavaBean 传参。顺序传参可读性差，不推荐；参数较少时推荐 `@Param`；参数灵活变化时可用 `Map`；业务参数较多且有明确结构时推荐 JavaBean。

**记忆版：** 少量参数用 `@Param`，复杂业务用 JavaBean，动态参数用 Map。

## 18. MyBatis 如何执行批量操作？

**通俗理解：** 批量操作有两种思路：SQL 里用 `foreach` 一次拼多条数据，或者用 `BatchExecutor` 批量提交。

**专业回答：** MyBatis 批量操作常用 `foreach` 标签构造批量 SQL，例如批量 `insert values (...), (...)` 或 `where id in (...)`。也可以使用 `ExecutorType.BATCH` 创建批处理 `SqlSession`，让多个更新语句批量发送执行。但批处理模式在事务提交前可能无法立即拿到自增主键。

**记忆版：** SQL 批量靠 `foreach`，执行批量靠 `ExecutorType.BATCH`。

## 19. `foreach` 标签常用属性有哪些？

**通俗理解：** `foreach` 就是循环拼 SQL，比如拼 `in (1,2,3)`。

**专业回答：** `foreach` 常用属性包括：

- `collection`：要遍历的集合
- `item`：当前元素别名
- `index`：当前索引或 key
- `open`：开始符号
- `separator`：分隔符
- `close`：结束符号

**记忆版：** `collection` 找集合，`item` 取元素，`open/separator/close` 控制拼接格式。

## 20. 如何获取插入后生成的主键？

**通俗理解：** MySQL 自增主键可以让 MyBatis 插入后自动把 id 回填到对象里；Oracle 这类没有自增的数据库常用序列配合 `selectKey`。

**专业回答：** 对 MySQL 这类支持自增主键的数据库，可以在 `insert` 标签中使用 `useGeneratedKeys="true"` 和 `keyProperty` 获取生成主键。对 Oracle 这类使用序列的数据库，可以使用 `selectKey` 标签，在插入前或插入后查询主键值并设置到对象属性中。

**示例：**

```xml
<insert id="insertUser" useGeneratedKeys="true" keyProperty="id">
  INSERT INTO user(name) VALUES(#{name})
</insert>
```

**记忆版：** MySQL 用 `useGeneratedKeys`；Oracle 常用 `selectKey`。

## 21. 实体属性名和表字段名不一致怎么办？

**通俗理解：** 要么 SQL 里起别名，让字段名变成属性名；要么用 `resultMap` 明确写映射关系。

**专业回答：** 可以通过 SQL 别名让查询列名与 Java 属性名一致，例如 `order_id AS id`；也可以使用 `resultMap` 配置列和属性的映射关系，适合字段较多或映射复杂的场景。

**记忆版：** 简单用别名，复杂用 `resultMap`。

## 22. Mapper 编写有哪几种方式？

**通俗理解：** 老方式要写实现类；现在更常用 Mapper 接口 + XML，或者扫描 Mapper 接口让 Spring 自动生成代理对象。

**专业回答：** 常见方式包括：接口实现类继承 `SqlSessionDaoSupport`；使用 `MapperFactoryBean`；使用 Mapper 扫描器自动扫描接口。实际 Spring 项目中通常使用 Mapper 扫描器，让 MyBatis 为 Mapper 接口创建代理对象。

**记忆版：** 旧方式实现类，新方式 Mapper 代理，常用扫描器。

## 23. 什么是 MyBatis 接口绑定？有哪些实现方式？

**通俗理解：** 接口绑定就是 Mapper 接口的方法和 SQL 绑定起来，调用接口方法就等于执行对应 SQL。

**专业回答：** 接口绑定是把 Mapper 接口方法与 SQL 语句绑定。实现方式主要有两种：注解绑定，在方法上使用 `@Select`、`@Update` 等注解；XML 绑定，在 Mapper XML 中配置 SQL，并让 `namespace` 等于接口全限定名。

**记忆版：** 简单 SQL 用注解，复杂 SQL 用 XML。

## 24. 使用 Mapper 接口调用有哪些要求？

**通俗理解：** 接口方法要和 XML 里的 SQL 对得上，否则 MyBatis 找不到该执行哪条 SQL。

**专业回答：**

- Mapper XML 的 `namespace` 必须是 Mapper 接口全限定名。
- 接口方法名要和 XML 中 statement 的 `id` 一致。
- 方法参数类型要和 SQL 参数匹配。
- 方法返回值类型要和 `resultType` 或 `resultMap` 匹配。

**记忆版：** namespace 对接口，方法名对 id，参数和返回值要匹配。

## 25. Mapper 接口的工作原理是什么？方法能重载吗？

**通俗理解：** Mapper 接口没有实现类，MyBatis 会生成代理对象。调用方法时，用“接口名 + 方法名”去找 XML 里的 SQL。

**专业回答：** Mapper 接口通过动态代理实现。接口全限定名对应 XML 的 `namespace`，方法名对应 `MappedStatement` 的 `id`。调用接口方法时，MyBatis 根据 `namespace + id` 找到唯一 `MappedStatement` 并执行。因为定位主要依赖方法名，Mapper 接口中不建议方法重载，否则容易导致 statement 定位和参数解析混乱。

**记忆版：** Mapper 是代理对象，靠“接口全名 + 方法名”找 SQL；不建议重载。

## 26. MyBatis 如何把 SQL 结果封装成目标对象？

**通俗理解：** MyBatis 会把结果集里的列名和 Java 对象属性名对应起来，然后用反射创建对象、设置属性。

**专业回答：** MyBatis 结果映射有两种常见方式：使用 `resultMap` 明确配置字段和属性关系；使用 SQL 别名让列名与属性名一致。映射时 MyBatis 通过反射创建目标对象，并根据列和属性的映射关系为属性赋值。

**记忆版：** 列名对属性名，反射创建对象并赋值。

## 27. XML 映射文件中常见标签有哪些？

**通俗理解：** Mapper XML 里不只有增删改查标签，还有结果映射、SQL 片段、动态 SQL、主键生成等标签。

**专业回答：** 常见标签包括 `select`、`insert`、`update`、`delete`、`resultMap`、`sql`、`include`、`selectKey`，以及动态 SQL 标签 `if`、`where`、`set`、`trim`、`foreach`、`choose`、`when`、`otherwise`、`bind`。

**记忆版：** 增删改查四标签，映射 `resultMap`，复用 `sql/include`，动态 SQL 九标签。

## 28. `sql` 片段通过 `include` 引用时，被引用片段必须写在前面吗？

**通俗理解：** 不必须。MyBatis 解析时如果先遇到引用、后面才看到片段，会先标记，等全部解析后再补解析。

**专业回答：** 被 `include` 引用的 `sql` 片段可以定义在引用语句之前，也可以定义在之后。MyBatis 解析 XML 时，如果发现引用目标暂时不存在，会将该节点标记为未解析，等所有节点解析完成后再次解析。

**记忆版：** `sql` 片段不怕写后面，MyBatis 会二次解析。

## 29. MyBatis 如何实现一对一、一对多查询？

**通俗理解：** 一种是多表联查一次查出来；另一种是先查主表，再根据外键查关联表。

**专业回答：** MyBatis 实现关联查询主要有联合查询和嵌套查询。联合查询通过多表 join 一次查出结果，再用 `resultMap` 中的 `association` 表示一对一，用 `collection` 表示一对多。嵌套查询先查主对象，再通过 `select` 配置查询关联对象或集合。

**记忆版：** 一对一用 `association`，一对多用 `collection`；方式有联查和嵌套查。

## 30. MyBatis 能否映射枚举 Enum？

**通俗理解：** 可以。枚举和数据库字段之间怎么转换，可以交给 TypeHandler。

**专业回答：** MyBatis 可以映射枚举类型，也可以通过自定义 `TypeHandler` 映射任意 Java 类型和数据库列类型。`TypeHandler` 的核心作用是完成 Java 类型到 JDBC 类型、JDBC 类型到 Java 类型的转换，主要通过 `setParameter()` 和 `getResult()` 实现。

**记忆版：** 类型转换找 `TypeHandler`。

## 31. MyBatis 动态 SQL 是做什么的？有哪些标签？

**通俗理解：** 动态 SQL 就是 SQL 会根据参数不同自动拼接。比如参数为空就不拼这个条件。

**专业回答：** MyBatis 动态 SQL 允许在 XML 中通过标签进行条件判断和 SQL 拼接。常用标签包括 `if`、`where`、`set`、`trim`、`foreach`、`choose`、`when`、`otherwise`、`bind`。其执行原理是基于 OGNL 表达式从参数对象中取值，判断后动态生成最终 SQL。

**记忆版：** 动态 SQL = 标签判断 + OGNL 取值 + 拼最终 SQL。

## 32. MyBatis 如何分页？分页插件原理是什么？

**通俗理解：** MyBatis 自带的 `RowBounds` 是内存分页，数据可能先查出来再截取；真正高效分页应该改写 SQL，加 `limit`。

**专业回答：** MyBatis 可以使用 `RowBounds` 分页，但它通常是逻辑分页或内存分页，不适合大数据量。分页插件通过 MyBatis 插件机制拦截 SQL 执行过程，根据数据库方言改写 SQL，例如 MySQL 添加 `limit offset, size`，从而实现物理分页。

**记忆版：** `RowBounds` 偏内存分页；分页插件改 SQL 做物理分页。

## 33. MyBatis 插件运行原理是什么？如何编写插件？

**通俗理解：** 插件就是在 MyBatis 执行 SQL 的关键环节插一段自己的逻辑，比如分页插件就在 SQL 执行前改写 SQL。

**专业回答：** MyBatis 插件基于拦截器和动态代理实现，只能拦截四类核心接口：`Executor`、`StatementHandler`、`ParameterHandler`、`ResultSetHandler`。编写插件需要实现 `Interceptor` 接口，重写 `intercept()` 方法，并使用注解指定拦截的接口和方法，最后在配置文件中注册插件。

**记忆版：** 插件拦四大对象：执行器、语句、参数、结果集。

## 34. MyBatis 一级缓存和二级缓存有什么区别？

**通俗理解：** 一级缓存跟着一次 `SqlSession` 走，同一个会话里重复查可能直接从缓存拿；二级缓存跟着 Mapper 命名空间走，多个会话可以共享。

**专业回答：** 一级缓存是 `SqlSession` 级别缓存，默认开启，作用域是当前会话，会话 `flush` 或 `close` 后缓存清空。二级缓存是 `namespace` 级别缓存，默认不开启，需要显式配置，缓存对象通常需要实现 `Serializable`。当对应作用域发生增删改操作时，相关查询缓存会被清空。

**记忆版：** 一级缓存看 Session，二级缓存看 namespace；增删改会清缓存。

## 35. MyBatis 中 `resultType` 和 `resultMap` 怎么选？

**通俗理解：** 字段名和属性名能自动对应，用 `resultType` 就够了；对应不上或有关联关系，用 `resultMap`。

**专业回答：** `resultType` 适合结果列和 Java 属性名一致、映射简单的场景。`resultMap` 适合字段名与属性名不一致、复杂对象映射、一对一、一对多、嵌套查询等场景。

**记忆版：** 简单映射用 `resultType`，复杂映射用 `resultMap`。
