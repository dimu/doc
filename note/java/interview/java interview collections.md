#java interview collections#

## java basic ##

**Java面向对象的特性**
java面向对象的三大特性：
继承：java是单继承，可以继承父类的变量，方法等，这样可以允许和鼓励类的重用。
封装：隐藏对象的属性与实现细节，仅对外提供公共的访问方式。将变化隔离，便于使用，提高重用性，提高安全性。
多态：由子类的引用来决定动态方法的调用。重写与重载是实现多态的必要条件，多态也是松耦合的必要条件。

**HashMap与HashTable的区别**
HashMap是线程非安全的，HashTable是线程安全的，在不要求线程安全的情况下优先使用HashMap，在要求线程安全的情况下也不推荐使用HashTable，优先使用jdk1.5引入的ConcurrentHashMap。

**java的抽象类与接口的区别**
抽象类与接口设计目标不同，抽象类是为了对对象进行抽象，而接口是对行为的约束。
抽象类可以有实现方法，可以有成员变量，可以有私有方法等，但是接口只能定义public的方法。不过java8允许接口实现默认方法，减少抽象类与接口之间的不同。

**Java io与nio区别**

**java进程通信方式与线程通信方式**

**java虚拟机内存模型**

**垃圾回收算法**
1、引用计数算法（Reference counting） ：对象有引用+1，删除引用-1，无法处理循环引用问题
2、复制（copying）：需要两倍的内存空间，不会产生碎片
3、标记-清除（Mark-sweep）：jdk早期处理方式，会产生大量碎片。
4、标记-整理（mark-compact）：标记与整理
5、分代（generational collection）：jdk1.2以后采用的算法，将对象按其生命周期不同分为年轻代（young generation），年老代（old generation），持久代（permanent generation）

**垃圾回收器有哪些**

**gc的运行方式**

**怎么优化设定新生代老生代等**