![78439166833](C:\Users\mjhqu\AppData\Local\Temp\1784391696404.png)

![78439170848](C:\Users\mjhqu\AppData\Local\Temp\1784391708486.png)

![78439195764](C:\Users\mjhqu\AppData\Local\Temp\1784391957648.png)

![78439215934](C:\Users\mjhqu\AppData\Local\Temp\1784392159345.png)

![78439224138](C:\Users\mjhqu\AppData\Local\Temp\1784392241383.png)

![78439253475](C:\Users\mjhqu\AppData\Local\Temp\1784392534759.png)

Arrays.asList() 

  将一个数组转化为一个List对象，这个方***返回一个ArrayList类型的对象， 这个ArrayList类并非java.util.ArrayList类，**而是Arrays类的静态内部类！**用这个对象对列表进行添加删除更新操作，就会报UnsupportedOperationException异常。

ConcurrentHashMap使用segment来分段和管理锁，segment继承自ReentrantLock，因此ConcurrentHashMap使用ReentrantLock来保证线程安全。

![78439267287](C:\Users\mjhqu\AppData\Local\Temp\1784392672871.png)

![78439285312](C:\Users\mjhqu\AppData\Local\Temp\1784392853120.png)

正确答案：**B、C**

**B 错误**

`do-while` 中，`while` 后的条件成立时会**继续循环**，条件不成立时才会结束。

```
do {
    // 循环体
} while (条件表达式);
```

因此，循环结束的条件应是：**条件表达式为 false**。

**C 错误**

`for` 循环的三个表达式都可以省略，但两个分号不能省略：

```
for (;;) {
    // 无限循环
}
```

标准结构为：

```
for (初始化表达式; 条件表达式; 更新表达式) {
}
```

**D 正确**

`while` 和 `for` 都属于条件循环，通常可以相互转换。例如：

```
int i = 0;
while (i < 5) {
    System.out.println(i);
    i++;
}
```

等价于：

```
for (int i = 0; i < 5; i++) {
    System.out.println(i);
}
```

![78439319088](C:\Users\mjhqu\AppData\Local\Temp\1784393190888.png)

![78439335800](C:\Users\mjhqu\AppData\Local\Temp\1784393358001.png)

![78439341891](C:\Users\mjhqu\AppData\Local\Temp\1784393418916.png)

## 原因

Java 中方法参数传递始终是**值传递**。对于引用类型，传递的是“引用值的副本”，并不是严格意义上的引用传递。

### 1. `String str`

调用时：

```
ex.change(ex.str, ex.ch);
```

方法中的参数 `str` 得到的是 `ex.str` 所保存引用的副本。最开始二者都指向字符串 `"good"`：

```
ex.str ──► "good"
str    ──► "good"
```

执行：

```
str = "test ok";
```

只是让方法内部的局部变量 `str` 指向新的字符串：

```
ex.str ──► "good"
str    ──► "test ok"
```

并没有修改 `ex.str`，所以最后：

```
System.out.print(ex.str);
```

输出：

```
good
```

另外，`String` 本身也是不可变对象，但这里最关键的原因是：**修改的是局部参数变量的指向，没有修改成员变量 ex.str。**

------

### 2. `char[] ch`

方法参数 `ch` 和成员变量 `ex.ch` 中保存的是两个相同的引用值，它们都指向同一个字符数组：

```
ex.ch ──┐
        ├──► {'a', 'b', 'c'}
ch    ──┘
```

执行：

```
ch[0] = 'g';
```

不是让 `ch` 指向一个新数组，而是通过 `ch` 修改它所指向的数组内容。

因此原数组变为：

```
{'g', 'b', 'c'}
```

所以：

```
System.out.print(ex.ch);
```

输出：

```
gbc
```

`PrintStream` 对 `char[]` 有专门的重载方法，会直接打印字符数组内容，而不是打印类似 `[C@xxxxxx` 的地址形式。

## 核心结论

```
str = "test ok";
```

属于**改变局部变量的引用指向**，不影响 `ex.str`。

```
ch[0] = 'g';
```

属于**修改引用所指向的对象内容**，因此会影响原字符数组。

原注释：

```
// 引用类型变量，传递的是地址，属于引用传递。
```

不够准确，建议改成：

```
// Java 只有值传递；引用类型传递的是引用值的副本。
```

![img](file:///C:\Users\mjhqu\AppData\Local\Temp\92b1900d-6412-4827-830f-61ce5c6f5e9f.png)

这段代码通过 `sendAsync()` **异步发送 HTTP 请求**，并立即返回一个：

```
CompletableFuture<HttpResponse<String>>
```

请求完成后，`CompletableFuture` 才会保存服务器返回的响应结果。Oracle 文档明确说明，`sendAsync()` 异步发送请求并返回 `CompletableFuture`。([Oracle Docs](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html))

------

## A：错误

> `sendAsync` 默认使用与主线程相同的线程发送请求

`sendAsync()` 是异步方法，不保证使用调用它的主线程执行网络请求。

当前代码没有手动配置 `Executor`，因此 `HttpClient` 的实现可以使用一个**内部的默认执行器**来执行异步任务。这个默认执行器甚至可能不会通过 `client.executor()` 暴露出来。([Oracle Docs](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html))

因此不能认为请求由 `main` 线程执行。

可以手动指定线程池：

```
ExecutorService executor = Executors.newFixedThreadPool(4);

HttpClient client = HttpClient.newBuilder()
        .executor(executor)
        .build();
```

------

## B：错误

> `sendAsync` 返回的 `CompletableFuture` 在请求完成前调用 `join()` 不会阻塞

需要区分两个操作：

```
CompletableFuture<HttpResponse<String>> future =
        client.sendAsync(request, HttpResponse.BodyHandlers.ofString());
```

调用 `sendAsync()` 本身通常会很快返回，不需要等待服务器响应。([Oracle Docs](https://docs.oracle.com/javase/jp/11/docs/api/java.net.http/java/net/http/HttpClient.html))

但是接着调用：

```
HttpResponse<String> response = future.join();
```

当请求尚未完成时，`join()` 会等待结果，因此会**阻塞当前调用线程**。完成后返回结果；如果异步任务异常完成，`join()` 会抛出 `CompletionException`。([Oracle Docs](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/concurrent/CompletableFuture.html))

所以：

```
sendAsync(); // 异步，不等待响应
future.join(); // 结果没完成时，会等待
```

更典型的异步处理方式是：

```
client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
        .thenApply(HttpResponse::body)
        .thenAccept(System.out::println);
```

------

## C：正确

> `HttpClient` 默认使用实现提供的默认 `executor` 来处理异步请求

当前创建方式：

```
HttpClient client = HttpClient.newHttpClient();
```

等价于：

```
HttpClient client = HttpClient.newBuilder().build();
```

因为没有调用：

```
.executor(...)
```

来指定执行器，所以异步任务由 `HttpClient` 实现提供的内部默认执行器处理。Oracle 文档也指出，即使 `client.executor()` 返回空的 `Optional`，客户端内部仍可能存在用于异步任务的默认执行器。([Oracle Docs](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html))

因此 **C 正确**。

------

## D：错误

> `sendAsync` 不支持 HTTP/2 协议

Java 11 的 `HttpClient` 支持：

- HTTP/1.1
- HTTP/2

而且默认首选协议版本就是：

```
HttpClient.Version.HTTP_2
```

当服务器、代理或网络条件不支持 HTTP/2 时，实际请求可能退回 HTTP/1.1。([Oracle Docs](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html))

也可以显式指定：

```
HttpClient client = HttpClient.newBuilder()
        .version(HttpClient.Version.HTTP_2)
        .build();
```

------

## 核心记忆

| 方法                 | 是否阻塞当前线程    | 返回值                               |
| -------------------- | ------------------- | ------------------------------------ |
| `client.send()`      | 是                  | `HttpResponse<T>`                    |
| `client.sendAsync()` | 否，立即返回 Future | `CompletableFuture<HttpResponse<T>>` |
| `future.join()`      | 未完成时会阻塞      | 异步任务的最终结果                   |