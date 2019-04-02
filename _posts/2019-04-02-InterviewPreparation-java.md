---
title: "Interview Preparation - Java"
published: true
---

# Java

## Collection Related

Collection

|—Set

|      |—HashSet

|      |—TreeSet

|

|—List—ArrayList

​	|—Vector

​	|—LinkedList

方法：

`add(Element e)` 

`addAll(Collection c)`

`remove(Element e)`

`clear();`

`size()`

`isEmpt()`

...



Collection是一个集合interface

Collections是一个包装类（工具类），包含各种有关集合操作的**静态多态方法**，**不能实例化**



### Set Related

TreeSet的底层是红黑树

### List Related

#### ArrayList 

在内存中是顺序储存，默认容量为10（一开始如果是空构造器，长度为0，放入一个元素后长度变成10），扩容增量是×1.5，不可以指定增量，线程不安全

#### Vector

在内存中顺序储存，默认容量为10，扩容增量默认是×2，可以在构造时指定增量，线程安全（加了synchronized）

#### LinkedList

内存中分开储存，线程不安全

## Map Related

常用的有HashMap, Hashtable, LinkedHashMap, TreeMap...



HashMap - 内部是数组 存的key-value对和next，哈希映射，线程不安全，key可以一个是null，value可以多个是null

HashMap - 无序的，随机访问

Hashtable - 线程安全，不允许null

LinkedHashMap - 按读取顺序访问 - 维护了一个双向链表

TreeMap（红黑树） - 按key大小升序访问 - 内部有一个comparable比较器



HashMap - 扩容因子为0.75，当到达容量0.75时，会×2，resize()，rehash（有的需要调整，有的不需要）

## String Related

### String

不可变（在jdk中被声明为final），创建时在（heap区中）创建或者（在heap区中跟static区）中都创建对象



`String str = “aa”`

可能创建一个或者不创建对象。如果”aa”在java String池里不存在，会在java String池里创建一个String对象(“ABC”)，然后str指向这个内存地址。

`String str = new String(“aa”)`

至少创建一个对象，也可能两个。会在heap区创建一个str的String对象。然后如果”aa”在java String池里不存在，会在java String池里创建一个String对象(“ABC”)，然后str指向这个内存地址。

### StringBuilder

可变，线程不安全

### StringBuffer

可变，线程安全

## Memory Related

栈 - 局部变量

堆 - `malloc`, `new`

data - static, global

JAVA new出来的对象都在堆中



`Student s = new Student();`在内存中做了了哪些事情? 

1.  加载Student.class文件进内存 

2.  在栈内存为s开辟空间 

3.  在堆内存为学⽣对象开辟空间

4.  对学生对象的成员变量进⾏初始化

5.  通过构造方法对学生对象的成员变量赋值 

6.  学生对象初始化完毕，把对象地址赋值给s变量



### JMM - java Memory Model

Specifies how the Java virtual machine works with the computer's memory (RAM). 

## JAVA四种引用

强引用 - `String str = new String()` - gc永远不会回收

软引用 - 在快要内存溢出时，会被回收（使用策略，堆可用大小等）

弱引用 - 在下一次gc时被回收

虚引用 - 不影响生存时间，在被gc回收时收到一个系统通知



## JAVA四个基本特性

抽象 - 将一类对象的共同特征总结出来构造类的过程。包括数据抽象和行为抽象

封装 - 把数据和操作封装起来

继承 - 子类继承父类的方法

多态 - 

 overload - 编译时的多态性 - 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。

 override - 运行时的多态性 - 子类对父类的允许访问的方法的实现过程进行重新编写, 返回值和形参都不能改变。

## JAVA编译过程

source code —(compiler)—> bytecode —(JVM) —>interpret & execute

`.java` -> `.class`

**java**字节码的执行有两种方式：

1.  即时编译方式：解释器先将字节编译成机器码，然后再执行该机器码。

2.  解释执行方式：解释器通过每次解释并执行一小段代码来完成java字节码程序的所有操作。

### JIT - just in time - 即时编译器

可以加速java程序的执行速度，（取决于代码结构），只有对频繁执行的代码，JIT编译才能保证有正面的收益

## Others

序列化 - 对象 -> 字节序列

反序列化 - 字节序列 -> 对象

作用：实现数据持久化，实现远程通讯

static的不会被序列化，对象的类名，属性会被序列化，方法不会被序列化



`try…catch…finally…` + `return`

不管有没有`exception`，`finally`都会运行

`try`, `catch`中有`return`，`finally`也会运行

`return`的值是在`finally`运行之前确定的

`finally`中最好不不要包含`return`，否则程序会提前退出，返回值不是`try`或`catch`中保存的返回值。 



JAVA泛型 - 没有继承性

增加代码安全性（编译时检查类型安全），复用性



传统IO - 每一个客户端用一个线程，可能会阻塞。- 基于字节流

NIO - 非阻塞 - 基于块



线程池 - 实现对线程的复用