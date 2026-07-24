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
