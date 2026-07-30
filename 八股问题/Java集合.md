# Java 集合

## 1. Java 集合框架的整体结构是什么？分为哪几类？

**答案：** Java 集合主要分为 `Collection` 和 `Map` 两大体系。`Collection` 下有 `List`、`Set`、`Queue`；`Map` 以键值对形式存储数据。

**核心记忆：**

- `List`：有序、可重复
- `Set`：一般无序、不可重复
- `Queue`：队列结构
- `Map`：键值对，key-value

## 2. ArrayList 和 LinkedList 的区别？

**答案：** `ArrayList` 基于动态数组，随机访问快，时间复杂度为 `O(1)`；插入删除相对慢。`LinkedList` 基于双向链表，插入删除快，随机访问慢，时间复杂度为 `O(n)`。

**核心记忆：**

- 查多改少：优先 `ArrayList`
- 增删多：可考虑 `LinkedList`

## 3. HashMap 的底层数据结构？JDK 7 和 JDK 8 有什么区别？

**答案：** JDK 7 中 `HashMap` 的底层是数组 + 链表；JDK 8 中是数组 + 链表 + 红黑树。链表长度大于 8 且数组容量大于 64 时，链表会转为红黑树，以优化查询效率。

**核心记忆：**

- JDK 7：数组 + 链表
- JDK 8：数组 + 链表 + 红黑树
- 树化条件：链表长度大于 8，且数组容量大于 64

## 4. HashSet 如何保证元素不重复？

**答案：** `HashSet` 依赖元素的 `hashCode()` 和 `equals()` 判断是否重复。先比较哈希值，哈希值不同则直接存入；哈希值相同再通过 `equals()` 判断是否相等。

**核心记忆：** `HashSet` 底层依赖 `HashMap`，元素作为 `HashMap` 的 key。

## 5. HashMap 和 Hashtable 的区别？

**答案：** `HashMap` 线程不安全，允许 `null` 键和 `null` 值；`Hashtable` 线程安全，方法使用 `synchronized` 修饰，不允许 `null` 键和 `null` 值。

**核心记忆：**

- `HashMap`：非线程安全，允许 `null`
- `Hashtable`：线程安全，不允许 `null`

## 6. Collection 和 Collections 的区别？

**答案：** `Collection` 是集合体系的根接口；`Collections` 是集合工具类，提供排序、同步化、查找等静态方法。

**核心记忆：**

- `Collection`：接口
- `Collections`：工具类

## 7. 什么是 fail-fast 机制？

**答案：** 在迭代集合时，如果集合结构被非迭代器方式修改，可能抛出 `ConcurrentModificationException`，这就是 fail-fast 机制。

**核心记忆：** fail-fast 是一种快速失败机制，用于尽早发现并发修改或错误修改。

## 8. ConcurrentHashMap 线程安全的实现原理？

**答案：** JDK 7 中 `ConcurrentHashMap` 采用分段锁 `Segment`；JDK 8 中主要采用 CAS + `synchronized`，锁住链表或红黑树的头节点。

**核心记忆：**

- JDK 7：分段锁
- JDK 8：CAS + `synchronized`

## 9. HashSet、LinkedHashSet、TreeSet 的区别？

**答案：** `HashSet` 底层是 `HashMap`，元素无序；`LinkedHashSet` 底层是 `LinkedHashMap`，按插入顺序保存；`TreeSet` 底层是 `TreeMap`，支持自然排序或定制排序。

**核心记忆：**

- `HashSet`：无序
- `LinkedHashSet`：插入顺序
- `TreeSet`：排序

## 10. 为什么重写 equals() 必须重写 hashCode()？

**答案：** 如果只重写 `equals()` 不重写 `hashCode()`，逻辑相等的对象可能产生不同哈希值，导致在 `HashSet`、`HashMap` 等哈希集合中出现重复元素或查找失败。

**核心记忆：** 相等对象必须有相同的哈希值。

## 11. Comparable 与 Comparator 的区别及应用？

**通俗理解：** `Comparable` 是对象自己会比较，像学生类自己规定“按年龄排序”；`Comparator` 是外部给一个比较规则，像临时指定“这次按成绩排序，下次按姓名排序”。

**专业回答：** `Comparable` 位于 `java.lang` 包，类实现该接口并重写 `compareTo()`，表示对象具备天然排序能力，常用于固定的自然排序。`Comparator` 位于 `java.util` 包，需要实现 `compare()`，表示外部比较器，适合不修改类源码或需要多种排序规则的场景。

**简单格式：**

```java
class Student implements Comparable<Student> {
    int age;

    @Override
    public int compareTo(Student other) {
        return this.age - other.age;
    }
}

Comparator<Student> byAge = (a, b) -> a.age - b.age;
```

**应用场景：**

- `Comparable`：类有稳定、默认排序规则，例如按 id、年龄、时间排序。
- `Comparator`：排序规则经常变化，例如按价格升序、销量降序、名称排序。

**记忆版：** `Comparable` 是内部自然排序；`Comparator` 是外部定制排序。

## 12. Iterable 与 Iterator 的区别？

**通俗理解：** `Iterable` 表示“这个对象可以被遍历”；`Iterator` 表示“真正负责一个个取元素的迭代器”。

**专业回答：** `Iterable` 是可迭代接口，定义 `iterator()` 方法，返回一个 `Iterator`。实现 `Iterable` 的对象可以被增强 `for` 循环遍历。`Iterator` 是迭代器接口，负责具体遍历过程，核心方法是 `hasNext()`、`next()`、`remove()`。

**简单格式：**

```java
Iterable<String> iterable = List.of("A", "B", "C");
Iterator<String> iterator = iterable.iterator();

while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

**记忆版：** `Iterable` 管“能不能遍历”，`Iterator` 管“怎么遍历”。

## 13. 描述一下常见 Java 集合框架：数据结构和特点？

**通俗理解：** Java 集合就是一套装数据的容器。不同容器底层结构不同，所以适合的场景也不同。

**专业回答：**

| 集合 | 底层数据结构 | 主要特点 | 常见场景 |
| --- | --- | --- | --- |
| `ArrayList` | 动态数组 | 有序、可重复、随机访问快、增删可能搬移元素 | 查询多、按下标访问多 |
| `LinkedList` | 双向链表 | 有序、可重复、首尾增删方便、随机访问慢 | 队列、首尾操作较多 |
| `HashSet` | 基于 `HashMap` | 无序、不可重复，依赖 `hashCode()` 和 `equals()` | 去重 |
| `LinkedHashSet` | 哈希表 + 双向链表 | 不重复，保留插入顺序 | 去重且需要顺序 |
| `TreeSet` | 红黑树 | 不重复，可自然排序或定制排序 | 排序集合 |
| `HashMap` | 数组 + 链表 + 红黑树 | key 唯一，value 可重复，非线程安全 | 普通 key-value 存储 |
| `LinkedHashMap` | 哈希表 + 双向链表 | 保留插入顺序或访问顺序 | LRU 缓存、顺序 Map |
| `TreeMap` | 红黑树 | key 有序 | 需要按 key 排序 |
| `ConcurrentHashMap` | 数组 + 链表 + 红黑树 + CAS/synchronized | 线程安全，并发性能较好 | 并发场景下的 Map |

**记忆版：** List 管顺序，Set 管去重，Map 管键值；数组查得快，链表增删快，红黑树能排序，哈希表查找快。
