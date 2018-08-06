1.java的接口可以实现多个，抽象类只能继承一个，继承有传递性

2.线性结构：线性表，栈和队列，双队列，数组，串。

 非线性结构：二维数组，多维数组，树，图，广义表。

3.如果用个矩阵表示有向图的存储结构，入度是第i列非零元素的个数，出度是第i行非零元素的个数，（入列出行）

4.Float
 
* Float是类，float不是类.
* 查看JDK源码就可以发现Byte，Character，Short，Integer，Long，Float，Double，Boolean都在java.lang包中.
* Float正确复制方式是Float f=1.0f,若不加f会被识别成double型,double无法向float隐式转换.
* Float a= new Float(1.0)是正确的赋值方法，但是在1.5及以上版本引入自动装箱拆箱后，会提示这是不必要的装箱的警告，通常直接使用Float f=1.0f.

5.深度搜索类似于树的前序访问，广度搜索类似于树的从树根出发的按层次的遍历。

6.头结点的存在，使得空链表与非空链表的处理变得一致，也方便了对链表的开始节点插入或者删除操作。

7.顺序表适合存取，链表适合插入删除

8.java

* java,exe是java虚拟机
* javadoc.exe用来制作java文档
* jdb.exe是java的调试器
* javaprof,exe是剖析工具

9.关于HashMap的一些说法

* HashMap实际上是一个“链表散列”的数据结构，即数组和链表的结合体。HashMap的底层结构是一个数组，数组中的每一项是一条链表。 
* b)  HashMap的实例有俩个参数影响其性能： “初始容量” 和 装填因子。 
* c)  HashMap实现不同步，线程不安全。  HashTable线程安全 
* d)  HashMap中的key-value都是存储在Entry中的。 
* e)  HashMap可以存null键和null值，不保证元素的顺序恒久不变，它的底层使用的是数组和链表，通过hashCode()方法和equals方法保证键的唯一性 
* f)  解决冲突主要有三种方法：定址法，拉链法，再散列法。HashMap是采用拉链法解决哈希冲突的。 注： 链表法是将相同hash值的对象组成一个链表放在hash值对应的槽位；    
* 用开放定址法解决冲突的做法是：当冲突发生时，使用某种探查(亦称探测)技术在散列表中形成一个探查(测)序列。 沿此序列逐个单元地查找，直到找到给定 的关键字，或者碰到一个开放的地址(即该地址单元为空)为止（若要插入，在探查到开放的地址，则可将待插入的新结点存人该地址单元）。   
* 拉链法解决冲突的做法是： 将所有关键字为同义词的结点链接在同一个单链表中 。若选定的散列表长度为m，则可将散列表定义为一个由m个头指针组成的指针数 组T[0..m-1]。凡是散列地址为i的结点，均插入到以T[i]为头指针的单链表中。T中各分量的初值均应为空指针。在拉链法中，装填因子α可以大于1，但一般均取α≤1。拉链法适合未规定元素的大小。

10.Hashtable和HashMap的区别

* 继承不同。  public class Hashtable extends Dictionary implements Map public class HashMap extends  AbstractMap implements Map 
* b)  Hashtable中的方法是同步的，而HashMap中的方法在缺省情况下是非同步的。在多线程并发的环境下，可以直接使用Hashtable，但是要使用HashMap的话就要自己增加同步处理了。 
* c)  Hashtable 中， key 和 value 都不允许出现 null 值。 在 HashMap 中， null 可以作为键，这样的键只有一个；可以有一个或多个键所对应的值为 null 。当 get() 方法返回 null 值时，即可以表示 HashMap 中没有该键，也可以表示该键所对应的值为 null 。因此，在 HashMap 中不能由 get() 方法来判断 HashMap 中是否存在某个键， 而应该用 containsKey() 方法来判断。 
* d)  两个遍历方式的内部实现上不同。Hashtable、HashMap都使用了Iterator。而由于历史原因，Hashtable还使用了Enumeration的方式 。 
* e)  哈希值的使用不同，HashTable直接使用对象的hashCode。而HashMap重新计算hash值。 
* f)  Hashtable和HashMap它们两个内部实现方式的数组的初始大小和扩容的方式。HashTable中hash数组默认大小是11，增加的方式是old*2+1。HashMap中hash数组的默认大小是16，而且一定是2的指数。   注：  HashSet子类依靠hashCode()和equal()方法来区分重复元素。      HashSet内部使用Map保存数据，即将HashSet的数据作为Map的key值保存，这也是HashSet中元素不能重复的原因。而Map中保存key值的,会去判断当前Map中是否含有该Key对象，内部是先通过key的hashCode,确定有相同的hashCode之后，再通过equals方法判断是否相同。

11.优化Hibernate所鼓励的七大措施

* 尽量使用many-to-one,避免使用one-to-many。
* 灵活使用单向one-to-many
* 不用一对一，使用多对一代替一对一
* 配置对象缓存，不使用集合缓存
* 一对多使用Bag，多对一使用Set
* 继承使用显示多态HQL：from object polymorphism="exlicit" 避免查处所有对象
* 消除大表，使用二级缓存。

12.存储结构是数据的逻辑结构用计算机语言实现，常见的存储结构有：顺序存储，链式存储，索引存储，以及散列存储。其中散列所形成的存储结构叫散列表（哈希表），栈逻辑结构对应的顺序存储结构为顺序栈，对应的链式存储结构为链栈，循环队列是顺序存储结构，链表是线性表的链式存储结构。