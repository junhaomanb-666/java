# Spring 面试题

> 来源：`D:\Documents\QQ_Files\06-Spring面试题-重点.pdf`
>
> 整理原则：去除重复问法，按 Spring 概述、IoC/DI、Bean、注解、数据访问、事务、AOP 分类重写为“通俗理解 + 专业回答 + 记忆版”。

## 1. 什么是 Spring？

**通俗理解：** Spring 就是一个帮 Java 程序“管对象、管依赖、管事务、管增强逻辑”的框架。以前很多对象要自己 `new`，依赖关系也要自己维护；用了 Spring 后，这些基础工作可以交给容器。

**专业回答：** Spring 是一个轻量级 Java 开发框架，核心目标是简化企业级 Java 开发。它通过 IoC/DI 管理对象创建与依赖关系，通过 AOP 抽取日志、事务、安全等横切逻辑，并提供事务、数据访问、Web、测试等基础设施支持，让开发者更专注业务逻辑。

**记忆版：** Spring = IoC 管对象 + AOP 做增强 + 事务/数据访问等基础设施。

## 2. Spring 的设计目标、设计理念和核心是什么？

**通俗理解：** Spring 想让 Java 开发少写重复代码、少和框架强绑定，让对象之间不要互相“绑死”。

**专业回答：** Spring 的设计目标是提供一站式、轻量级应用开发平台。设计理念是支持 POJO 和面向接口编程，以非侵入方式降低业务代码对框架的依赖。核心是 IoC 容器和 AOP：IoC 负责对象创建、装配和生命周期管理；AOP 负责在不修改业务代码的情况下添加横切功能。

**记忆版：** 目标是简化开发；理念是低侵入、松耦合；核心是 IoC 和 AOP。

## 3. Spring 的优缺点是什么？

**通俗理解：** Spring 的好处是省事、解耦、好扩展；缺点是体系很大，学起来有门槛。

**专业回答：** Spring 的优点包括：方便解耦、简化开发；支持 AOP；支持声明式事务；便于测试；方便集成 MyBatis、Hibernate 等框架；封装 JDBC、JavaMail 等复杂 API。缺点包括：框架体系较庞大，学习成本较高；底层大量使用反射和代理，理解源码和排查问题需要一定基础；过度使用配置或注解可能增加项目复杂度。

**记忆版：** 优点：解耦、AOP、事务、测试、集成；缺点：大而全、学习成本高。

## 4. Spring 有哪些应用场景？

**通俗理解：** 只要是 Java 企业项目，尤其是需要分层、事务、数据库访问、Web 接口的项目，Spring 都很常见。

**专业回答：** Spring 常用于 JavaEE 企业应用开发，例如 SSM、Spring Boot、微服务应用等。它可以作为完整 Web 应用框架的基础，也可以只作为业务层/持久层中间层使用，还可以集成第三方框架，统一管理对象、事务、数据访问和横切逻辑。

**记忆版：** Spring 适合企业级 Java：Web、业务层、数据访问、事务、集成。

## 5. Spring 由哪些主要模块组成？

**通俗理解：** Spring 像一个工具箱，里面有管对象的、做 AOP 的、访问数据库的、做 Web 的、写测试的。

**专业回答：** Spring 主要模块包括 Core Container、AOP、Data Access/Integration、Web、Messaging、Test 等。常见子模块有 `spring-core`、`spring-beans`、`spring-context`、`spring-aop`、`spring-jdbc`、`spring-web`、`spring-test`。其中 Core Container 是基础，提供 IoC 和 DI 能力。

**记忆版：** 核心容器打底，AOP 增强，JDBC/ORM 访问数据，Web 做接口，Test 做测试。

## 6. Spring 中用到了哪些设计模式？

**通俗理解：** Spring 不是一个单一技术点，它内部用了很多经典设计模式，比如工厂创建 Bean、单例管理 Bean、代理实现 AOP。

**专业回答：** Spring 常见设计模式包括：工厂模式，如 `BeanFactory` 创建和管理 Bean；单例模式，Spring Bean 默认单例；代理模式，AOP 使用 JDK 动态代理或 CGLIB；模板方法模式，如 `JdbcTemplate`、`RestTemplate`；观察者模式，如事件发布和 `ApplicationListener`；适配器模式，如 MVC 中的 `HandlerAdapter`。

**记忆版：** Spring 常考模式：工厂、单例、代理、模板、观察者、适配器。

## 7. 什么是 Spring IoC 容器？

**通俗理解：** IoC 容器就是 Spring 的“对象仓库”。对象不再由我们到处 `new`，而是由容器创建好，需要时直接拿。

**专业回答：** IoC 是 Inversion of Control，控制反转。传统代码中对象创建和依赖查找由程序自己控制；在 Spring 中，对象创建、依赖注入、生命周期管理交给 IoC 容器。Spring IoC 容器负责读取配置元数据，创建 Bean，注入依赖，并管理 Bean 生命周期。

**记忆版：** IoC = 对象控制权从程序交给容器。

## 8. IoC 有什么作用和优点？

**通俗理解：** IoC 最大好处是对象之间不用互相硬编码依赖，换实现、做测试都更方便。

**专业回答：** IoC 可以统一管理对象创建和依赖维护，降低类之间耦合；便于面向接口编程和替换实现；便于单元测试；可以在对象创建过程中加入代理、生命周期回调等容器能力；让业务类更专注业务逻辑。

**记忆版：** IoC 优点：解耦、好替换、好测试、统一生命周期。

## 9. Spring IoC 的实现机制是什么？

**通俗理解：** Spring 先读取配置，知道要创建哪些类；需要对象时，通过反射创建，再把依赖塞进去。

**专业回答：** Spring IoC 的核心实现可以概括为“工厂模式 + 反射 + 配置元数据”。容器先把 XML、注解或 Java 配置解析成 `BeanDefinition`，保存到容器内部；调用 `getBean()` 时，根据 BeanDefinition 反射实例化对象，处理属性注入、依赖递归创建、初始化回调、后置处理器等流程。

**简化示例：**

```java
class BeanFactoryDemo {
    public static Object getBean(String className) throws Exception {
        Class<?> clazz = Class.forName(className);
        return clazz.getDeclaredConstructor().newInstance();
    }
}
```

**记忆版：** IoC 底层思路：配置变 BeanDefinition，反射创建 Bean，递归注入依赖。

## 10. BeanFactory 和 ApplicationContext 有什么区别？

**通俗理解：** `BeanFactory` 像基础仓库，只负责 Bean 的创建和获取；`ApplicationContext` 像完整应用中心，功能更多。

**专业回答：** `BeanFactory` 是 Spring 最底层的 IoC 容器接口，提供 Bean 定义读取、创建、依赖管理等基础能力，默认懒加载。`ApplicationContext` 是 `BeanFactory` 的子接口，除基础 IoC 功能外，还支持国际化、资源访问、事件发布、多个上下文、自动注册后置处理器等，通常在实际项目中使用。`ApplicationContext` 默认启动时预实例化单例 Bean，能更早暴露配置问题。

**记忆版：** BeanFactory 基础、懒加载；ApplicationContext 高级、功能全、项目常用。

## 11. ApplicationContext 常见实现类有哪些？

**通俗理解：** 不同实现类就是从不同地方加载 Spring 配置，比如 classpath、文件系统、Web 环境。

**专业回答：** 常见实现包括：`ClassPathXmlApplicationContext`，从 classpath 加载 XML；`FileSystemXmlApplicationContext`，从文件系统路径加载 XML；`WebApplicationContext`，用于 Web 应用环境；注解配置场景常见 `AnnotationConfigApplicationContext`。

**记忆版：** classpath 用 ClassPath，文件路径用 FileSystem，Web 用 WebApplicationContext，注解用 AnnotationConfig。

## 12. 什么是依赖注入 DI？

**通俗理解：** 一个对象需要另一个对象时，不再自己去找，而是让 Spring 在创建它时自动传进来。

**专业回答：** DI 是 Dependency Injection，依赖注入，是 IoC 的主要实现方式。组件不负责查找依赖对象，而是暴露构造器、Setter 或字段，由容器在运行期把依赖对象注入进去。这样可以降低组件之间的耦合，提升可测试性和可维护性。

**记忆版：** DI = 依赖由容器传进来，不由对象自己找。

## 13. 依赖注入有哪些方式？构造器注入和 Setter 注入有什么区别？

**通俗理解：** 构造器注入像“出生时必须带上依赖”，Setter 注入像“创建后再补充可选依赖”。

**专业回答：** 常见依赖注入方式包括构造器注入、Setter 方法注入和字段注入。构造器注入适合强制依赖，可以保证对象创建后状态完整，也便于不可变设计；Setter 注入适合可选依赖，灵活但可能出现对象创建后依赖未完全设置的问题；字段注入代码简洁，但不利于测试和显式表达依赖，实际项目更推荐构造器注入。

**记忆版：** 必需依赖用构造器，可选依赖用 Setter，字段注入少用。

## 14. 什么是 Spring Bean？

**通俗理解：** 被 Spring 容器创建、装配和管理的对象，就叫 Bean。

**专业回答：** Spring Bean 是由 Spring IoC 容器实例化、装配和管理的 Java 对象。Bean 的创建依据来自配置元数据，如 XML、注解或 Java 配置。容器会负责 Bean 的生命周期、依赖注入和相关扩展处理。

**记忆版：** Bean = 被 Spring 管起来的 Java 对象。

## 15. 一个 Spring Bean 定义包含哪些信息？

**通俗理解：** Bean 定义就像对象说明书，告诉 Spring 创建哪个类、叫什么名、依赖谁、生命周期方法是什么。

**专业回答：** BeanDefinition 通常包含类名、Bean 名称、作用域、构造参数、属性依赖、是否懒加载、初始化方法、销毁方法、自动装配模式等元数据。Spring 根据这些元数据完成 Bean 的创建和管理。

**记忆版：** BeanDefinition = 类信息 + 作用域 + 依赖 + 生命周期配置。

## 16. Spring 有几种配置元数据方式？

**通俗理解：** 告诉 Spring 怎么创建对象，常见方式有 XML、注解和 Java 配置类。

**专业回答：** Spring 常见配置方式包括 XML 配置、注解配置和 Java Config。XML 适合集中配置；注解配置如 `@Component`、`@Autowired` 更贴近代码；Java Config 使用 `@Configuration` 和 `@Bean`，类型安全、便于重构，是现代项目常见方式。

**记忆版：** Spring 配置三种：XML、注解、Java Config。

## 17. Spring Bean 有哪些作用域？

**通俗理解：** 作用域决定一个 Bean 是全局共用一个，还是每次创建新的，或者每个请求/会话一个。

**专业回答：** 常见作用域包括：`singleton`，每个容器一个实例，默认作用域；`prototype`，每次获取创建新实例；`request`，每个 HTTP 请求一个实例；`session`，每个 HTTP Session 一个实例；`application`，每个 ServletContext 一个实例；早期还常见 `globalSession`，主要用于 Portlet 环境。

**记忆版：** 默认 singleton；想每次新建用 prototype；Web 场景有 request/session/application。

## 18. Spring 中的单例 Bean 是线程安全的吗？

**通俗理解：** Spring 只保证单例 Bean 只有一个，不保证它里面的可变数据线程安全。

**专业回答：** Spring 单例 Bean 本身不天然线程安全。Spring 容器只负责创建和管理单例对象，不会自动为 Bean 的成员变量加锁。如果 Bean 是无状态的，例如 Service、DAO 通常不保存请求级数据，一般可以安全复用；如果 Bean 保存可变状态，就需要开发者自己保证线程安全，或改用 `prototype`、ThreadLocal、局部变量等方式。

**记忆版：** 单例不等于线程安全；无状态才适合单例共享。

## 19. Spring 如何处理线程并发问题？

**通俗理解：** Spring 常见做法是让 Bean 尽量无状态；如果必须保存线程相关数据，就用 ThreadLocal 给每个线程一份。

**专业回答：** Spring 本身不会替业务 Bean 自动解决线程安全问题。常见策略包括：将共享 Bean 设计为无状态；避免在单例 Bean 中保存请求级可变成员变量；使用局部变量；必要时使用 `ThreadLocal` 保存线程私有数据；对共享资源使用并发容器、锁或数据库事务控制。

**记忆版：** Spring 并发安全思路：无状态优先，线程数据用 ThreadLocal，共享资源要同步。

## 20. Spring Bean 的生命周期是什么？

**通俗理解：** Bean 从创建到销毁，不是简单 `new` 一下就完了。Spring 会创建对象、注入属性、执行各种回调、初始化，最后容器关闭时销毁。

**专业回答：** 典型生命周期包括：实例化 Bean；属性赋值和依赖注入；执行 Aware 回调，如 `BeanNameAware`、`BeanFactoryAware`、`ApplicationContextAware`；执行 `BeanPostProcessor#postProcessBeforeInitialization`；执行初始化方法，如 `InitializingBean#afterPropertiesSet`、`init-method`、`@PostConstruct`；执行 `postProcessAfterInitialization`，此阶段可能生成代理对象；Bean 可被使用；容器关闭时执行销毁方法，如 `DisposableBean#destroy`、`destroy-method`、`@PreDestroy`。

**记忆版：** 生命周期：实例化 -> 注入 -> Aware -> 前置处理 -> 初始化 -> 后置处理 -> 使用 -> 销毁。

## 21. Bean 的初始化和销毁方法有哪些？

**通俗理解：** 初始化方法用于 Bean 准备好前做准备工作；销毁方法用于容器关闭前释放资源。

**专业回答：** 初始化方式包括 `@PostConstruct`、实现 `InitializingBean`、配置 `init-method`、`@Bean(initMethod = "...")`。销毁方式包括 `@PreDestroy`、实现 `DisposableBean`、配置 `destroy-method`、`@Bean(destroyMethod = "...")`。实际开发更常用注解或 `@Bean` 属性，避免业务类强依赖 Spring 接口。

**记忆版：** 初始化：PostConstruct/afterPropertiesSet/init-method；销毁：PreDestroy/destroy/destroy-method。

## 22. 什么是 Spring 内部 Bean？

**通俗理解：** 内部 Bean 就是只在某个 Bean 内部使用的 Bean，像内部配件，不单独暴露出来。

**专业回答：** 内部 Bean 是定义在另一个 Bean 属性或构造参数内部的 Bean，一般不能被外部独立引用，生命周期依附于外部 Bean。它适合表达“该对象只服务于某个 Bean”的关系。现代项目中更常使用注解和 Java Config 表达这种依赖。

**记忆版：** 内部 Bean = 外部 Bean 的私有依赖。

## 23. Spring 如何注入集合？

**通俗理解：** 如果一个对象需要一组值或一组依赖，Spring 可以把 List、Set、Map、Properties 注入进去。

**专业回答：** XML 中可以使用 `<list>`、`<set>`、`<map>`、`<props>` 注入集合。注解和 Java Config 中也可以直接注入 `List<接口>`、`Map<String, Bean类型>`，Spring 会根据类型收集匹配的 Bean。集合注入适合策略列表、处理器链、配置映射等场景。

**记忆版：** 集合注入记四类：List、Set、Map、Properties。

## 24. 什么是 Bean 装配和自动装配？

**通俗理解：** 装配就是把 Bean 和它依赖的其他 Bean 组装到一起；自动装配就是让 Spring 根据名称或类型自动帮你找依赖。

**专业回答：** Bean 装配指 Spring 容器根据依赖关系把多个 Bean 组合起来。自动装配是容器根据规则自动解析依赖并注入 Bean，常见方式有 XML 的 `autowire`，以及注解中的 `@Autowired`、`@Resource`、`@Inject`。自动装配能减少配置，但在多个候选 Bean 存在时需要配合名称、`@Qualifier` 或 `@Primary` 消除歧义。

**记忆版：** 装配 = 组依赖；自动装配 = 容器自动找依赖。

## 25. XML 中自动装配有哪些方式？

**通俗理解：** XML 自动装配可以按名字找、按类型找，也可以按构造器参数找。

**专业回答：** XML 自动装配常见模式包括：`no`，默认不自动装配；`byName`，按属性名匹配 Bean 名称；`byType`，按属性类型匹配 Bean；`constructor`，按构造器参数类型装配；早期还有 `autodetect`，自动判断构造器或 byType，较新版本已不推荐。

**记忆版：** XML 自动装配：no、byName、byType、constructor。

## 26. `@Autowired` 的装配过程是什么？

**通俗理解：** `@Autowired` 先按类型找 Bean；如果找到多个，再结合名称、`@Qualifier` 等进一步确定。

**专业回答：** Spring 通过 `AutowiredAnnotationBeanPostProcessor` 处理 `@Autowired`。默认按类型查找候选 Bean；如果只有一个，直接注入；如果有多个，会结合 `@Primary`、`@Qualifier`、字段名/参数名等规则确定；如果找不到且 `required=true`，容器启动会抛异常；设置 `required=false` 可以允许依赖不存在。

**记忆版：** `@Autowired`：先类型，多个再限定，找不到默认报错。

## 27. 自动装配有哪些局限性？

**通俗理解：** 自动装配方便，但遇到多个同类型 Bean 时可能不知道该选谁。

**专业回答：** 自动装配的局限包括：多个候选 Bean 时可能产生歧义；基本类型、字符串等简单值不适合自动装配；隐式依赖过多会降低代码可读性；不如显式配置精确。因此复杂场景建议配合 `@Qualifier`、`@Primary` 或构造器显式表达依赖。

**记忆版：** 自动装配怕歧义；复杂依赖要显式。

## 28. Spring 可以注入 null 和空字符串吗？

**通俗理解：** 可以。空字符串就是 `""`，`null` 表示没有值，配置时可以明确告诉 Spring。

**专业回答：** Spring XML 中可以通过 `<null/>` 注入 null，通过 `<value></value>` 或空字符串值注入空字符串。Java Config 中则可以直接返回或设置对应值。但业务上应谨慎注入 null，避免空指针问题。

**记忆版：** 能注入 null 和空字符串，但业务上少用 null。

## 29. 什么是基于 Java 的 Spring 注解配置？

**通俗理解：** 不写 XML，也可以用 Java 类和注解告诉 Spring 哪些对象要交给容器。

**专业回答：** Java Config 使用 `@Configuration` 标记配置类，使用 `@Bean` 标记方法返回对象并注册为 Bean。它具有类型安全、易重构、便于条件配置等优点，是现代 Spring 项目常用配置方式。

**示例：**

```java
@Configuration
public class AppConfig {
    @Bean
    public UserService userService() {
        return new UserService();
    }
}
```

**记忆版：** `@Configuration` 定义配置类，`@Bean` 注册对象。

## 30. `@Component`、`@Controller`、`@Service`、`@Repository` 有什么区别？

**通俗理解：** 它们本质都能把类交给 Spring 管理，只是语义不同：控制层、业务层、数据层各用各的。

**专业回答：** `@Component` 是通用组件注解。`@Controller` 用于 Web 控制层。`@Service` 用于业务服务层，表达业务意图。`@Repository` 用于 DAO/持久层，并能配合 Spring 将持久层异常转换为统一的 `DataAccessException`。这些注解都有组件扫描注册 Bean 的作用。

**记忆版：** Component 通用，Controller 控制层，Service 业务层，Repository 数据层。

## 31. `@Autowired`、`@Resource`、`@Qualifier` 有什么区别？

**通俗理解：** `@Autowired` 主要按类型找，`@Resource` 默认按名字找，`@Qualifier` 用来告诉 Spring 具体选哪个。

**专业回答：** `@Autowired` 是 Spring 提供的注解，默认按类型装配，可配合 `@Qualifier` 指定 Bean 名称。`@Resource` 来自 JSR-250，默认按名称装配，找不到名称时再按类型装配。`@Qualifier` 通常与 `@Autowired` 搭配，用于多个同类型候选 Bean 时消除歧义。

**记忆版：** Autowired 按类型，Resource 按名称，Qualifier 指定具体 Bean。

## 32. `@Required` 注解有什么作用？

**通俗理解：** 它要求某个属性必须被设置，否则容器初始化时报错。

**专业回答：** `@Required` 用于 Setter 方法，表示该属性必须在配置阶段被注入，否则抛出 `BeanInitializationException`。不过该注解在新版本 Spring 中已经不推荐使用，现代项目更推荐构造器注入或校验注解表达必需依赖。

**记忆版：** `@Required` = 属性必须注入；现代项目少用。

## 33. Spring 如何更高效地使用 JDBC？

**通俗理解：** 原生 JDBC 要自己开连接、关连接、处理异常，很繁琐；Spring 用 `JdbcTemplate` 帮你封装这些重复代码。

**专业回答：** Spring JDBC 通过 `JdbcTemplate` 简化数据库访问，统一处理连接获取、资源释放、异常转换、SQL 执行和结果映射。开发者只需要关注 SQL、参数和结果处理。常见类包括 `JdbcTemplate`、`NamedParameterJdbcTemplate`、`SimpleJdbcInsert`、`SimpleJdbcCall` 等。

**记忆版：** `JdbcTemplate` = 封装 JDBC 样板代码，开发者专注 SQL。

## 34. Spring DAO 有什么作用？

**通俗理解：** Spring DAO 让不同持久层技术的异常和访问方式更统一，切换技术时更方便。

**专业回答：** Spring DAO 模块为 JDBC、Hibernate、JPA、JDO 等数据访问技术提供统一支持，尤其是统一异常体系。它可以把底层技术相关异常转换为 Spring 的 `DataAccessException`，降低业务代码对具体持久层技术的依赖。

**记忆版：** Spring DAO = 统一数据访问 + 统一异常。

## 35. Spring 如何集成 ORM 框架？

**通俗理解：** Spring 可以把 Hibernate、JPA、MyBatis 等框架纳入统一的 Bean 和事务管理中。

**专业回答：** Spring 通过 ORM 集成模块支持 Hibernate、JPA、JDO、iBATIS/MyBatis 等持久层框架。它可以统一管理 `SessionFactory`、`EntityManagerFactory`、Mapper、事务边界和异常转换，使 ORM 框架与 Spring IoC、事务管理自然结合。

**记忆版：** Spring 集成 ORM：统一对象、事务、异常。

## 36. Spring 支持哪些事务管理方式？

**通俗理解：** 一种是自己写代码控制事务，另一种是用注解/配置让 Spring 自动控制事务。

**专业回答：** Spring 支持编程式事务和声明式事务。编程式事务通过 `TransactionTemplate` 或事务管理器手动控制提交回滚，灵活但侵入业务代码。声明式事务通过 XML 或 `@Transactional` 管理事务，业务代码侵入小，实际项目最常用。

**记忆版：** 编程式灵活但侵入；声明式常用、简洁。

## 37. Spring 事务的实现原理是什么？

**通俗理解：** Spring 本身不凭空实现数据库事务，它是在方法外面套一层代理，帮你开启、提交或回滚数据库事务。

**专业回答：** Spring 事务本质依赖底层数据库或资源管理器的事务能力。声明式事务基于 AOP 代理实现：调用被 `@Transactional` 标记的方法时，事务拦截器会在方法执行前开启事务，方法正常结束则提交，抛出符合规则的异常则回滚。真正提交和回滚由 JDBC Connection、JPA EntityManager 或其他事务资源完成。

**记忆版：** Spring 事务 = AOP 代理控制边界 + 数据库真正提交回滚。

## 38. Spring 事务传播行为有哪些？

**通俗理解：** 传播行为解决的是“一个事务方法调用另一个事务方法时，事务该共用还是新建”的问题。

**专业回答：** 常见传播行为包括：`REQUIRED`，有事务就加入，没有就新建，默认最常用；`SUPPORTS`，有事务就加入，没有就非事务执行；`MANDATORY`，必须存在事务，否则报错；`REQUIRES_NEW`，总是新建事务，并挂起当前事务；`NOT_SUPPORTED`，以非事务执行，挂起当前事务；`NEVER`，必须非事务执行；`NESTED`，存在事务则创建嵌套事务，否则类似 REQUIRED。

**记忆版：** REQUIRED 最常用；REQUIRES_NEW 新开；NESTED 嵌套；MANDATORY/NEVER 是强约束。

## 39. Spring 事务隔离级别有哪些？

**通俗理解：** 隔离级别决定多个事务同时操作数据时，能不能看到别人没提交或刚修改的数据。

**专业回答：** Spring 事务隔离级别包括：`DEFAULT`，使用数据库默认级别；`READ_UNCOMMITTED`，可能脏读、不可重复读、幻读；`READ_COMMITTED`，避免脏读；`REPEATABLE_READ`，避免脏读和不可重复读，MySQL 默认；`SERIALIZABLE`，最高隔离级别，串行执行，性能成本最高。

**记忆版：** Spring 隔离跟数据库一致；MySQL 默认 REPEATABLE_READ。

## 40. 你更倾向使用哪种事务管理方式？

**通俗理解：** 大多数业务开发用声明式事务，写起来干净，也不容易把事务代码散落到业务里。

**专业回答：** 实际项目更推荐声明式事务，因为它对业务代码侵入小，配置简单，便于统一管理事务边界。只有在事务边界非常细、需要在一个方法内部精确控制多个事务片段时，才考虑编程式事务。

**记忆版：** 默认声明式；需要精细控制才编程式。

## 41. 什么是 AOP？

**通俗理解：** AOP 就是把日志、权限、事务这些很多地方都会用的公共逻辑抽出来，统一插到业务方法前后。

**专业回答：** AOP 是 Aspect-Oriented Programming，面向切面编程，是对 OOP 的补充。它将日志、安全、事务、监控等横切关注点从业务代码中抽离，通过切面统一增强目标方法，降低重复代码和模块耦合。Spring AOP 主要通过动态代理实现。

**记忆版：** AOP = 抽公共增强逻辑，统一织入业务方法。

## 42. Spring AOP 和 AspectJ AOP 有什么区别？

**通俗理解：** Spring AOP 是运行时用代理包一层；AspectJ 更底层，可以在编译期或类加载期把增强织进字节码。

**专业回答：** Spring AOP 基于动态代理，运行时创建代理对象，只支持方法级连接点，使用简单且与 Spring 容器集成好。AspectJ 是更完整的 AOP 框架，支持编译期、类加载期织入，连接点类型更丰富，性能通常更好，但需要额外编译器或织入配置。

**记忆版：** Spring AOP 运行时代理、只拦方法；AspectJ 能编译期织入、功能更强。

## 43. JDK 动态代理和 CGLIB 动态代理有什么区别？

**通俗理解：** JDK 动态代理要求目标类有接口；CGLIB 不要求接口，它通过生成子类来代理。

**专业回答：** JDK 动态代理基于接口，通过 `Proxy` 和 `InvocationHandler` 生成代理类，只能代理接口方法。CGLIB 基于继承生成目标类子类，重写方法实现增强，不要求目标类实现接口。但 CGLIB 不能代理 `final` 类和 `final` 方法。Spring AOP 默认有接口时优先 JDK 动态代理，无接口时使用 CGLIB。

**记忆版：** 有接口 JDK；无接口 CGLIB；final 不能被 CGLIB 代理。

## 44. Spring AOP 中有哪些核心术语？

**通俗理解：** AOP 术语可以理解成：在哪里插、插什么、插到谁身上、最终生成什么代理对象。

**专业回答：** 核心术语包括：`Aspect` 切面，通知和切点的组合；`Join point` 连接点，Spring AOP 中通常是方法执行；`Pointcut` 切点，用于匹配连接点；`Advice` 通知，真正增强逻辑；`Target` 目标对象，被增强对象；`Proxy` 代理对象；`Weaving` 织入，把切面应用到目标对象生成代理的过程。

**记忆版：** 切面 = 切点 + 通知；切点定位置，通知写真正增强。

## 45. Spring 通知有哪些类型？

**通俗理解：** 通知就是增强代码，可以放在方法前、方法后、异常时，或者把整个方法包起来。

**专业回答：** 常见通知类型包括：前置通知 `Before`，目标方法前执行；后置通知 `After`，方法结束后执行；返回通知 `AfterReturning`，方法正常返回后执行；异常通知 `AfterThrowing`，方法抛异常后执行；环绕通知 `Around`，包裹目标方法，能在执行前后增强，也能决定是否继续调用目标方法。

**记忆版：** 通知五类：前、后、返回、异常、环绕。

## 46. Spring AOP 为什么只支持方法级连接点？

**通俗理解：** 因为 Spring AOP 是靠代理对象拦截方法调用实现的，所以它天然关注“方法调用”。

**专业回答：** Spring AOP 基于动态代理，代理对象主要拦截外部对目标对象方法的调用，因此只支持方法执行这一类连接点。不支持字段访问、构造器调用等更底层连接点。如果需要这些能力，需要使用 AspectJ。

**记忆版：** Spring AOP 靠代理拦方法；字段/构造器找 AspectJ。

## 47. 关注点和横切关注点有什么区别？

**通俗理解：** 关注点是某个模块关心的功能；横切关注点是很多模块都关心的公共功能，比如日志、权限、事务。

**专业回答：** Concern 指应用中的某个功能或模块行为。Cross-cutting concern 指横跨多个模块的公共关注点，会分散在很多业务逻辑中，例如日志、安全、事务、监控、缓存等。AOP 的主要目的就是把横切关注点抽离出来统一管理。

**记忆版：** 普通关注点管一个模块；横切关注点横跨很多模块。

## 48. Spring 什么时候创建 AOP 代理对象？

**通俗理解：** Spring 在 Bean 创建和后置处理阶段发现它需要被增强，就会生成一个代理对象放进容器。

**专业回答：** Spring AOP 通常在 Bean 初始化后，通过自动代理创建器和 BeanPostProcessor 判断 Bean 是否匹配切点。如果匹配，就为目标 Bean 创建代理对象，并将代理对象作为最终 Bean 暴露给容器。之后外部调用 Bean 方法时，实际调用的是代理对象。

**记忆版：** Bean 初始化后匹配切点，Spring 暴露代理对象。

## 49. Spring AOP 的核心应用场景有哪些？

**通俗理解：** AOP 适合处理“很多业务方法都要做，但又不是核心业务”的公共逻辑，比如日志、事务、权限。

**专业回答：** Spring AOP 常用于声明式事务、统一日志记录、权限校验、接口限流、性能监控、异常统一处理、缓存处理、审计追踪等横切场景。这些逻辑如果直接写进每个业务方法，会造成大量重复代码；使用 AOP 可以将公共逻辑抽成切面，通过切点匹配目标方法，在方法前后统一增强。

**记忆版：** AOP 场景：事务、日志、权限、限流、监控、异常、缓存。
