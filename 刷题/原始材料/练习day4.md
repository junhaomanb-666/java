1.

![78468122510](C:\Users\mjhqu\AppData\Local\Temp\1784681225102.png)

左连接之后得到的行数>=左边表行数，举例：左表是学生姓名，右表是学生成绩。左连接，当一个学生有多条成绩，那么得到的左连接之后的行数为2，原左表行数为1。既，1对N就是大于。其余都是等于



2.

![78468182561](C:\Users\mjhqu\AppData\Local\Temp\1784681825611.png)

A.查询的是最近30天  B.左边是完整日期时间，比如2026-07-22 10:30:00，右边是字符串：202607 没有比较意义  D.只比较了月份 没有年份

3.![78469852912](C:\Users\mjhqu\AppData\Local\Temp\1784698529123.png)

![78469854114](C:\Users\mjhqu\AppData\Local\Temp\1784698541149.png)

4.

![78469996532](C:\Users\mjhqu\AppData\Local\Temp\1784699965325.png)

正确的多重catch顺序应该是从最具体的异常到最一般的异常 先子类后父类

  ArithmeticException 是算数异常 

  NumberFormatException 是数据格式异常 

  Exception 异常 

  ArrayIndexOutOfBoundException 数组索引超过界限异常 



5.

![78470014453](C:\Users\mjhqu\AppData\Local\Temp\1784700144538.png)

`StringBuffer` 线程安全（同步），`StringBuilder` 非线程安全



6.

![78470021582](C:\Users\mjhqu\AppData\Local\Temp\1784700215827.png)

  start()方法是启动一个线程，此时的线程处于就绪状态，但并不一定就会执行，还需要等待CPU的调度。

  run()方法才是线程获得CPU时间，开始执行的点。



7.

![78470026802](C:\Users\mjhqu\AppData\Local\Temp\1784700268026.png)

答案：**A、C、D 错误**。

这里的“类方法”一般指 **static 方法**。

------

## A 错误

> 在类方法中可用 `this` 来调用本类的类方法

错误。`this` 代表当前对象，而 `static` 方法属于类，不属于某个具体对象。

```
class Test {
    static void m1() {}

    static void m2() {
        // this.m1(); // 错误：static方法中不能使用this
    }
}
```

------

## B 正确

> 在类方法中调用本类的类方法时可直接调用

正确。

```
class Test {
    static void m1() {}

    static void m2() {
        m1(); // 正确
    }
}
```

也可以写成：

```
Test.m1();
```

------

## C 错误

> 在类方法中只能调用本类中的类方法

错误。类方法也可以调用其他类的类方法。

```
class A {
    static void hello() {}
}

class B {
    static void test() {
        A.hello(); // 正确，调用其他类的类方法
    }
}
```

------

## D 错误

> 在类方法中绝对不能调用实例方法

错误。类方法中不能**直接**调用实例方法，但可以通过对象调用。

```
class Test {
    void instanceMethod() {}

    static void staticMethod() {
        Test t = new Test();
        t.instanceMethod(); // 正确，通过对象调用实例方法
    }
}
```

不能这样写：

```
static void staticMethod() {
    // instanceMethod(); // 错误，没有对象
}
```



8.

![78470087527](C:\Users\mjhqu\AppData\Local\Temp\1784700875275.png)

`Object` 类中常见方法有：

```
hashCode()
equals()
toString()
getClass()
clone()
finalize()
wait()
notify()
notifyAll()
```



9.

![78470130597](C:\Users\mjhqu\AppData\Local\Temp\1784701305972.png)

![img](https://uploadfiles.nowcoder.com/images/20221023/627522546_1666493124181/91FF47232CEDE96718C242DDE2AF3691)

 定义字符串的时候看定义时等号右边拼接字符串时有没有使用到变量, 如果有, 则重新创建一个新的对象 



10.

![78470136978](C:\Users\mjhqu\AppData\Local\Temp\1784701369783.png)

复制的效率System.arraycopy>clone>Arrays.copyOf>for循环，这里面在System类源码中给出了arraycopy的方法，是native方法，也就是本地方法，肯定是最快的。而Arrays.copyOf(注意是Arrays类，不是Array)的实现，在源码中是调用System.arraycopy的，多了一个步骤，肯定就不是最快的。前面几个说System.copyOf的不要看，System类底层根本没有这个方法，自己看看源码就全知道了。 



11.

![78470157735](C:\Users\mjhqu\AppData\Local\Temp\1784701577356.png)

Collection是java.util包下的顶层接口，它是Java集合框架的根接口，定义了所有集合类的共性操作。List、Set等接口都继承自Collection接口。Collection接口规定了所有集合类都必须实现的一组方法，如add()、remove()、contains()等。

Collections是java.util包下的工具类，它提供了一系列用于操作集合的静态方法。比如排序(sort)、查找(binarySearch)、反转(reverse)等实用方法，这些方法可以方便地操作各种集合对象。(一般带s结尾的都是工具类  不可能是接口)



12.

![78470173939](C:\Users\mjhqu\AppData\Local\Temp\1784701739399.png)

## A  不严谨

> volatile 修饰的变量被修改之前会从主存中读取最新的值覆盖掉 CPU 缓存

这个说法不准确。

`volatile` 的核心是：

```
读 volatile 变量时，能读到主内存中的最新值
写 volatile 变量时，会把修改结果刷新到主内存
```

但不能简单说“修改之前一定从主存读取覆盖 CPU 缓存”。尤其是：

```
volatile int count = 0;

count++;
```

`count++` 实际上是：

```
读取 count
加 1
写回 count
```

虽然 volatile 能保证可见性，但不能保证整个 `count++` 是原子操作。

------

## B 正确

> volatile 底层实现遵循 happens-before 原则
>
> `happens-before` 原则就是：**如果操作 A happens-before 操作 B，那么 A 的结果对 B 可见，并且 A 的执行顺序排在 B 之前。**(一个线程对共享变量的修改，另一个线程能不能看见。)

正确。

Java 内存模型中有一条规则：

```
对 volatile 变量的写操作
happens-before
后续对这个 volatile 变量的读操作
```

意思是：

```
volatile boolean flag = false;
int num = 0;

// 线程A
num = 10;
flag = true;

// 线程B
if (flag) {
    System.out.println(num);
}
```

如果线程B读到：

```
flag = true
```

那么它也能看到线程A在写 `flag = true` 之前对 `num` 的修改。

------

## C 错误

> volatile 修饰的共享变量是线程安全的

错误。

`volatile` 只能保证：

```
可见性
一定程度的有序性
```

不能保证：

```
原子性
```

例如：

```
volatile int count = 0;

count++;
```

多线程下仍然不安全。

因为 `count++` 不是一步操作，而是三步：

```
1. 读取 count
2. count + 1
3. 写回 count
```

多个线程同时执行时，仍然会发生数据丢失。

------

## D 正确

> volatile 可以保证被修饰变量在运算时不会进行指令重排

这个按考试理解是正确的。

更严谨地说：

```
volatile 会通过内存屏障禁止相关指令重排序
```

它可以保证 volatile 变量读写前后的操作顺序不会被随意打乱。

经典场景是单例模式中的双重检查锁：

```
private static volatile Singleton instance;
```

这里 `volatile` 是为了防止对象创建过程发生指令重排。