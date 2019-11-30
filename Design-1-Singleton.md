---
title: 设计模式(一)单例模式
date: 2019-9-12 17:27:31
categories: 
    Design
tags:
    Design-Singleton
cover: http://r.photo.store.qq.com/psb?/V13Zm3q236IRIM/TMd.YqN1SoVpdRJeSYuSM04SbVKS9fW.NVFtlkBPvGI!/r/dLYAAAAAAAAA
mp3: https://api.uomg.com/api/rand.music

---

# 设计模式六大原则

**1、开闭原则（Open Close Principle）**

开闭原则的意思是：**对扩展开放，对修改关闭**。**在程序需要进行拓展的时候，不能去修改原有的代码**，实现一个热插拔的效果。简言之，是为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用接口和抽象类，后面的具体设计中我们会提到这点。

**2、里氏代换原则（Liskov Substitution Principle）**

里氏代换原则是面向对象设计的基本原则之一。 里氏代换原则中说，任何基类可以出现的地方，子类一定可以出现。LSP 是继承复用的基石，只有当派生类可以替换掉基类，且软件单位的功能不受到影响时，基类才能真正被复用，而派生类也能够在基类的基础上增加新的行为。里氏代换原则是对开闭原则的补充。实现开闭原则的关键步骤就是抽象化，而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。

**3、依赖倒转原则（Dependence Inversion Principle）**

这个原则是开闭原则的基础，具体内容：针对接口编程，依赖于抽象而不依赖于具体。

**4、接口隔离原则（Interface Segregation Principle）**

这个原则的意思是：使用多个隔离的接口，比使用单个接口要好。它还有另外一个意思是：降低类之间的耦合度。由此可见，其实设计模式就是从大型软件架构出发、便于升级和维护的软件设计思想，它强调降低依赖，降低耦合。

**5、迪米特法则，又称最少知道原则（Demeter Principle）**

最少知道原则是指：一个实体应当尽量少地与其他实体之间发生相互作用，使得系统功能模块相对独立。

**6、合成复用原则（Composite Reuse Principle）**

合成复用原则是指：尽量使用合成/聚合的方式，而不是使用继承。

# 一、创建型

## 1.单例模式（Singleton）

### 1.1 介绍

**意图：** 保证一个类仅有一个实例，并提供一个访问它的全局访问点。

**主要解决：** 一个全局使用的类频繁地创建与销毁。

**何时使用：** 当想控制实例数目，节省系统资源的时候。

**如何解决：** 判断系统是否已经有这个单例，如果有则返回，如果没有则创建。

**关键代码：** 构造函数是私有的。

**应用实例：**

1、Windows 是多进程多线程的，在操作一个文件的时候，就不可避免地出现多个进程或线程同时操作一个文件的现象，所以所有文件的处理必须通过唯一的实例来进行。 

2、一些设备管理器常常设计为单例模式，比如一个电脑有两台打印机，在输出的时候就要处理不能两台打印机打印同一个文件。

**优点：** 

1、在内存里只有一个实例，减少了内存的开销，尤其是频繁的创建和销毁实例（比如管理学院首页页面缓存）。 

2、避免对资源的多重占用（比如写文件操作）。

**缺点：** **没有接口，不能继承，与单一职责原则冲突，一个类应该只关心内部逻辑，而不关心外面怎么样来实例化。**

**使用场景：** 

1、要求生产唯一序列号。 

2、WEB 中的计数器，不用每次刷新都在数据库里加一次，用单例先缓存起来。

3、创建的一个对象需要消耗的资源过多，比如 I/O 与数据库的连接等，**数据库连接池**。

**注意事项：**getSingletonInstance() 方法中需要使用同步锁 synchronized (Singleton.class) 防止多线程同时进入造成 instance 被多次实例化。

### 1.2 实现方式

使用一个私有构造函数、一个私有静态变量以及一个公有静态函数来实现。

私有构造函数保证了不能通过构造函数来创建对象实例，只能通过公有静态函数返回唯一的私有静态变量。

**懒汉式-线程不安全**

以下实现中，私有静态变量 singletonInstance 被延迟实例化（把对象的创建延迟到使用的时候创建，而不是对象实例化的时候创建 ），这样做的好处是，如果没有用到该类，那么就不会实例化 singletonInstance，从而节约资源。

这个实现在多线程环境下是不安全的，如果多个线程能够同时进入 `if (singletonInstance == null)` ，并且此时 singletonInstance 为 null，那么会有多个线程执行 `singletonInstance = new Singleton();` 语句，这将导致实例化多次 singletonInstance。

```java
package com.singleton.demo01;

/**
 * @Auther: Jibny Zhan
 * @Date: 2019/9/12 15:59
 * @Description:懒汉式-线程不安全
 */
public class Singleton {

    private static int count;
    private static Singleton singletonInstance;

    private Singleton() {
        System.out.println("Singleton 私有的构造方法被实例化 " + (++count) + " 次。");
    }

    public static Singleton getSingletonInstance() {
        if (singletonInstance == null) {
            singletonInstance = new Singleton();
        }
        return singletonInstance;
    }
}

```

**饿汉式-线程安全**

线程不安全问题主要是由于 singletonInstance 被实例化多次，采取直接实例化 singletonInstance 的方式就不会产生线程不安全问题。但是直接实例化的方式也丢失了延迟实例化带来的节约资源的好处。

```java
package com.singleton.demo02;

/**
 * @Auther: Jibny Zhan
 * @Date: 2019/9/12 16:44
 * @Description:饿汉式-线程安全
 */
public class Singleton {
    private static int count;
    private static Singleton singletonIntance = new Singleton();

    private Singleton() {
        System.out.println("Singleton 私有的构造方法被实例化 " + (++count) + " 次。");
    }

    public static Singleton getSingletonIntance() {
        return singletonIntance;
    }
}

```

**懒汉式-线程安全**

只需要对 getSingletonInstance() 方法加锁，那么在一个时间点只能有一个线程能够进入该方法，从而避免了实例化多次 singletonInstance。但是当一个线程进入该方法之后，其它试图进入该方法的线程都必须等待，即使 singletonInstance 已经被实例化了。这会让线程阻塞时间过长，因此该方法有性能问题，不推荐使用。

```java
package com.singleton.demo03;

/**
 * @Auther: Jibny Zhan
 * @Date: 2019/9/12 16:53
 * @Description: 懒汉式-线程安全-同步锁阻塞
 */
public class Singleton {
    private static int count;
    private static Singleton singletonInstance;

    private Singleton() {
        System.out.println("Singleton 私有的构造方法被实例化 " + (++count) + " 次。");
    }

    public static synchronized Singleton getSingletonInstance() {
        if (singletonInstance == null) {
            singletonInstance = new Singleton();
        }
        return singletonInstance;
    }
}

```

**双重校验锁-线程安全**

singletonInstance 只需要被实例化一次，之后就可以直接使用了。加锁操作只需要对实例化那部分的代码进行，只有当 singletonInstance 没有被实例化时，才需要进行加锁。双重校验锁先判断 singletonInstance 是否已经被实例化，如果没有被实例化，那么才对实例化语句进行加锁。

```java
package com.singleton.demo04;

/**
 * @Auther: Jibny Zhan
 * @Date: 2019/9/12 17:03
 * @Description: 双重校验锁-线程安全
 */
public class Singleton {
    private static int count;
    private static volatile Singleton singletonInstance;

    private Singleton(){
        System.out.println("Singleton 私有的构造方法被实例化 " + (++count) + " 次。");
    }

    public static Singleton getSingletonInstance(){
        if(singletonInstance == null){
            synchronized (Singleton.class){
                if(singletonInstance == null){
                    singletonInstance = new Singleton();
                }
            }
        }
        return singletonInstance;
    }
}

```

如果上述代码中只使用外部一个if语句话，那么就有可能两个线程都进入到if语句内部，这样的话singletonInstance就会被实例化两次了，因此必须使用双重校验锁。

> ==singletonInstance 采用 volatile 关键字修饰也是很有必要的， `singletonInstance = new Singleton();` 这段代码其实是分为三步执行：==
>
> 1. ==为 singletonInstance 分配内存空间==
> 2. ==初始化 singletonInstance==
> 3. ==将 singletonInstance 指向分配的内存地址==
>
> ==但是由于 JVM 具有指令重排的特性，执行顺序有可能变成 1>3>2。指令重排在单线程环境下不会出现问题，**但是在多线程环境下会导致一个线程获得还没有初始化的实例**。例如，线程 T1 执行了 1 和 3，此时 T2 调用 getSingletonInstance() 后发现 singletonInstance 不为空，因此返回 singletonInstance，但此时 singletonInstance 还未被初始化。==
>
> ==使用 volatile 可以禁止 JVM 的指令重排，保证在多线程环境下也能正常运行。==

**静态内部类实现**

当 Singleton 类加载时，**静态内部类 SingletonHolder 没有被加载进内存**。只有当调用 `getSingletonInstance()` 方法从而触发 `SingletonHolder.singletonInstance` 时 SingletonHolder 才会被加载，此时初始化singletonInstance 实例，并且 JVM 能确保 singletonInstance 只被实例化一次。

这种方式不仅具有延迟初始化的好处，而且由 JVM 提供了对线程安全的支持。

```java
package com.singleton.demo05;

/**
 * @Auther: Jibny Zhan
 * @Date: 2019/9/12 17:10
 * @Description:静态内部类实现(推荐)
 */
public class Singleton {
    private static int count;

    private Singleton() {
        System.out.println("Singleton 私有的构造方法被实例化 " + (++count) + " 次。");
    }

    private static class SingletonHolder {
        private static final Singleton singletonInstance = new Singleton();
    }

    public static Singleton getSingletonInstance() {
        return SingletonHolder.singletonInstance;
    }
}

```

**测试单例实现**

```Java
package com.singleton.test;

import com.singleton.demo05.Singleton;

/**
 * @Auther: Jibny Zhan
 * @Date: 2019/9/12 16:57
 * @Description:
 */
public class Main {
    public static void main(String[] args) {
//        Singleton singleton1 = Singleton.getSingletonInstance();
//        Singleton singleton2 = Singleton.getSingletonInstance();
//        System.out.println(singleton1 == singleton1);
//        System.out.println(singleton1);
//        System.out.println(singleton2);
//        true

//        线程测试,不安全
//        线程 1 运行到 （1）处的时候,线程 2 抢到的 CPU 的执行权，进入 getInstance() 方法，
//        运行了 instance = new Singleton();，但线程 2 创建了对象这件事情，线程 1 根本不知道，
//        等到线程 1 重新获得 CPU 执行权的时候，从 （1） 处继续执行，又运行了 instance = new Singleton();
//        这行代码，这样，多余的对象就被创建出来了

        Runnable task = () -> {
            String threadName = Thread.currentThread().getName();
            Singleton s1 = Singleton.getSingletonInstance();
            System.out.println("线程 " + threadName + "\t => " + s1.hashCode());
        };
        for (int i = 0; i < 100; i++) {
            new Thread(task, "" + i).start();
        }
//        Singleton 私有的构造方法被实例化 1 次。
//        Singleton 私有的构造方法被实例化 3 次。
//        Singleton 私有的构造方法被实例化 1 次。
//        Singleton 私有的构造方法被实例化 2 次。
//        线程 2	 => 1133046463
//        线程 3	 => 503674368
//        线程 0	 => 2115147268
//        线程 1	 => 151286434
//        线程 4	 => 151286434 ......
    }
}

```
}

### 1.3 JDK

- [java.lang.Runtime#getRuntime()](http://docs.oracle.com/javase/8/docs/api/java/lang/Runtime.html#getRuntime%28%29)
- [java.awt.Desktop#getDesktop()](http://docs.oracle.com/javase/8/docs/api/java/awt/Desktop.html#getDesktop--)
- [java.lang.System#getSecurityManager()](http://docs.oracle.com/javase/8/docs/api/java/lang/System.html#getSecurityManager--)

### 1.4 破坏单例模式

**1、反射**

通过反射获得单例类的构造函数，由于该构造函数是private的，通过setAccessible(true)指示反射的对象在使用时应该取消 Java 语言访问检查,使得私有的构造函数能够被访问，这样使得单例模式失效。

**如果要抵御这种攻击，要防止构造函数被成功调用两次。需要在构造函数中对实例化次数进行统计，大于一次就抛出异常。**

**2、序列化**

一是可以实现数据的持久化；二是可以对象数据的远程传输。 如果过该类implements Serializable，那么就会在反序列化的过程中再创一个对象。这个问题的解决办法就是在反序列化时，指定反序化的对象实例。添加如下方法：

```java
 private static final long serialVersionUID = -3706817479790597301L;
 
    private volatile static Singleton singleton;
 
    private Object readResolve() {
        return singleton;
    }

```

**3、克隆**

由克隆我们可以想到原型模式，原型模式就是通过clone方法实现对象的创建的，clone方式是Object方法，每个对象都有，那我使用一个单例模式类的对象，调用clone方法，再创建一个新的对象了，那岂不是上面说的单例模式失效了。

当然答案是否定，某一个对象直接调用clone方法，会抛出异常，即并不能成功克隆一个对象。调用该方法时，必须实现一个Cloneable 接口。这也就是原型模式的实现方式。还有即如果该类实现了Cloneable接口，尽管构造函数是私有的，他也可以创建一个对象。

即clone方法是不会调用构造函数的，他是直接从内存中copy内存区域的。

**所以单例模式的类是不可以实现cloneable接口的。**