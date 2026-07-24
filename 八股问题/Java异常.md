# Java 异常

> 本文件已按“通俗理解 + 专业回答 + 记忆版”整理。重复问题已合并。

## 1. Error 和 Exception 有什么区别？

**通俗理解：** `Error` 像是 JVM 或系统层面出了大事故，例如内存爆了；`Exception` 更像程序运行过程中遇到的问题，例如空指针、文件找不到，很多时候可以捕获并处理。

**专业回答：** `Error` 和 `Exception` 都继承自 `Throwable`。`Error` 表示严重的、通常不可恢复的问题，应用程序一般不应该捕获，例如 `OutOfMemoryError`、`StackOverflowError`。`Exception` 表示程序可以处理的异常情况，又分为受检异常和运行时异常。

**记忆版：** `Error` 是系统级大问题，`Exception` 是程序级可处理问题。

## 2. 检查异常与非检查异常有什么区别？

**通俗理解：** 检查异常就是编译器会盯着你处理的异常；非检查异常就是编译器不强制你处理，但运行时可能会炸。

**专业回答：** 检查异常也叫受检异常，通常指除 `RuntimeException` 及其子类以外的 `Exception`，编译期必须通过 `try-catch` 或 `throws` 处理。非检查异常包括 `RuntimeException` 及其子类，以及 `Error`，编译器不强制处理。

**例子：**

- 受检异常：`IOException`、`SQLException`、`ClassNotFoundException`
- 非检查异常：`NullPointerException`、`IndexOutOfBoundsException`、`ClassCastException`

**记忆版：** 编译器强制处理的是受检异常；运行时才暴露的是非检查异常。

## 3. JVM 如何处理异常？

**通俗理解：** 方法里出异常后，JVM 会顺着方法调用链一层一层往外找，看有没有人能接住这个异常。没人接，程序就交给默认处理器打印异常并终止。

**专业回答：** 当方法执行过程中发生异常时，JVM 会创建异常对象并抛出。随后 JVM 会在当前方法的异常表中查找匹配的 `catch` 块；如果找不到，就把异常向调用者传播，沿调用栈继续查找。如果最终没有任何代码处理该异常，则由默认异常处理器处理，通常打印异常栈信息并终止当前线程。

**记忆版：** 异常处理就是“当前方法找，找不到往上抛，没人处理就终止”。

## 4. throw 和 throws 有什么区别？

**通俗理解：** `throw` 是真的把一个异常扔出去；`throws` 是在方法门口贴告示，告诉调用者“我可能会扔这些异常”。

**专业回答：** `throw` 用在方法体内部，后面跟一个具体异常对象，用于主动抛出异常。`throws` 用在方法声明上，后面跟异常类型列表，用于声明该方法可能向外抛出的异常，尤其常用于受检异常。

**示例：**

```java
public void readFile(String path) throws IOException {
    if (path == null) {
        throw new IllegalArgumentException("path cannot be null");
    }
}
```

**记忆版：** `throw` 抛对象，`throws` 声明类型。

## 5. NoClassDefFoundError 和 ClassNotFoundException 有什么区别？

**通俗理解：** `ClassNotFoundException` 是你主动去找一个类，结果没找到；`NoClassDefFoundError` 是程序本来编译时见过这个类，但运行时突然找不到了。

**专业回答：** `ClassNotFoundException` 是受检异常，常见于 `Class.forName()`、类加载器动态加载类时找不到目标类。`NoClassDefFoundError` 是 `Error`，表示 JVM 在运行时需要使用某个类定义，但类路径中找不到该类，常见于编译期存在依赖、运行期缺少 jar 包。

**记忆版：** 主动加载找不到是 `ClassNotFoundException`；运行时依赖缺失是 `NoClassDefFoundError`。

## 6. try-catch-finally 中 catch 执行 return，finally 还会执行吗？

**通俗理解：** 会。即使 `catch` 里准备返回了，`finally` 通常也会先执行完，再真正返回。

**专业回答：** 正常情况下，`finally` 会在方法返回前执行。即使 `try` 或 `catch` 中有 `return`，JVM 也会先保存返回值，再执行 `finally`，最后返回。但如果执行了 `System.exit()`、JVM 崩溃、进程被强制杀死，`finally` 不会执行。

**注意：** 如果 `finally` 里也有 `return`，会覆盖 `try` 或 `catch` 中的返回值，因此实际开发中不建议在 `finally` 里写 `return`。

**记忆版：** `return` 挡不住 `finally`，但 `System.exit()` 可以。

## 7. 常见运行时异常有哪些？

**通俗理解：** 运行时异常大多是代码逻辑不严谨造成的，比如对象是空的还去调用方法，数组越界还去访问。

**专业回答：** 常见 `RuntimeException` 包括：

- `NullPointerException`：空指针异常
- `ClassCastException`：类型转换异常
- `ArrayIndexOutOfBoundsException`：数组下标越界
- `IndexOutOfBoundsException`：集合或序列下标越界
- `NumberFormatException`：字符串转数字格式错误
- `IllegalArgumentException`：非法参数异常
- `ArithmeticException`：算术异常，例如除以 0

**记忆版：** 空指针、越界、强转、数字格式、非法参数，是运行时异常高频组合。

## 8. final、finally、finalize 的区别？

**通俗理解：** `final` 是“不能变”；`finally` 是“最后一定尽量做”；`finalize` 是对象被回收前可能调用的旧方法。

**专业回答：** `final` 是关键字，可以修饰变量、方法和类；修饰变量表示不可重新赋值，修饰方法表示不能被重写，修饰类表示不能被继承。`finally` 是异常处理结构的一部分，通常用于释放资源。`finalize()` 是 `Object` 的方法，可能在垃圾回收前调用，但执行时机不确定，且已经不推荐使用。

**记忆版：** `final` 管定义，`finally` 管收尾，`finalize` 管回收前但不可靠。

## 9. 方法覆盖对异常有什么要求？

**通俗理解：** 子类重写父类方法时，不能比父类“惹更大的麻烦”。

**专业回答：** 子类重写方法不能抛出比父类方法更宽泛的受检异常，可以不抛、抛相同异常、抛更具体的子类异常。运行时异常不受该规则严格限制。

**记忆版：** 重写方法的受检异常范围不能扩大。

## 10. 如何自定义异常？

**通俗理解：** 自定义异常就是给自己业务里的错误起一个专门名字，比如余额不足、库存不足。

**专业回答：** 可以继承 `Exception` 创建受检异常，也可以继承 `RuntimeException` 创建运行时异常。实际业务开发中更常继承 `RuntimeException`，减少大量强制捕获代码。

```java
public class BizException extends RuntimeException {
    public BizException() {
    }

    public BizException(String message) {
        super(message);
    }
}
```

**记忆版：** 业务异常通常继承 `RuntimeException`，并提供带消息的构造方法。
