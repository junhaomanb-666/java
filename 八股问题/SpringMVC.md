# Spring MVC 面试题

> 来源：`D:\Documents\QQ_Files\05-Spring MVC面试题.pdf`
>
> 整理原则：按 Spring MVC 概述、核心组件、工作流程、常用注解、参数绑定、视图、异常、拦截器分类整理，去重后统一为“通俗理解 + 专业回答 + 记忆版”。

## 1. 什么是 Spring MVC？

**通俗理解：** Spring MVC 是 Spring 体系里专门处理 Web 请求的框架。浏览器发请求过来，它负责找到对应方法处理，再把结果返回给前端。

**专业回答：** Spring MVC 是基于 Java 的轻量级 Web MVC 框架，采用请求驱动模型，通过模型 Model、视图 View、控制器 Controller 分离，实现 Web 层职责解耦。它以 `DispatcherServlet` 为核心，配合处理器映射器、处理器适配器、视图解析器等组件完成请求处理。

**记忆版：** Spring MVC = Spring 的 Web MVC 框架，核心是 DispatcherServlet。

## 2. Spring MVC 有哪些优点？

**通俗理解：** 它把 Web 请求处理流程拆得很清楚，和 Spring 结合自然，也支持多种视图和 REST 接口。

**专业回答：** Spring MVC 的优点包括：与 Spring IoC、AOP、事务等无缝集成；角色分工清晰；支持注解开发；支持多种视图技术，如 JSP、Freemarker、PDF、JSON 等；请求映射灵活；参数绑定和数据转换能力强；适合开发传统 Web 和 REST API。

**记忆版：** 优点：集成 Spring、角色清晰、注解方便、视图多样、REST 友好。

## 3. Spring MVC 的主要组件有哪些？

**通俗理解：** 一次请求进来，会先到总调度员，再找路由、找适配器、调用控制器，最后解析视图返回。

**专业回答：** 主要组件包括：`DispatcherServlet` 前端控制器，统一接收请求并调度；`HandlerMapping` 处理器映射器，根据 URL 查找 Handler；`HandlerAdapter` 处理器适配器，调用具体 Handler；`Handler` 控制器方法，处理业务请求；`ViewResolver` 视图解析器，将逻辑视图名解析为具体 View；`View` 视图，负责渲染结果。

**记忆版：** 核心组件：前端控制器、映射器、适配器、处理器、视图解析器、视图。

## 4. 什么是 DispatcherServlet？

**通俗理解：** `DispatcherServlet` 是 Spring MVC 的总入口，所有请求先到它这里，再由它分发给具体控制器。

**专业回答：** `DispatcherServlet` 是 Spring MVC 的前端控制器，负责接收 HTTP 请求、调用 HandlerMapping 查找处理器、调用 HandlerAdapter 执行处理器、处理返回结果、解析视图、渲染响应。它降低了各组件之间的耦合，是 Spring MVC 请求处理流程的核心。

**记忆版：** DispatcherServlet = 请求总入口 + 流程调度中心。

## 5. 什么是 Spring MVC 控制器？

**通俗理解：** 控制器就是处理用户请求的方法所在的类，负责接收参数、调用业务层、返回结果。

**专业回答：** Controller 是表现层组件，通常使用 `@Controller` 或 `@RestController` 标记。它接收 DispatcherServlet 分发的请求，解析参数，调用 Service 处理业务，将结果封装为视图模型或响应体返回。控制器不应写复杂业务逻辑，业务应下沉到 Service 层。

**记忆版：** Controller 管请求入口，业务逻辑交给 Service。

## 6. Spring MVC 控制器是单例吗？有什么线程安全问题？

**通俗理解：** 默认是单例。多个请求会共享同一个 Controller 对象，所以不要在 Controller 里放会被请求修改的成员变量。

**专业回答：** Spring MVC Controller 默认是单例 Bean。单例本身不代表线程安全，如果 Controller 中定义可变成员变量保存请求数据，多线程请求会共享该变量，可能产生数据错乱。解决方式是让 Controller 保持无状态，把请求数据放在方法局部变量、方法参数、Request/Session 或专门的作用域 Bean 中。

**记忆版：** Controller 默认单例；不要写请求级成员变量。

## 7. Spring MVC 的工作流程是什么？

**通俗理解：** 请求先进 DispatcherServlet，然后找处理方法，执行方法，拿到结果，再决定返回页面还是 JSON。

**专业回答：** 流程如下：用户请求到达 `DispatcherServlet`；`DispatcherServlet` 调用 `HandlerMapping` 查找 Handler 和拦截器；调用 `HandlerAdapter` 执行 Handler；Handler 返回 `ModelAndView`、字符串、对象或其他结果；`DispatcherServlet` 根据返回值选择视图解析或消息转换；若是页面，交给 `ViewResolver` 解析并渲染；若是 `@ResponseBody`，通过 `HttpMessageConverter` 写入响应体；最后响应客户端。

**记忆版：** 请求流程：入口 -> 找 Handler -> 适配执行 -> 返回结果 -> 视图/JSON 响应。

## 8. MVC 是什么？有什么好处？

**通俗理解：** MVC 把数据、页面、控制逻辑拆开，让页面展示和业务处理不要混在一起。

**专业回答：** MVC 是 Model-View-Controller。Model 表示模型数据和业务状态，View 负责展示，Controller 负责接收请求并协调模型和视图。好处是职责清晰、降低耦合、便于并行开发、提高可维护性和可扩展性。

**记忆版：** MVC = 模型管数据，视图管展示，控制器管请求。

## 9. Java 注解的原理是什么？

**通俗理解：** 注解本身像贴在代码上的标签，真正生效要靠反射、代理或框架扫描读取这些标签。

**专业回答：** 注解本质上是继承 `Annotation` 的特殊接口。运行期可保留的注解会被编译进 class 文件，框架通过反射读取注解元数据。JDK 在运行时会为注解生成代理对象，调用注解方法时从注解属性值映射中取值。Spring MVC 大量使用注解完成请求映射、参数绑定和响应转换。

**记忆版：** 注解 = 元数据标签；框架通过反射读取并执行规则。

## 10. Spring MVC 常用注解有哪些？

**通俗理解：** 常用注解主要分三类：标记控制器、映射请求、绑定参数/响应 JSON。

**专业回答：** 常见注解包括：`@Controller` 标记控制器；`@RestController` 等价于 `@Controller + @ResponseBody`；`@RequestMapping`、`@GetMapping`、`@PostMapping` 映射请求；`@RequestParam` 获取请求参数；`@PathVariable` 获取路径变量；`@RequestBody` 接收 JSON 请求体；`@ResponseBody` 将返回对象写入响应体；`@ModelAttribute` 绑定模型属性；`@SessionAttributes` 将模型数据放入 Session。

**记忆版：** 常用注解：Controller、RequestMapping、RequestParam、PathVariable、RequestBody、ResponseBody。

## 11. `@Controller` 和 `@RestController` 有什么区别？

**通俗理解：** `@Controller` 常用于返回页面；`@RestController` 常用于返回 JSON。

**专业回答：** `@Controller` 标记控制器类，方法返回值默认会被当作视图名解析，若要返回 JSON 需要配合 `@ResponseBody`。`@RestController` 是组合注解，相当于 `@Controller + @ResponseBody`，类中方法返回值默认写入 HTTP 响应体，常用于 REST API。

**记忆版：** 页面用 Controller；接口 JSON 多用 RestController。

## 12. `@RequestMapping` 有什么作用？

**通俗理解：** 它负责把某个 URL 请求绑定到某个控制器类或方法上。

**专业回答：** `@RequestMapping` 用于请求路径映射，可标注在类或方法上。常用属性包括：`value/path` 指定 URL；`method` 指定 GET、POST 等请求方式；`params` 指定必须包含的请求参数；`headers` 指定请求头条件；`consumes` 指定请求提交内容类型；`produces` 指定响应内容类型。

**记忆版：** RequestMapping = URL + 请求方法 + 参数/头/内容类型条件。

## 13. `@RequestBody` 和 `@ResponseBody` 有什么区别？

**通俗理解：** `@RequestBody` 是把前端 JSON 读成 Java 对象；`@ResponseBody` 是把 Java 对象写成 JSON 返回给前端。

**专业回答：** `@RequestBody` 用于读取 HTTP 请求体，通过 `HttpMessageConverter` 将 JSON、XML 等内容转换为 Java 对象。`@ResponseBody` 用于将方法返回值通过 `HttpMessageConverter` 转换为 JSON、XML 等格式并写入响应体。二者常用于前后端分离接口。

**记忆版：** RequestBody 管入参请求体，ResponseBody 管返回响应体。

## 14. `@PathVariable` 和 `@RequestParam` 有什么区别？

**通俗理解：** `@PathVariable` 从 URL 路径里取值，`@RequestParam` 从问号后面的参数里取值。

**专业回答：** `@PathVariable` 用于获取路径模板变量，例如 `/user/{id}` 中的 `id`。`@RequestParam` 用于获取请求参数，例如 `/user?id=1` 中的 `id`。前者更适合 RESTful 风格资源路径，后者更适合查询条件、表单参数。

**示例：**

```java
@GetMapping("/user/{id}")
public User getById(@PathVariable Long id) {
    return userService.getById(id);
}

@GetMapping("/user")
public List<User> list(@RequestParam String name) {
    return userService.listByName(name);
}
```

**记忆版：** 路径变量 PathVariable，查询参数 RequestParam。

## 15. Spring MVC 和 Struts2 有什么区别？

**通俗理解：** Spring MVC 更轻、更贴近方法；Struts2 更偏向类和成员变量，线程安全处理更麻烦。

**专业回答：** Spring MVC 的前端控制器是 Servlet，即 `DispatcherServlet`；Struts2 的前端控制器是 Filter。Spring MVC 基于方法处理请求，参数通过方法形参绑定，Controller 默认单例但通常无状态，线程安全更容易控制。Struts2 基于类，常通过成员变量接收参数，Action 通常多例。Spring MVC 是 Spring 框架一部分，整合成本更低，企业项目中使用更广泛。

**记忆版：** Spring MVC 是 Servlet + 方法级；Struts2 是 Filter + 类级/值栈。

## 16. Spring MVC 如何设置转发和重定向？

**通俗理解：** 返回字符串前加 `forward:` 表示服务器内部转发；加 `redirect:` 表示让浏览器重新发请求。

**专业回答：** Spring MVC 中可以通过返回值前缀控制跳转：`forward:` 表示请求转发，地址栏不变，共享同一次 request；`redirect:` 表示重定向，客户端重新请求新地址，地址栏变化，默认不共享 request 数据。

**示例：**

```java
return "forward:/user/detail";
return "redirect:/user/list";
```

**记忆版：** forward 服务器内部转；redirect 浏览器重新请求。

## 17. Spring MVC 如何和 AJAX 配合？

**通俗理解：** 前端 AJAX 发 JSON，请求到 Controller；Controller 用 `@RequestBody` 接收，用 `@ResponseBody` 或 `@RestController` 返回 JSON。

**专业回答：** Spring MVC 通过 `HttpMessageConverter` 完成 JSON 与 Java 对象之间的转换。项目中引入 Jackson 等 JSON 库后，可以使用 `@RequestBody` 接收 JSON 请求体，使用 `@ResponseBody` 或 `@RestController` 返回对象、集合等数据，框架会自动序列化为 JSON。

**记忆版：** AJAX 对接：Jackson + RequestBody + ResponseBody/RestController。

## 18. 如何解决 POST 和 GET 请求中文乱码？

**通俗理解：** POST 乱码通常用编码过滤器统一设置 UTF-8；GET 乱码通常检查服务器连接器编码。

**专业回答：** POST 请求乱码可配置 `CharacterEncodingFilter`，统一设置请求和响应编码为 UTF-8。GET 请求参数乱码通常与服务器 URI 解码有关，可在 Tomcat Connector 中设置 `URIEncoding="UTF-8"`。现代 Spring Boot 项目通常通过配置项统一处理编码。

**示例：**

```xml
<filter>
    <filter-name>characterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>characterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

**记忆版：** POST 用编码过滤器；GET 看服务器 URIEncoding。

## 19. Spring MVC 如何处理异常？

**通俗理解：** 不要每个 Controller 都到处 `try-catch`，可以让 Spring 统一捕获异常并返回页面或 JSON。

**专业回答：** Spring MVC 异常处理方式包括：实现 `HandlerExceptionResolver`；使用 `@ExceptionHandler` 处理当前 Controller 异常；使用 `@ControllerAdvice + @ExceptionHandler` 做全局异常处理；返回统一错误页面或统一 JSON 响应。实际项目常用全局异常处理器。

**记忆版：** 异常处理：局部 ExceptionHandler，全局 ControllerAdvice。

## 20. 如何限制某个方法只处理 GET 请求？

**通俗理解：** 在映射注解里指定请求方式，或者直接使用 `@GetMapping`。

**专业回答：** 可以使用 `@RequestMapping(method = RequestMethod.GET)` 限制请求方法，也可以使用组合注解 `@GetMapping`。类似地，POST、PUT、DELETE 可分别使用 `@PostMapping`、`@PutMapping`、`@DeleteMapping`。

**示例：**

```java
@RequestMapping(value = "/user", method = RequestMethod.GET)
public String list() {
    return "userList";
}
```

**记忆版：** 限 GET：`method = GET` 或 `@GetMapping`。

## 21. 如何在 Controller 方法中获取 Request、Session？

**通俗理解：** 直接把 `HttpServletRequest`、`HttpSession` 写到方法参数里，Spring 会自动传进来。

**专业回答：** Spring MVC 支持在控制器方法参数中声明 Servlet API 对象，如 `HttpServletRequest`、`HttpServletResponse`、`HttpSession`，框架会自动注入当前请求对应对象。也可以通过注解绑定参数，减少对 Servlet API 的直接依赖。

**示例：**

```java
@GetMapping("/profile")
public String profile(HttpServletRequest request, HttpSession session) {
    Object user = session.getAttribute("user");
    return "profile";
}
```

**记忆版：** 方法参数写 Request/Session，Spring 自动给。

## 22. 如何获取前台传入的参数或对象？

**通俗理解：** 单个参数直接写同名形参；一组参数可以封装成对象，Spring 会按字段名自动赋值。

**专业回答：** Spring MVC 支持通过方法参数绑定请求参数。简单参数可使用同名形参或 `@RequestParam`；路径参数用 `@PathVariable`；表单对象可直接声明 Java Bean，框架按属性名自动绑定；JSON 请求体使用 `@RequestBody` 转换为对象。

**记忆版：** 单值用参数，对象用 Java Bean，JSON 用 RequestBody。

## 23. Spring MVC 方法返回值有哪些？

**通俗理解：** 可以返回页面名、数据模型加页面，也可以直接返回 JSON 数据。

**专业回答：** 常见返回值包括：`String`，通常表示逻辑视图名，也可配合 `forward:`/`redirect:`；`ModelAndView`，同时包含模型和视图；对象或集合，配合 `@ResponseBody` 返回 JSON；`void`，直接操作响应；`ResponseEntity`，可控制状态码、响应头和响应体。

**记忆版：** 返回页面用 String/ModelAndView；返回接口用对象/ResponseEntity。

## 24. Spring MVC 如何从后台向前台传递数据？

**通俗理解：** 返回页面时，把数据放进 `Model` 或 `ModelMap`，页面就能取到。

**专业回答：** Spring MVC 可通过 `Model`、`ModelMap`、`Map` 或 `ModelAndView` 向视图传递数据。数据默认放入 request 域，JSP 可通过 EL 表达式获取。若需要放入 Session，可使用 `@SessionAttributes` 或直接操作 `HttpSession`。

**示例：**

```java
@GetMapping("/user")
public String user(Model model) {
    model.addAttribute("name", "Tom");
    return "user";
}
```

**记忆版：** 页面传值用 Model；跨请求会话用 Session。

## 25. `@SessionAttributes` 有什么作用？

**通俗理解：** 它可以把 Model 里的某些数据同步放到 Session 里，让多个请求都能用。

**专业回答：** `@SessionAttributes` 标注在 Controller 类上，用于将指定名称或类型的模型属性暂存到 Session 中。它适合短流程页面表单等场景。普通登录态、用户信息等更常直接使用 `HttpSession`、Spring Security 或分布式 Session 方案。

**记忆版：** SessionAttributes = Model 中指定 key 放入 Session。

## 26. Spring MVC 拦截器怎么写？

**通俗理解：** 拦截器可以在 Controller 方法执行前后插入逻辑，比如登录校验、权限检查、日志记录。

**专业回答：** Spring MVC 拦截器通常实现 `HandlerInterceptor`，核心方法包括 `preHandle`、`postHandle`、`afterCompletion`。`preHandle` 在 Handler 执行前调用，可决定是否放行；`postHandle` 在 Handler 执行后、视图渲染前调用；`afterCompletion` 在请求完成后调用，适合资源清理和日志。

**示例：**

```java
public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request,
                             HttpServletResponse response,
                             Object handler) {
        return request.getSession().getAttribute("user") != null;
    }
}
```

**记忆版：** 拦截器三步：前置 preHandle、后置 postHandle、完成 afterCompletion。

## 27. Spring MVC 拦截器和 Filter 有什么区别？

**通俗理解：** Filter 是 Servlet 规范里的，更靠前；Interceptor 是 Spring MVC 里的，更懂 Controller。

**专业回答：** Filter 属于 Servlet 规范，作用在请求进入 Servlet 前后，能拦截几乎所有 Web 请求。Interceptor 属于 Spring MVC，作用在 DispatcherServlet 之后、Controller 前后，可以访问 Handler、ModelAndView 等 Spring MVC 上下文。过滤器更适合编码、跨域、通用安全过滤；拦截器更适合登录校验、权限、日志等 MVC 层逻辑。

**记忆版：** Filter 更外层，Interceptor 更贴近 Controller。

## 28. 什么是 WebApplicationContext？

**通俗理解：** 它是 Web 环境下的 Spring 容器，比普通 ApplicationContext 多了 Web 相关能力。

**专业回答：** `WebApplicationContext` 继承自 `ApplicationContext`，增加了 Web 应用所需能力，能访问 ServletContext、处理主题资源，并与具体 Servlet 关联。Spring MVC 中通常根容器管理 Service、DAO 等 Bean，DispatcherServlet 子容器管理 Controller、ViewResolver 等 Web 层 Bean。

**记忆版：** WebApplicationContext = Web 版 Spring 容器。

