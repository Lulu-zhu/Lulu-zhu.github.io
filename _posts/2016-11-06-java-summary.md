---
layout: post
title: "Java知识点整理"
subtitle: "Java"
author: "Lulu"
header-img: "img/post-bg/javasummary.jpg"
date: 2016-11-06
catalog: true
tags:
    - Java
---

## 前言

本篇文章是Android开发以及Java语言的相关知识点整理。

## Java知识点

在我写这篇文章之时，Java语言的最新JDK版本仍然是2014推出的JDK 1.8。所以，你要注意了，在之后文章中提及的Java语言特性是基于Java8的。

### switch-case语句

switch()的参数不仅可以接受int, short, byte, char和相对应的封装类，还可以接受string以及Enum类型。
此处请你参考Java文档[The Java™ Tutorials-The switch Statement](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html)

### Java数据类型

Java数据类型分为基本数据类型和引用数据类型。基本数据类型分为三类，字符型(char)，布尔型(boolean)和数值型(整数型byte，short，int，long以及浮点型float，double)。引用数据类型也分为三类，类(class)，接口(interface)和数组(array)。此处请你参考Java文档[The Java™ Tutorials-Primitive Data Types](http://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)

### equals与==的区别：`此处请你参考源码`

==是Java中的运算符

对于Java的八种基本数据类型boolean, byte, char, short, int, long, float, double。==比较的是数据值。
对于引用数据类型，==比较的是引用对象实例的内存地址，而不是该实例的内容，这是与基本数据类型不同地方，请你注意。

equals()方法

该方法是继承自Object。所以，很明显，你在这里比较的对象是引用对象实例。在大多数情况下，该方法比较的是实例的内存地址。**请注意**，我这里指的大多数情况，是该对象实例没有重写equals()方法的情况。但是当你在使用Boolean，Double，Float，Integer，Short，Long，String，Date等这些类时，你要明白，上述类已经**重写**了继承的equals()方法。那么此时，这些类是先比较实例的引用对象是否相同。相同的话，接下来会去比较对象实例的内容是否相同。你发现了吧，即使是equals方法，也可能会去比较实例的内容。

### Object方法：[此处参考JDK8的API](http://docs.oracle.com/javase/8/docs/api/)

|Modifier and Type|Method | Description|
|--|--|--|
|protected Object|	clone() |Creates and returns a copy of this object.|
|boolean|equals(Object obj) |Indicates whether some other object is "equal to" this one.|
|protected void|	finalize()|Called by the garbage collector on an object when garbage collection determines that there are no more references to the object.|
|Class<?>|getClass()|Returns the runtime class of this Object.|
|int|hashCode()|Returns a hash code value for the object.|
|void|notify()|Wakes up a single thread that is waiting on this object's monitor.|
|void|notifyAll()|Wakes up all threads that are waiting on this object's monitor.|
|String	|toString()|Returns a string representation of the object.|
|void|wait()|Causes the current thread to wait until another thread invokes the notify() method or the notifyAll() method for this object.|
|void|wait(long timeout)|Causes the current thread to wait until either another thread invokes the notify() method or the notifyAll() method for this object, or a specified amount of time has elapsed.|
|void|wait(long timeout, int nanos)|Causes the current thread to wait until another thread invokes the notify() method or the notifyAll() method for this object, or some other thread interrupts the current thread, or a certain amount of real time has elapsed.|

在这里，我把这些方法贴出来，仅供参考。其实你不必要去背这些方法，当你需要使用该方法的时候，直接查看Java文档的API说明就可以了。

###  equals()和hashCode()的关系：

当你读到这里，一定已经对equals方法多少有所了解。回想一下上面提到的equals方法，你会发现。当你的类重写equals方法时，同时也需要去重写hashCode方法。`详细的原因，请参考hashMap的实现源码。`我简单的介绍下原因：在实现存储的过程中，JVM是将你的实例通过hashCode方法计算出该实例的哈希码，然后该哈希码作为存储你实例对象的地址值。所以，重写了equals也需要重写hashCode方法，来判定对象是否相同。

介绍完了hashCode方法，相信你大概能明白，equals方法在判断两个实例是否相同的依据，就是hashCode方法提供的哈希码。所以，当equals方法判定相等的两个实例对象，hashCode()一定是相同的。反之，**你需要注意**，equals方法判定不相等的两个实例对象，却不能判定hashCode()是不相等。这里的结论，可能对于你来说有点疑惑。但是，当你去了解了哈希码的生成算法后，你应该能明白。这里会出现这样状况的原因之一是，哈希码可能会出现冲突，换言之，哈希码相对于实例变量来说并不是唯一的，不同的实例对象可能会有相同的哈希码。还有一种原因，你应该更容易接受，就是在你重写了equals方法后，实际上比较的是两个实例对象的内容，那么此时两个不同的实例对象可能有相同的内容。

### String, StringBuffer和StringBuilder的区别：

相信你已经读过我之前的文章。你应该能自己动手找到解决该问题的方法。首先是阅读[Java8的API文档](http://docs.oracle.com/javase/8/docs/api/)，然后是去阅读相关类的源码。

在这里，这三个类的主要区别在于性能。

String是字符串常量，每次修改String的内容时，实际上是重新创建了一个实例对象，并且把修改过后的内容赋值给新创建的实例对象。

StringBuilder和StringBuffer都是字符串变量，区别在于StringBuilder不是线程安全的，StringBuffer是线程安全的。所以创建字符串实例时，执行速度快慢依次是StringBuilder>StringBuffer>String。

**你需要注意**，如果是`String str = "A" + "B" + "C";`，则String方式创建实例和StringBuilder方式是一样快的，原因是JVM在编译时对String方式进行了优化，也是通过StringBuilder的方法进行创建实例对象。

### Override和Overload的含义区别：

Override是重写，Overload是重载。这是比较容易混淆的，我建议你先记清楚含义，然后区别就比较明显了。

Override通常存在于继承关系中，指的是子类对父类方法的重写。重写要求函数签名（包括函数名称，参数列表和返回值）是和被重写方法一致的。

Overload通常存在于类的多态性，重载要求相同的方法名，不同的参数列表。**请注意**，不能通过访问权限，返回值类型以及抛出的异常进行重载。

### 抽象类和接口的区别：

抽象类是子类的通用特性，不能被实例化，只能用作子类的超类。接口是抽象方法的集合。如果一个类实现了某个接口，就必须实现这些方法。具体的请你参见下表内容：

|参数|抽象类|接口|
|--|--|--|
|默认的方法实现|它可以有默认的方法实现|接口完全是抽象的。它根本不存在方法的实现|
|实现|子类使用extends关键字来继承抽象类。如果子类不是抽象类的话，它需要提供抽象类中所有声明的方法的实现。|子类使用关键字implements来实现接口。它需要提供接口中所有声明的方法的实现|
|构造器|抽象类可以有构造器|接口不能有构造器|
|访问修饰符|抽象方法可以有public、protected和default这些修饰符|接口方法默认修饰符是public。你不可以使用其它修饰符。|
|多继承|抽象方法可以继承一个类和实现多个接口|接口只可以继承一个或多个其它接口|
|速度|它比接口速度要快|接口是稍微有点慢的，因为它需要时间去寻找在类中实现的方法。|

###  解析XML的几种方式的原理与特点：DOM、SAX、PULL

DOM：为 XML 文档的已解析版本定义了一组接口。解析器读入整个文档，然后构建一个驻留内存的树结构，然后代码就可以使用 DOM 接口来操作这个树结构。优点：整个文档树在内存中，便于操作；支持删除、修改、重新排列等多种功能；缺点：将整个文档调入内存（包括无用的节点），浪费时间和空间；使用场合：一旦解析了文档还需多次访问这些数据；硬件资源充足（内存、CPU）。 

SAX：为解决DOM的问题，出现了SAX。SAX ，事件驱动。当解析器发现元素开始、元素结束、文本、文档的开始或结束等时，发送事件，程序员编写响应这些事件的代码，保存数据。优点：不用事先调入整个文档，占用资源少；SAX解析器代码比DOM解析器代码小，适于Applet，下载。缺点：不是持久的；事件过后，若没保存数据，那么数据就丢了；无状态性；从事件中只能得到文本，但不知该文本属于哪个元素；使用场合：Applet;只需XML文档的少量内容，很少回头访问；机器内存少；

PULL：Pull是Android内置的xml解析器。Pull解析器的运行方式与SAX 解析器相似。它提供了类似的事件，如：开始元素和结束元素事件，使用parser.next()可以进入下一个元素并触发相应事件。事件将作为数值代码被发送，因此可以使用一个switch对感兴趣的事件进行处理。当元素开始解析时，调用parser.nextText()方法可以获取下一个Text类型节点的值。

### wait()和sleep()的区别：

wait()是Object类中的方法，sleep()是Thread类中的方法。

它们的主要区别在于对象锁。每个线程对象都是有一个锁来控制同步访问。区别在于，当前线程睡眠时，sleep()方法没有释放锁，wait()方法释放了锁。

sleep()使当前线程进入停滞状态(阻塞当前线程)，让出CPU资源给其他线程，当前线程休眠，但是锁没有释放，其他线程还是无法访问这个对象。线程休眠期满了之后，重新抢占CPU时间片。

wait()方法使得当前线程进入线程等待池，失去对象锁，其他线程可以访问。wait()必须放在同步块中，否则会抛异常。wait()使用notify或者notifyAll或者指定睡眠时间来唤醒当前等待池中的线程。

### JAVA多态的实现原理

多态是指不同类的对象能对同一消息作出响应。同一消息能对不同的对象采取不同的响应方式。

实现多态的技术称为，动态绑定技术。是指程序在执行期间，判断出所引用对象的实际类型，根据实际类型调用相应的方法。具体的可能需要你去学习JVM的相关知识。

### Java的垃圾回收和内存分配策略

垃圾回收是释放不在持有引用的对象所占的内存。

垃圾回收的几种算法：

引用计数：每个对象计算指向它的引用次数，当次数为0时，则可以回收该对象的内存空间。这是最容易理解的一种方式，但是缺陷也很明显，无法解决循环引用问题。也就是说，两个对象互相持有对方的引用，则这两个对象永远无法释放内存。

标记-清除：为了解决循环引用问题。垃圾回收器采用了根集合的概念。从根集合开始扫描，识别出哪些对象可达，哪些对象不可达。垃圾回收器回收不可达对象的内存空间。这种方式，解决了循环引用问题，但同时也带来了新的问题。你可能已经猜到，内存的碎片化问题。

分代回收：为了解决内存的碎片化问题。垃圾回收器将堆分成不同的代。每次在一个代上回收不可达对象后，将存活对象整理到另一个代上。

### Java的四种引用的区别

强引用：如果一个对象具有强引用，它就不会被垃圾回收器回收。即使当前内存空间不足，JVM 也不会回收它，而
是抛出 OutOfMemoryError 错误，使程序异常终止。如果想中断强引用和某个对象之间的关联，可以显式地将引用赋值为null，这样一来的话，JVM在合适的时间就会回收该对象。

软引用：在使用软引用时，如果内存的空间足够，软引用就能继续被使用，而不会被垃圾回收器回收，只有在内存不足时，软引用才会被垃圾回收器回收。

弱引用：具有弱引用的对象拥有的生命周期更短暂。因为当 JVM 进行垃圾回收，一旦发现弱引用对象，无论当前内存空间是否充足，都会将弱引用回收。不过由于垃圾回收器是一个优先级较低的线程，所以并不一定能迅速发现弱引用对象。

虚引用：顾名思义，就是形同虚设，如果一个对象仅持有虚引用，那么它相当于没有引用，在任何时候都可能被垃圾回收器回收。

### 什么是线程池，线程池的作用是什么

线程池是一个线程的集合。根据应用程序的需求和可用内存数量，开辟一段内存存放一定数量的线程。池中线程执行调度由池管理器来处理。当有线程任务时，从池中取一个，执行完成后线程对象归池，这样可以避免反复创建线程对象所带来的性能开销，节省了系统的资源。

Java提供的线程池的作用：
1. 重用存在的线程，减少对象创建、消亡的开销，性能佳。
2. 可有效控制最大并发线程数，提高系统资源的使用率，同时避免过多资源竞争，避免堵塞。
3. 提供定时执行、定期执行、单线程、并发数控制等功能。