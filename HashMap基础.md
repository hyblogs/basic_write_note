## HashMap基础

<!--目录结构-->
[toc]

### 1.前提
>本系列基于jdk1.8主要介绍HashMap的概念以及源码分析，会对比常见集合与HashMap之间的区别,以及面试遇到的问题进行说明。

### 2.HashMap简介
>　　在Java编程语言中，最基本的结构就是两种，一个是数组，另外一个是模拟指针（引用），所有的数据结构都可以用这两个基本结构来构造的，HashMap也不例外。HashMap实际上是一个“链表散列”的数据结构，即数组和链表的结合体。

>　　HashMap 是一个散列表，它存储的内容是键值对(key-value)映射。<br>
HashMap 继承于AbstractMap，实现了Map,Cloneable,java.io.Serializable接口。
HashMap的实现不是同步的，这意味着它不是线程安全的。它的key、value都可以为null。此外，HashMap中的映射不是有序的。
HashMap有两个参数影响其性能：初始容量和加载因子。默认初始容量是16，加载因子是0.75。容量是哈希表中桶(Entry数组)的数量，
初始容量只是哈希表在创建时的容量。加载因子是哈希表在其容量自动增加之前可以达到多满的一种尺度。
当哈希表中的条目数超出了加载因子与当前容量的乘积时，通过调用 rehash 方法将容量翻倍。

### 3.Hash实现原理
>在介绍hashMap源码之前先讲几个基本概念以及Object类的两个方法hashCode和equals

####3.1 Java中 == 号与 equals() 方法的区别
> == 号和 equals() 方法都是比较是否相等的方法，那它们有什么区别和联系呢？ <br>
首先，== 号在比较基本数据类型时比较的是值，而用 == 号比较两个对象时比较的是两个对象的地址值。<br>
示例：

    package hy.example;

    public class Test {
        public static void main(String[] args) {
            int x = 10;
            int y = 10;
            String str1 = new String("hello");
            String str2 = new String("hello");
            System.out.println(x == y); // 输出true
            System.out.println(str1 == str2); // 输出false
    
    
        }
    }
>在比较基本类型的值的时候也会引申一个自动装箱和拆箱的问题，比如下面的例子:

    package hy.example;

    public class Test {
        public static void main(String[] args) {
            int x = 10;
            int y = 10;
            String str1 = new String("hello");
            String str2 = new String("hello");
            System.out.println(x == y); // 输出true
            System.out.println(str1 == str2); // 输出false
    
            Integer a = 1444;
            int b = 1444;
            Integer x1 = 10;
            Integer y1 = 10;
            Integer x2 = 1444;
            Integer y2 = 1444;
            System.out.println(a == b); // 输出true
            System.out.println(x1 == y1); // 输出true
            System.out.println(x2 == y2); // 输出false
        }
    }

>我们可以通过查看源码知道，equals()方法存在于Object类中，因为Object类是所有类的直接或间接父类，
也就是说所有的类中的equals()方法都继承自Object类，而通过源码我们发现，Object类中equals()方法底层依赖的是 == 号；
那么，在所有没有重写equals()方法的类中，调用equals()方法其实和使用 == 号的效果一样，也是比较的地址值，
然而，Java提供的所有类中，绝大多数类都重写了equals()方法，重写后的equals()方法一般都是比较两个对象的值。
下面看一下String类中重写了equals方法源码：

    public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    // 逐个判断字符是否相等 
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }

>比如下面的实例：

    package hy.example;

    public class Test {
        public static void main(String[] args) {
            String str1 = new String("abc");
            String str2 = new String("abc");
            System.out.println(str1.equals(str2));// 输出true
            System.out.println(str1 == str2);// 输出false
    
        }
    }

>这里又引申一个问题，java 常量池问题，具体介绍详细看java的自动装箱和拆箱这篇文章

    package hy.example;

    public class Test {
        public static void main(String[] args) {
            String str1 ="abc";
            String str2 ="abc";
            System.out.println(str1.equals(str2));// 输出true
            System.out.println(str1 == str2);// 输出true
    
        }
    }

>综上所叙，如果想让两个对象相等，需要重写equals方法。

#### 3.2 hashCode方法
>　　hashCode方法，这个方法我们平时通常是用不到的，它是为哈希家族的集合类框架(HashMap、HashSet、HashTable)提供服务，hashCode 的常规协定是： <br>
>　　在 Java 应用程序执行期间，在同一对象上多次调用 hashCode 方法时，必须一致地返回相同的整数，前提是对象上 equals 比较中所用的信息没有被修改。
从某一应用程序的一次执行到同一应用程序的另一次执行，该整数无需保持一致。 <br>
如果根据 equals(Object) 方法，两个对象是相等的，那么在两个对象中的每个对象上调用 hashCode 方法都必须生成相同的整数结果。 <br>

>以下情况不是必需的：如果根据 equals(java.lang.Object) 方法，两个对象不相等，那么在两个对象中的任一对象上调用 hashCode 方法必定会生成不同的整数结果。
但是，程序员应该知道，为不相等的对象生成不同整数结果可以提高哈希表的性能。 
当我们看到实现这两个方法有这么多要求时，立刻凌乱了，幸好有IDE来帮助我们，Eclipse中可以通过快捷键alt+shift+s调出快捷菜单，
选择Generate hashCode() and equals()，根据业务需求，勾选需要生成的属性，确定之后，这两个方法就生成好了，我们通常需要在JavaBean对象中重写这两个方法。 
实例：当我比较两个对象时，如果只是比对某几个属性，可重新生成equals和hashcode方法，比如：

    package hy.example;

    public class Model {
        public Integer id;
        public String name;
        public String code;
    
        public String getCode() {
            return code;
        }
    
        public void setCode(String code) {
            this.code = code;
        }
    
        public Integer getId() {
            return id;
        }
    
        public void setId(Integer id) {
            this.id = id;
        }
    
        public String getName() {
            return name;
        }
    
        public void setName(String name) {
            this.name = name;
        }
    
        /**
         * 重写equals方法
         */
        @Override
        public boolean equals(Object o) {
            if (this == o) return true;
            if (o == null || getClass() != o.getClass()) return false;
    
            Model model = (Model) o;
            //若两个对象ID不相等则返回false表明两个对象不等
            if (!id.equals(model.id)) return false;
            //若两个对象ID相等则判断name属性是否相等，相等则返回true，不等则返回false
            return name.equals(model.name);
        }
    
        /**
         * 重写hashCode方法
         */
        @Override
        public int hashCode() {
            int result = id.hashCode();
            result = 31 * result + name.hashCode();
            return result;
        }
    }
    
   >上面例子说明即使属性code不一样，而id和name一样，也一样认为两个对象相等。
   
##### 3.2.1 在改写equals方法的时候，需要满足以下三点： 
>　(1)	自反性：就是说a.equals(a)必须为true。 <br>
>　(2)	对称性：就是说a.equals(b)=true的话，b.equals(a)也必须为true。 <br>
>　(3)	传递性：就是说a.equals(b)=true，并且b.equals(c)=true的话，a.equals(c)也必须为true。 <br>
>通过改写key对象的equals和hashcode方法，我们可以将任意的业务对象作为map的key(前提是你确实有这样的需要)。 
   
#### 3.3 HashMap中定义的成员变量解读
    /**
     * The default initial capacity - MUST be a power of two.
     *
     * 默认初始化容量：1 * 2 ^ 4 => 2的四次方 = 16，必须为2的幂
     */
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16

    /**
     * The maximum capacity, used if a higher value is implicitly specified
     * by either of the constructors with arguments.
     * MUST be a power of two <= 1<<30.
     *
     * 最大容量：1 * 2 ^ 30 => 2的30次方 = 1 073 741 824
     */
    static final int MAXIMUM_CAPACITY = 1 << 30;

    /**
     * The load factor used when none specified in constructor.
     *
     * 默认加载因子0.75
     * 表示Hash表中元素的填满的程度.若:加载因子越大,填满的元素越多,好处是,空间利用率高了,但:冲突的机会加大了.
     * 反之,加载因子越小,填满的元素越少,好处是:冲突的机会减小了,但:空间浪费多了.
     * 冲突的机会越大,则查找的成本越高.反之,查找的成本越小.因而,查找时间就越小. 
     */
    static final float DEFAULT_LOAD_FACTOR = 0.75f;

    /**
     * The bin count threshold for using a tree rather than list for a
     * bin.  Bins are converted to trees when adding an element to a
     * bin with at least this many nodes. The value must be greater
     * than 2 and should be at least 8 to mesh with assumptions in
     * tree removal about conversion back to plain bins upon
     * shrinkage.
     *
     * 由链表转换成树的阈值TREEIFY_THRESHOLD
     * 一个桶中bin（箱子）的存储方式由链表转换成树的阈值。即当桶中bin的数量超过TREEIFY_THRESHOLD时使用树来代替链表。默认值是8 
     */
    static final int TREEIFY_THRESHOLD = 8;

    /**
     * The bin count threshold for untreeifying a (split) bin during a
     * resize operation. Should be less than TREEIFY_THRESHOLD, and at
     * most 6 to mesh with shrinkage detection under removal.
     *
     * 由树转换成链表的阈值UNTREEIFY_THRESHOLD
     * 当执行resize操作时，当桶中bin的数量少于UNTREEIFY_THRESHOLD时使用链表来代替树。默认值是6 
     */
    static final int UNTREEIFY_THRESHOLD = 6;

    /**
     * The smallest table capacity for which bins may be treeified.
     * (Otherwise the table is resized if too many nodes in a bin.)
     * Should be at least 4 * TREEIFY_THRESHOLD to avoid conflicts
     * between resizing and treeification thresholds.
     *
     * 当桶中的bin被树化时最小的hash表容量。（如果没有达到这个阈值，即hash表容量小于MIN_TREEIFY_CAPACITY，
     * 当桶中bin的数量太多时会执行resize扩容操作）这个MIN_TREEIFY_CAPACITY的值至少是TREEIFY_THRESHOLD的4倍。
     */
    static final int MIN_TREEIFY_CAPACITY = 64;
    
    /**
     * The number of key-value mappings contained in this map.
     *
     * 当前HashMap实际储存Key-Value键值对个数
     * 有关Transient修饰符，请看 Transient.md 了解详情
     */
    transient int size;
    
    /**
     * The number of times this HashMap has been structurally modified
     * Structural modifications are those that change the number of mappings in
     * the HashMap or otherwise modify its internal structure (e.g.,
     * rehash).  This field is used to make iterators on Collection-views of
     * the HashMap fail-fast.  (See ConcurrentModificationException).
     *
     * 修改次数
     */
    transient int modCount;
    
#### 3.3.1 DEFAULT_LOAD_FACTOR-默认负载因子

>用来衡量HashMap满的程度。loadFactor的默认值为0.75f。<br>

>下面是HashMap的一个构造函数，两个参数initialCapacity,loadFactor <br>
>这关系HashMap的迭代性能。<br>

    /**
     * Constructs an empty <tt>HashMap</tt> with the specified initial
     * capacity and load factor.
     *
     * @param  initialCapacity the initial capacity
     * @param  loadFactor      the load factor
     * @throws IllegalArgumentException if the initial capacity is negative
     *         or the load factor is nonpositive
     */
    public HashMap(int initialCapacity, float loadFactor) {
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " +
                                               loadFactor);
        this.loadFactor = loadFactor;
        this.threshold = tableSizeFor(initialCapacity);
    }

>关于这两个参数值的设定界限：<br>
>　1.initialCapacity是map的初始化容量，initialCapacity > MAXIMUM_CAPACITY，表明map的最大容量是1<<30,也就是1左移30位，每左移一位乘以2，所以就是1*2^30=1073741824。<br>
>　2.loadFactor是map的负载因子,loadFactor <= 0 || Float.isNaN(loadFactor),表明负载因子要大于0，且是非无穷大的数字。

##### 负载因子为什么会影响HashMap性能

>首先回忆HashMap的数据结构，
我们都知道有序数组存储数据，对数据的索引效率都很高，但是插入和删除就会有性能瓶颈（回忆ArrayList）；
链表存储数据，要依次比较元素来检索出数据，所以索引效率低，但是插入和删除效率高（回忆LinkedList）；
两者取长补短就产生了哈希散列这种存储方式，也就是HashMap的存储逻辑.<br>
而负载因子表示一个散列表的空间的使用程度，有这样一个公式：initialCapacity*loadFactor=HashMap的容量 (HashMap初始容量 * HashMap负载因子 = HashMap的容量)。<br>
所以负载因子越大则散列表的装填程度越高，也就是能容纳更多的元素，元素多了，链表大了，所以此时索引效率就会降低。
反之，负载因子越小则链表中的数据量就越稀疏，此时会对空间造成浪费，但是此时索引效率高。


##### 如何科学设置 initialCapacity, loadFactor的值

>　　HashMap有三个构造函数，可以选用无参构造函数，不进行设置。默认值分别是initialCapacity = 16 和 loadFactor = 0.75. <br>
官方的建议是initialCapacity设置成2的n次幂，loadFactor根据业务需求，如果迭代性能不是很重要，可以设置大一些。

##### 为什么initialCapacity要设置成2的n次幂? <br>
>Hash算法:<br>
>　　我们可以看到在HashMap中要找到某个元素，需要根据key的hash值来求得对应数组中的位置。如何计算这个位置就是hash算法。
前面说过HashMap的数据结构是数组和链表的结合，所以我们当然希望这个HashMap里面的元素位置尽量的分布均匀些，
尽量使得每个位置上的元素数量只有一个，那么当我们用hash算法求得这个位置的时候，马上就可以知道对应位置的元素就是我们要的，
而不用再去遍历链表。 
所以我们首先想到的就是把hashcode对数组长度取模运算，这样一来，元素的分布相对来说是比较均匀的。但是，“模”运算的消耗还是比较大的，
能不能找一种更快速，消耗更小的方式那？java中时这样做的， 

>Java代码:

    /**
     * Returns index for hash code h.
     */
    static int indexFor(int h, int length) {  
       return h & (length - 1);  
    }  

>首先算得key得hashcode值，然后跟数组的长度-1(length -1) 做一次“与”运算（&）。看上去很简单，其实比较有玄机。
比如数组的长度是2的4次方，那么hashcode就会和2的4次方-1做“与”运算。
很多人都有这个疑问，为什么HashMap的数组初始化大小都是2的次方大小时，HashMap的效率最高。
我以2的4次方举例，来解释一下为什么数组大小为2的幂时HashMap访问的性能最高。 

>　　左边两组是数组长度为16（2的4次方），右边两组是数组长度为15。两组的hashcode均为8和9，但是很明显，当它们和1110“与”的时候，产生了相同的结果，也就是说它们会定
位到数组中的同一个位置上去，这就产生了碰撞，8和9会被放到同一个链表上，那么查询的时候就需要遍历这个链表，得到8或者9，这样就降低了查询的效率。同时，我们也可以
发现，当数组长度为15的时候，hashcode的值会与14（1110）进行“与”，那么最后一位永远是0，而0001，0011，0101，1001，1011，0111，1101这几个位置永远都不能
存放元素了，空间浪费相当大，更糟的是这种情况中，数组可以使用的位置比数组长度小了很多，这意味着进一步增加了碰撞的几率，减慢了查询的效率！
![picture](https://github.com/hyblogs/blogs/blob/master/Java_Images/HashMap/02.jpg)

>所以说，当数组长度为2的n次幂的时候，不同的key算得的元素在数组中的位置(下标:index)相同的几率较小，那么数据在数组上分布就比较均匀，也就是说碰撞的几率小(相对的)，查询的时候就不用
遍历某个位置上的链表，这样查询效率也就较高了。

##### resize()方法

>initialCapacity，loadFactor会影响到HashMap扩容。
HashMap每次put操作时都会检查一遍 size（当前容量）> initialCapacity * loadFactor 是否成立。如果成立则HashMap扩容为以前的两倍（数组扩成两倍），
然后重新计算每个元素在数组中的位置，然后再进行存储。这是一个十分消耗性能的操作。
所以如果能根据业务预估出HashMap的容量，应该在创建的时候指定初始容量(initialCapacity)，那么就可以避免 resize() 了.

##### 那么HashMap什么时候进行扩容呢？
>当HashMap中的元素个数超过数组大小 * loadFactor时，就会进行数组扩容，loadFactor的默认值为0.75，也就是说，默认情况下，数组大小为16，
那么当HashMap中元素个数超过 16 * 0.75 = 12 的时候，就把数组的大小扩展为: 2 * 16 = 32，即扩大一倍，然后重新计算每个元素在数组中的位置，
而这是一个非常消耗性能的操作，所以如果我们已经预知HashMap中元素的个数，那么预设元素的个数能够有效的提高HashMap的性能。
比如说，我们有1000个元素new HashMap(1000), 但是理论上来讲new HashMap(1024)更合适，不过上面已经说过，即使是1000，
HashMap也自动会将其设置为1024。 但是new HashMap(1024)还不是更合适的，因为0.75*1000 < 1000, 也就是说为了让0.75 * size > 1000, 
我们必须这样new HashMap(2048)才最合适，既考虑了&的问题，也避免了resize的问题。 

#### 3.3.2 modCount修改次数
>所有使用modCount属性的全是线程不安全的,只有在本数据结构对应迭代器中才使用,以HashMap为例：
    
    abstract class HashIterator {
        Node<K,V> next;        // next entry to return
        Node<K,V> current;     // current entry
        int expectedModCount;  // for fast-fail
        int index;             // current slot

        HashIterator() {
            expectedModCount = modCount;
            Node<K,V>[] t = table;
            current = next = null;
            index = 0;
            if (t != null && size > 0) { // advance to first entry
                do {} while (index < t.length && (next = t[index++]) == null);
            }
        }

        public final boolean hasNext() {
            return next != null;
        }

        final Node<K,V> nextNode() {
            Node<K,V>[] t;
            Node<K,V> e = next;
            if (modCount != expectedModCount)
                throw new ConcurrentModificationException();
            if (e == null)
                throw new NoSuchElementException();
            if ((next = (current = e).next) == null && (t = table) != null) {
                do {} while (index < t.length && (next = t[index++]) == null);
            }
            return e;
        }

        public final void remove() {
            Node<K,V> p = current;
            if (p == null)
                throw new IllegalStateException();
            if (modCount != expectedModCount)
                throw new ConcurrentModificationException();
            current = null;
            K key = p.key;
            removeNode(hash(key), key, null, false, false);
            expectedModCount = modCount;
        }
    }

>由以上代码可以看出，在一个迭代器初始的时候会赋予它调用这个迭代器的对象的 modCount，如何在迭代器遍历的过程中，一旦发现这个对象的 modCount 和迭代器中存储的 modCount 不一样那就抛异常。<br>
好的，下面是这个的完整解释:<br>
**Fail-Fast 机制** <br>
我们知道 java.util.HashMap 不是线程安全的，因此如果在使用迭代器的过程中若有其他线程修改了map，
那么将抛出ConcurrentModificationException，这就是所谓fail-fast策略。
这一策略在源码中的实现是通过 modCount 域，modCount 顾名思义就是修改次数，对HashMap 内容的修改都将增加这个值，
那么在迭代器初始化过程中会将这个值赋给迭代器的 expectedModCount。在迭代过程中，判断 modCount 跟 expectedModCount 是否相等，
如果不相等就表示已经有其他线程修改了Map。<br>

><font color=#FF0000 size=3>注: modCount 被声明为 volatile，即为了保证线程之间修改的可见性。</font><br>

><font color=#FF0000 size=3>所以在这里和大家建议，当大家遍历那些非线程安全的数据结构时，尽量使用迭代器</font>

### 4.HashMap解决Hash冲突的几种方法
#### 4.1 开放定址法
>Hi=(H(key) + di) MOD m i=1,2,...k(k<=m-1)其中H(key)为哈希函数；m为哈希表表长；di为增量序列。

##### 4.1.1 开放定址法根据步长不同可以分为３种：

>　1）线性探查法(Linear Probing)：di=1,2,3,...,m-1
　 简单地说就是以当前冲突位置为起点，步长为１循环查找，直到找到一个空的位置就把元素插进去，循环完了都找不到说明容器满了。就像你去一条街上的店里吃饭，问了第一家被告知满座，然后挨着一家家去问是否有位置一样。

>　2）线性补偿探测法：di=Ｑ　下一个位置满足 Hi=(H(key) + Ｑ) mod m i=1,2,...k(k<=m-1) ，要求 Q 与 m 是互质的，以便能探测到哈希表中的所有单元。
继续用上面的例子，现在你不是挨着一家家去问了，拿出计算器算了一下，然后隔Ｑ家问一次有没有位置。

>　3）伪随机探测再散列：di=伪随机数序列。还是那个例子，这是完全根据心情去选一家店来问了

>缺点：

>这种方法建立起来的hash表当冲突多的时候数据容易堆聚在一起，这时候对查找不友好；
删除结点不能简单地将被删结 点的空间置为空，否则将截断在它之后填人散列表的同义词结点的查找路径。因此在 用开放地址法处理冲突的散列表上执行删除操作，只能在被删结点上做删除标记，而不能真正删除结点
当空间满了，还要建立一个溢出表来存多出来的元素。

#### 4.2 再哈希法
>Hi = RHi（key），i=1,2,...k
RHi均是不同的哈希函数，即在同义词产生地址冲突时计算另一个哈希函数地址，直到不发生冲突为止。这种方法不易产生聚集，但是增加了计算时间。

>缺点：增加了计算时间。

#### 4.3 建立一个公共溢出区
>假设哈希函数的值域为[0,m-1]，则设向量HashTable[0...m-1]为基本表，每个分量存放一个记录，另设立向量OverTable[0....v]为溢出表。所有关键字和基本表中关键字为同义词的记录，不管他们由哈希函数得到的哈希地址是什么，一旦发生冲突，都填入溢出表。

>简单地说就是搞个新表存冲突的元素。

#### 4.4 链地址法（拉链法）
>将所有关键字为同义词的记录存储在同一线性链表中，也就是把冲突位置的元素构造成链表。

>拉链法的优点:

>拉链法处理冲突简单，且无堆积现象，即非同义词决不会发生冲突，因此平均查找长度较短；
由于拉链法中各链表上的结点空间是动态申请的，故它更适合于造表前无法确定表长的情况；
在用拉链法构造的散列表中，删除结点的操作易于实现。只要简单地删去链表上相应的结点即可。

>拉链法的缺点：

>指针需要额外的空间，故当结点规模较小时，开放定址法较为节省空间，而若将节省的指针空间用来扩大散列表的规模，可使装填因子变小，
这又减少了开放定址法中的冲突，从而提高平均查找速度

#### 4.5 解决冲突对应的数据结构示例图
>RE：HashMap实际上是一个“链表散列”的数据结构，即数组和链表的结合体。
![picture](https://github.com/hyblogs/blogs/blob/master/Java_Images/HashMap/01.png)
