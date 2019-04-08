# Java常见基础知识汇总
> 原文与出处：https://blog.csdn.net/u010697681/article/details/79414112、https://blog.csdn.net/IbelieveSmile/article/details/81334205

[toc]

## 基础篇

### 基本功

#### 面向对象特征

> 答：封装，继承，多态和抽象。 

##### 封装
> 封装给对象提供了隐藏内部特性和行为的能力。对象提供一些能被其他对象访问的方法来改变它内部的数据。在 Java 当中，有 4 种修饰符： public、private、protected和默认修饰符。每一种修饰符给其他的位于同一个包或者不同包下面对象赋予了不同的访问权限。  

> 下面列出了使用封装的一些好处：  
> 1.通过隐藏对象的属性来保护对象内部的状态。  
> 2.提高了代码的可用性和可维护性，因为对象的行为可以被单独的改变或者是扩展。  
> 3.禁止对象之间的不良交互提高模块化。  

##### 继承
> 继承给对象提供了从基类获取字段和方法的能力。继承提供了代码的重用性，也可以在不修改类的情况下给现存的类添加新特性。

##### 多态
> 多态是编程语言给不同的底层数据类型做相同的接口展示的一种能力。一个多态类型上的操作可以应用到其他类型的值上面。

##### 抽象
> 抽象是把想法从具体的实例中分离出来的步骤，因此，要根据他们的功能而不是实现细节来创建类。 Java 支持创建只暴漏接口而不包含方法实现的抽象的类。这种抽象技术的主要目的是把类的行为和实现细节分离开。

#### final, finally, finalize 的区别

##### final
> 修饰符（关键字）如果一个类被声明为final，意味着它不能再派生出新的子类，不能作为父类被继承。因此一个类不能既被声明为 abstract的，又被声明为final的。将变量或方法声明为final，可以保证它们在使用中不被改变。被声明为final的变量必须在声明时给定初值，而在以后的引用中只能读取，不可修改。被声明为final的方法也同样只能使用(<font color=pink>可以重载</font>)，不能<font color=blue>重写</font>。  

##### finally
> 在异常处理时提供 finally 块来执行任何清除操作。如果抛出一个异常，那么相匹配的 catch 子句就会执行，然后控制就会进入 finally 块（如果有的话）。  
> 注意：线程如果意外挂掉或者在try的时候exit了就不会再执行到finally了。

##### finalize
> 方法名。Java 技术允许使用 finalize() 方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在确定这个对象没有被引用时对这个对象调用的。它是在 Object 类中定义的，因此所有的类都继承了它。子类覆盖 finalize() 方法以整理系统资源或者执行其他清理工作。finalize() 方法是在垃圾收集器删除对象之前对这个对象调用的。

#### int 和 Integer 有什么区别

> int 是基本数据类型。 
> Integer是其包装类，注意是一个类。  
> **为什么要提供包装类呢？？？**  
> 是为了在各种类型间转化，通过各种方法的调用。否则 你无法直接通过变量转化。  
> 比如，现在int要转为String，如：

	int a=0;
	String result=Integer.toString(a);
	
> 在java中包装类，比较多的用途是用在于各种数据类型的转化中。  

	//通过包装类来实现转化的
	int num=Integer.valueOf("12");
	int num2=Integer.parseInt("12");
	double num3=Double.valueOf("12.2");
	double num4=Double.parseDouble("12.2");
	//其他的类似。通过基本数据类型的包装来的valueOf和parseXX来实现String转为XX
	String a=String.valueOf("1234");//这里括号中几乎可以是任何类型
	String b=String.valueOf(true);
	String c=new Integer(12).toString();//通过包装类的toString()也可以
	String d=new Double(2.3).toString();

> 再举例下。比如我现在要用泛型：   

	List<Integer> nums;
	
> 这里<>需要类。如果你用int。它会报错的。  

#### 重载和重写的区别

##### override（重写）

> 1. 方法名、参数、返回值相同。
2. 子类方法不能缩小父类方法的访问权限。
3. 子类方法不能抛出比父类方法更多的异常(但子类方法可以不抛出异常)。
4. 存在于父类和子类之间。
5. 方法被定义为final不能被重写。

##### overload（重载）

> 1. 参数类型、个数、顺序至少有一个不相同。
2. 不能重载只有返回值不同的方法名。
3. 存在于父类和子类、同类中。

> ————————————————————————————————————————  
**区别点** | <font color=#0000FF> **重载** </font> | <font color=#008000>**重写（覆写）**</font>  
英文   | <font color=#0000FF>Overloading</font>| <font color=#008000>Overiding</font>  
定义   | <font color=#0000FF>方法名称相同，参数的类型或个数不同</font>| <font color=#008000>方法名称、参数类型、返回值类型全部相同</font>  
权限   | <font color=#0000FF>对权限没要求</font>| <font color=#008000>被重写的方法不能拥有更严格的权限</font>  
范围   | <font color=#0000FF>发生在一个类中</font>| <font color=#008000>发生在继承类中</font>  
——————————————————————————————————————————  

#### 抽象类和接口有什么区别

> 接口是公开的，里面不能有私有的方法或变量，是用于让别人使用的，而抽象类是可以有私有方法或私有变量的.  
> 另外，实现接口的一定要实现接口里定义的所有抽象方法(默认隐藏了abstract关键字)<font color=red>（Java8已经支持有默认方法和静态方法）</font>，而实现抽象类可以有选择地重写需要用到的方法，一般的应用里，最顶级的是接口，然后是抽象类实现接口，最后才到具体类实现。  
> 还有，接口可以实现多重继承，而一个类只能继承一个超类，但可以通过继承多个接口实现多重继承，接口还有标识（里面没有任何方法，如Remote接口）和数据共享（里面的变量全是常量）的作用。

#### 说说反射的用途及实现

> Java反射机制主要提供了以下功能：在运行时构造一个类的对象；判断一个类所具有的成员变量和方法；调用一个对象的方法；生成动态代理。反射最大的应用就是框架.  

##### Java反射的主要功能：
> 1.确定一个对象的类.  
> 2.取出类的modifiers,数据成员,方法,构造器,和超类.  
> 3.找出某个接口里定义的常量和方法说明.  
> 4.创建一个类实例,这个实例在运行时刻才有名字(运行时才生成的对象).  
> 5.取得和设定对象数据成员的值,如果数据成员名是运行时刻确定的也能做到.  
> 6.在运行时刻调用动态对象的方法.  
> 7.创建数组,数组大小和类型在运行时刻才确定,也能更改数组成员的值.  

> _**反射的应用很多，很多框架都有用到**_:  
> 1.spring 的 ioc/di 也是反射….  
> 2.javaBean和jsp之间调用也是反射….  
> 3.struts的 FormBean 和页面之间…也是通过反射调用….  
> 4.JDBC 的 classForName()也是反射….  
> 5.hibernate的 find(Class clazz) 也是反射….  

> 反射还有一个不得不说的问题，就是性能问题，大量使用反射系统性能大打折扣。怎么使用使你的系统达到最优就看你系统架构和综合使用问题啦，这里就不多说了。  
来源：http://uule.iteye.com/blog/1423512

#### 说说自定义注解的场景及实现

> （此题自由发挥，就看你对注解的理解了!）登陆、权限拦截、日志处理，以及各种Java框架，如Spring，Hibernate，JUnit  提到注解就不能不说反射，Java自定义注解是通过运行时靠反射获取注解。实际开发中，例如我们要获取某个方法的调用日志，可以通过AOP（动态代理机制）给方法添加切面，通过反射来获取方法包含的注解，如果包含日志注解，就进行日志记录。  

#### HTTP 请求的 GET 与 POST 方式的区别

> GET方法会把名值对追加在请求的URL后面。因为URL对字符数目有限制，进而限制了用户在客户端请求的参数值的数目。并且请求中的参数值是可见的，因此，敏感信息不能用这种方式传递。  
> POST方法通过把请求参数值放在请求体中来克服GET方法的限制，因此，可以发送的参数的数目是没有限制的。最后，通过POST请求传递的敏感信息对外部客户端是不可见的。  
> 参考：https://www.cnblogs.com/wangli-66/p/5453507.html

#### session 与 cookie 区别

> cookie 是 Web 服务器发送给浏览器的一块信息。浏览器会在本地文件中给每一个 Web 服务器存储 cookie。以后浏览器在给特定的 Web 服务器发请求的时候，同时会发送所有为该服务器存储的 cookie。   

> _**下面列出了 session 和 cookie 的区别**_：  
> 无论客户端浏览器做怎么样的设置，session都应该能正常工作。客户端可以选择禁用 cookie，
但是， session 仍然是能够工作的，因为客户端无法禁用服务端的 session。

#### JDBC 流程

> **1、 加载JDBC驱动程序：**  
> 在连接数据库之前，首先要加载想要连接的数据库的驱动到JVM（Java虚拟机），
这通过java.lang.Class类的静态方法forName(String className)实现。
例如：

	try {
	    //加载MySql的驱动类
	    Class.forName("com.mysql.jdbc.Driver") ;
	} catch(ClassNotFoundException e) {
	    System.out.println("找不到驱动程序类 ，加载驱动失败！");
	    e.printStackTrace() ;
	}
	
> 成功加载后，会将Driver类的实例注册到DriverManager类中。

> **2、 提供JDBC连接的URL**  
> 连接URL定义了连接数据库时的协议、子协议、数据源标识。  
> <font color=blue>书写形式：协议：子协议：数据源标识</font>  
> 协议：在JDBC中总是以jdbc开始; 子协议：是桥连接的驱动程序或是数据库管理系统名称。  
> 数据源标识：标记找到数据库来源的地址与连接端口。  
> 例如：  

	jdbc:mysql://localhost:3306/test?useUnicode=true&characterEncoding=gbk;useUnicode=true;//（MySql的连接URL）
	//表示使用Unicode字符集。如果characterEncoding设置为 gb2312或GBK，本参数必须设置为true 。characterEncoding=gbk：字符编码方式。

> **3、创建数据库的连接**  
> 要连接数据库，需要向java.sql.DriverManager请求并获得Connection对象， 该对象就代表一个数据库的连接。  
> 使用DriverManager的getConnectin(String url , String username , String password)方法传入指定的欲连接的数据库的路径、数据库的用户名和密码来获得。  
> 例如： 

	//连接MySql数据库，用户名和密码都是root
	String url = "jdbc:mysql://localhost:3306/test" ;
	String username = "root" ;
	String password = "root" ;
	try{
	    Connection con = DriverManager.getConnection(url , username , password ) ;
	}catch(SQLException se) {
	    System.out.println("数据库连接失败！");
	    se.printStackTrace() ;
	}

> **4、 创建一个Statement**  
> 要执行SQL语句，必须获得java.sql.Statement实例，Statement实例分为以下3 种类型：  
> 1、执行静态SQL语句。通常通过Statement实例实现。  
> 2、执行动态SQL语句。通常通过PreparedStatement实例实现。  
> 3、执行数据库存储过程。通常通过CallableStatement实例实现。  

> _具体的实现方式_：
	
	Statement stmt = con.createStatement(); 
	PreparedStatement pstmt = con.prepareStatement(sql); 
	CallableStatement cstmt = con.prepareCall("{CALL demoSp(? , ?)}");
	
> **5、执行SQL语句**  
> Statement接口提供了三种执行SQL语句的方法：executeQuery 、executeUpdate 和execute.  
> 1、ResultSet executeQuery(String sqlString)：执行查询数据库的SQL语句 ，返回一个结果集（ResultSet）对象。  
> 2、int executeUpdate(String sqlString)：用于执行INSERT、UPDATE或 DELETE语句以及SQL DDL语句，如：CREATE TABLE和DROP TABLE等.  
> 3、execute(sqlString):用于执行返回多个结果集、多个更新计数或二者组合的语句。   
> _具体实现的代码_：  

	ResultSet rs = stmt.executeQuery(“SELECT * FROM …”); 
	int rows = stmt.executeUpdate(“INSERT INTO …”); 
	boolean flag = stmt.execute(String sql);

> **6、处理结果**  
> _两种情况_：  
> 1、执行更新返回的是本次操作影响到的记录数。  
> 2、执行查询返回的结果是一个ResultSet对象。  

> • ResultSet包含符合SQL语句中条件的所有行，并且它通过一套get方法提供了对这些 行中数据的访问。  
> • 使用结果集（ResultSet）对象的访问方法获取数据：  

	while(rs.next()){
	    String name = rs.getString(“name”) ;
	    String pass = rs.getString(1) ; // 此方法比较高效
	}
> （列是从左到右编号的，并且从列1开始）

> **7、关闭JDBC对象**  
> 操作完成以后要把所有使用的JDBC对象全都关闭，以释放JDBC资源，关闭顺序和声明顺序相反：  
> 1、关闭记录集.  
> 2、关闭声明.  
> 3、关闭连接对象.  

	if (rs != null) { // 关闭记录集
	    try{
	      rs.close() ;
	    }catch(SQLException e){
	      e.printStackTrace() ;
	    }
	}
	if (stmt != null) { // 关闭声明
	    try{
	      stmt.close() ;
	    } catch(SQLException e) {
	      e.printStackTrace() ;
	    }
	}
	if (conn != null) { // 关闭连接对象
	    try{
	      conn.close() ;
	    } catch(SQLException e) {
	      e.printStackTrace() ;
	    }
	}

#### MVC 设计思想

> _MVC就是_:  
> M:Model 模型.  
> V:View 视图.  
> C:Controller 控制器.  

> 模型就是封装业务逻辑和数据的一个一个的模块,控制器就是调用这些模块的(java中通常是用Servlet来实现,框架的话很多是用Struts2来实现这一层),视图就主要是你看到的,比如JSP等.  
> 当用户发出请求的时候,控制器根据请求来选择要处理的业务逻辑和要选择的数据,再返回去把结果输出到视图层,这里可能是进行重定向或转发等.  

#### equals 与 == 的区别

> 值类型（int,char,long,boolean等）都是用 == 判断相等性。对象引用的话，== 判断引用所指的对象是否是同一个。equals是Object的成员函数，有些类会覆盖（override）这个方法，用于判断对象的等价性。  例如String类，两个引用所指向的String都是"abc"，但可能出现他们实际对应的对象并不是同一个（和jvm实现方式有关），因此用==判断他们可能不相等，但用equals判断一定是相等的。  

#### 什么是Java序列化和反序列化；如何实现Java序列化；或者请描述Serializable接口的作用
> **序列化**：把对象转换为字节序列的过程称为对象的序列化；  
> **反序列化**：把字节序列恢复为对象的过程称为对象的反序列化。  
> **如何实现Java序列化**：实现serializable接口.  

> ObjectOutputStream（对象输出流）：  
> 它的 writeObject(Object obj) 方法可对参数指定的obj对象进行序列化，把得到的字节序列写到一个目标输出流中；

> ObjectInputStream（对象输入流）：  
> 它的 readObject() 方法从一个源输入流中读取字节序列，再把他们反序列化为一个对象，并将其返回。

### 集合

#### List 和 Set 区别

> **List,Set都是继承自Collection接口**  
> _List特点_：元素有放入顺序，元素可重复.  
> _Set特点_：元素无放入顺序，元素不可重复，重复元素会覆盖掉.  

> <font color=blue>（注意：元素虽然无放入顺序，但是元素在set中的位置是有该元素的HashCode决定的，其位置其实是固定的，加入Set 的Object必须定义equals()方法 ，另外list支持for循环，也就是通过下标来遍历，也可以用迭代器，但是Set只能用迭代，因为他无序，无法用下标来取得想要的值。）</font>

> **Set和List对比**：  
> _Set_：检索元素效率低下，删除和插入效率高，插入和删除不会引起元素位置改变。  
> _List_：和数组类似，List可以动态增长，查找元素效率高，插入删除元素效率低，因为会引起其他元素位置改变。  

#### List 和 Map 区别
> List是对象集合，允许对象重复。  
> Map是键值对的集合，不允许key重复。  

#### Arraylist 与 LinkedList 区别

> **Arraylist**：  
> _优点_：ArrayList是实现了基于动态数组的数据结构,因为地址连续，一旦数据存储好了，查询操作效率会比较高（在内存里是连着放的）。  
> _缺点_：因为地址连续， ArrayList要移动数据,所以插入和删除操作效率比较低。  

> **LinkedList**：  
> _优点_：LinkedList基于链表的数据结构,地址是任意的，所以在开辟内存空间的时候不需要等一个连续的地址，对于新增和删除操作add和remove，LinedList比较占优势。LinkedList 适用于要头尾操作或插入指定位置的场景.  
> _缺点_：因为LinkedList要移动指针,所以查询操作性能比较低。  
> _适用场景分析_：  
> 当需要对数据进行对此访问的情况下选用ArrayList，当需要对数据进行多次增加删除修改时采用LinkedList。  

#### ArrayList 与 Vector 区别

> **ArrayList有三个构造方法**：

	public ArrayList(int initialCapacity)//构造一个具有指定初始容量的空列表。
	public ArrayList()//构造一个初始容量为10的空列表(ArrayList默认初始容量为10)。
	public ArrayList(Collection<?  extends E> c)//构造一个包含指定 collection 的元素的列表

> **Vector有四个构造方法**：

	public Vector()//使用指定的初始容量和等于零的容量增量构造一个空向量。
	public Vector(int initialCapacity)//构造一个空向量，使其内部数据数组的大小，其标准容量增量为零。
	public Vector(Collection<? extends E> c)//构造一个包含指定 collection 中的元素的向量
	public Vector(int initialCapacity,int capacityIncrement)//使用指定的初始容量和容量增量构造一个空的向量

> **ArrayList和Vector都是用数组实现的，主要有这么三个区别**：  
> Vector是多线程安全的，线程安全就是说多线程访问同一代码，不会产生不确定的结果。而ArrayList不是，这个可以从源码中看出，Vector类中的方法很多有synchronized进行修饰，这样就导致了Vector在效率上无法与ArrayList相比；  
> 两个都是采用的线性连续空间存储元素，但是当空间不足的时候，两个类的增加方式是不同。  
> Vector可以设置增长因子，而ArrayList不可以。  

> Vector是一种老的动态数组，是线程同步的，效率很低，一般不赞成使用。

> **适用场景分析**：
> Vector是线程同步的，所以它也是线程安全的，而ArrayList是线程异步的，是不安全的。如果不考虑到线程的安全因素，一般用ArrayList效率比较高。
如果集合中的元素的数目大于目前集合数组的长度时，在集合中使用数据量比较大的数据，用Vector有一定的优势。

#### HashMap 和 Hashtable 的区别

> 1.hashMap去掉了HashTable 的contains方法，但是加上了containsValue（）和containsKey（）方法。  
> 2.hashTable同步的，而HashMap是非同步的，效率上逼hashTable要高。  
> 3.hashMap允许空键值，而hashTable不允许。  

> **注意**：
> _TreeMap_：非线程安全基于红黑树实现。TreeMap没有调优选项，因为该树总处于平衡状态。  
> _Treemap_：适用于按自然顺序或自定义顺序遍历键(key)。  

> 参考：http://blog.csdn.net/qq_22118507/article/details/51576319

#### HashSet 和 HashMap 区别

> set是线性结构，set中的值不能重复，hashset是set的hash实现，hashset中值不能重复，使用hashmap的put方法来实现Add的。  
> map是键值对映射，可以空键空值。HashMap是Map接口的hash实现，key的唯一性是通过key值hash值的唯一来确定，value值是则是链表结构。  
> <font color=red>他们的共同点都是hash算法实现的唯一性，他们都不能持有基本类型，只能持有对象 </font>.  

#### HashMap 和 ConcurrentHashMap 的区别

> _ConcurrentHashMap是线程安全的HashMap的实现_  
> （1）ConcurrentHashMap对整个桶数组进行了分割分段(Segment)，然后在每一个分段上都用lock锁进行保护，相对于HashTable的syn关键字锁的粒度更精细了一些，并发性能更好，而HashMap没有锁机制，不是线程安全的。  
> （2）HashMap的键值对允许有null，但是ConCurrentHashMap都不允许。  

#### HashMap 的工作原理及代码实现

> 参考：[https://tracylihui.github.io/2015/07/01/Java集合学习1：HashMap的实现原理/ConcurrentHashMap 的工作原理及代码实现](https://tracylihui.github.io/2015/07/01/Java%E9%9B%86%E5%90%88%E5%AD%A6%E4%B9%A01%EF%BC%9AHashMap%E7%9A%84%E5%AE%9E%E7%8E%B0%E5%8E%9F%E7%90%86/)

> HashTable里使用的是synchronized关键字，这其实是对对象加锁，锁住的都是对象整体，当Hashtable的大小增加到一定的时候，性能会急剧下降，因为迭代时需要被锁定很长的时间。  
> ConcurrentHashMap算是对上述问题的优化，其构造函数如下，默认传入的是16，0.75，16。  

	public ConcurrentHashMap(int paramInt1, float paramFloat, int paramInt2)  {
	    //…
	    int i = 0;
	    int j = 1;
	    while (j < paramInt2) {
	       ++i;
	       j <<= 1;
	    }
	    this.segmentShift = (32 - i);
	    this.segmentMask = (j - 1);
	    this.segments = Segment.newArray(j);
	    //…
	    int k = paramInt1 / j;
	    if (k * j < paramInt1) {
	       ++k;
	    }
	    int l = 1;
	    while (l < k) {
	        l <<= 1;
	        }
	    for (int i1 = 0; i1 < this.segments.length; ++i1)
	        this.segments[i1] = new Segment(l, paramFloat);
	    }
	    public V put(K paramK, V paramV)  {
	        if (paramV == null) {
	          throw new NullPointerException();
	        }
	        int i = hash(paramK.hashCode()); //这里的hash函数和HashMap中的不一样  
	        return this.segments[(i >>> this.segmentShift & this.segmentMask)].put(paramK, i, paramV, false);
	    }
	}

> ConcurrentHashMap引入了分割(Segment)，上面代码中的最后一行其实就可以理解为把一个大的Map拆分成N个小的HashTable，在put方法中，会根据hash(paramK.hashCode())来决定具体存放进哪个Segment，如果查看Segment的put操作，我们会发现内部使用的同步机制是基于lock操作的，这样就可以对Map的一部分（Segment）进行上锁，这样影响的只是将要放入同一个Segment的元素的put操作，保证同步的时候，锁住的不是整个Map（HashTable就是锁住的整个Map），相对于HashTable提高了多线程环境下的性能，因此HashTable已经被淘汰了。

### 线程

#### 线程和进程的概念
> **线程**：单个进程中执行的每个任务就是一个线程。线程是进程中执行运算的最小单位；  
> **进程**：是执行中的一段程序，即一旦程序被载入到内存中并准备执行，它就是一个进程；进程表示资源分配的基本概念，又是调度原型的基本单位，是系统中的并发执行的单位。

#### 并行和并发的概念
> **并行**：指应用能够同时执行不同的任务；  
> **并发**：指应用能够交替执行不同的任务。  

#### 创建线程的方式及实现

> **Java中创建线程主要有三种方式**：  

##### 一、继承Thread类创建线程类
> （1）定义Thread类的子类，并重写该类的run方法，该run方法的方法体就代表了线程要完成的任务。因此把run()方法称为<font color=blue>_执行体_</font>。  
> （2）创建Thread子类的实例，即创建了线程对象。  
> （3）<font color=blue>调用线程对象的start()方法来启动该线程。</font>  

	package com.thread;
	
	public class FirstThreadTest extends Thread {
	    int i = 0;
	    //重写run方法，run方法的方法体就是现场执行体
	    public void run() {
	        for (;i<100;i++) {
	          System.out.println(getName()+"  "+i);
	        }
	    }
	    public static void main(String[] args) {
	        for(int i = 0;i< 100;i++) {
	            System.out.println(Thread.currentThread().getName()+"  : "+i);
	            if(i==20) {
	                new FirstThreadTest().start();
	                new FirstThreadTest().start();
	            }
	        }
	    }
	}

> 上述代码中Thread.currentThread()方法返回当前正在执行的线程对象。getName()方法返回调用该方法的线程的名字。  

##### 二、通过Runnable接口创建线程类
> （1）定义runnable接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程执行体。  
> （2）创建 Runnable实现类的实例，并依此实例作为Thread的target来创建Thread对象，该Thread对象才是真正的线程对象。  
> （3）调用线程对象的start()方法来启动该线程。  
	
	package com.thread;
	
	public class RunnableThreadTest implements Runnable {
	
	    private int i;
	    public void run() {
	        for(i = 0;i <100;i++) {
	            System.out.println(Thread.currentThread().getName()+" "+i);
	        }
	    }
	    public static void main(String[] args) {
	        for(int i = 0;i < 100;i++) {
	            System.out.println(Thread.currentThread().getName()+" "+i);
	            if(i==20) {
	                RunnableThreadTest rtt = new RunnableThreadTest();
	                new Thread(rtt,"新线程1").start();
	                new Thread(rtt,"新线程2").start();
	            }
	        }
	    }
	}
	
##### 三、通过Callable和Future创建线程
> （1）创建Callable接口的实现类，并实现call()方法，该call()方法将作为线程执行体，并且有返回值。  
> （2）创建Callable实现类的实例，使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call()方法的返回值。   
> （3）使用FutureTask对象作为Thread对象的target创建并启动新线程。  
> （4）调用FutureTask对象的get()方法来获得子线程执行结束后的返回值.  

	package com.thread;
	
	import java.util.concurrent.Callable;
	import java.util.concurrent.ExecutionException;
	import java.util.concurrent.FutureTask;
	
	public class CallableThreadTest implements Callable<Integer> {
	    public static void main(String[] args) {
	        CallableThreadTest ctt = new CallableThreadTest();
	        FutureTask<Integer> ft = new FutureTask<>(ctt);
	        for(int i = 0;i < 100;i++) {
	            System.out.println(Thread.currentThread().getName()+" 的循环变量i的值"+i);
	            if(i==20) {
	                new Thread(ft,"有返回值的线程").start();
	            }
	        }
	        try {
	            System.out.println("子线程的返回值："+ft.get());
	        } catch (InterruptedException e) {
	            e.printStackTrace();
	        } catch (ExecutionException e) {
	            e.printStackTrace();
	        }
	    }
	    @Override
	    public Integer call() throws Exception {
	        int i = 0;
	        for(;i<100;i++) {
	            System.out.println(Thread.currentThread().getName()+" "+i);
	        }
	        return i;
	    }
	}

> **创建线程的三种方式的对比**  
> _采用实现Runnable、Callable接口的方式创见多线程时_  
> **优势是**：  
>         线程类只是实现了Runnable接口或Callable接口，还可以继承其他类。
在这种方式下，多个线程可以共享同一个target对象，所以非常适合多个相同线程来处理同一份资源的情况，从而可以将CPU、代码和数据分开，形成清晰的模型，较好地体现了面向对象的思想。

> **劣势是**：  
        编程稍微复杂，如果要访问当前线程，则必须使用Thread.currentThread()方法。  

> _使用继承Thread类的方式创建多线程时_  
> **优势是**：  
>         编写简单，如果需要访问当前线程，则无需使用Thread.currentThread()方法，直接使用this即可获得当前线程。  
> **劣势是**：  
>         线程类已经继承了Thread类，所以不能再继承其他父类。  

#### 进程间通信的方式(非线程间通信)
> 进程间通信（IPC，InterProcess  Communication）是指在不同进程之间传播或交换信息。

> **1.无名管道通信**  
> 管道是一种半双工（即数据只能在一个方向上流动）的通信方式，数据只能单向流动，而且只能在具有亲缘关系的进程间使用。进程的亲缘关系通常指父子进程关系。

> **2.高级管道通信**  
> 将另一个程序当做一个新的进程在当前程序进程中启动，则它算是当前程序的子进程，这种方式我们称为高级管道方式。

> **3.有名管道通信**  
> 有名管道也是半双工的通信方式，但是它允许无亲缘关系进程间的通信。

> **4.消息队列通信**  
> 是由消息的链表，存放在内核中并由消息队列标识符标识。消息队列克服了信号传递信息少、管道只能承载无格式字节流以及缓冲区大小受限等缺点。

> **5.信号量通信**  
> 信号量（Semaphore）是一个计数器，可以用来控制多个进程对共享资源的访问。它常作为一种锁机制，防止某进程正在访问共享资源时，其他进程也访问该资源。因此，主要作为进程间以及统一进程内不用线程之间的同步手段。

> **6.信号**  
> 信号是一种比较复杂的通信方式，用于通知接收进程某个事件已经发生。

> **7.共享内存通信**  
> 共享内存就是映射一段能被其他进程所访问的内存，这段共享内存由一个进程创建，但多个进程都可以访问。共享内存是对快的IPC方式，它是针对其他进程间通信方式运行效率低而专门设计的。它往往与其他通信机制，如信号量配合使用，来实现进程间的同步和通信。

> **8.套接字通信**  
> 套接字（socket）：套接字也是一种进程间通信机制，与其他通信机制不同的是，它可用于不同机器间的进程通信。

#### sleep() 、join（）、yield（）有什么区别

##### 1、sleep()方法
> 在指定的毫秒数内让当前正在执行的线程休眠（暂停执行），此操作受到系统计时器和调度程序精度和准确性的影响。让其他线程有机会继续执行，但它并不释放对象锁。也就是如果有Synchronized同步块，其他线程仍然不能访问共享数据。注意该方法要捕获异常!  
> 比如有两个线程同时执行(没有Synchronized)，一个线程优先级为 <font color=blue>MAX-PRIORITY</font>，另一个为 <font color=blue>MIN-PRIORITY</font>，如果没有Sleep()方法，只有高优先级的线程执行完成后，低优先级的线程才能执行；但当高优先级的线程sleep(5000)后，低优先级就有机会执行了。  
> 总之，sleep()可以使低优先级的线程得到执行的机会，当然也可以让同优先级、高优先级的线程有执行的机会。

##### 2、yield()方法
> yield()方法和sleep()方法类似，也不会释放“锁标志”，区别在于，它没有参数，即yield()方法只是使当前线程重新回到可执行状态，所以执行yield()的线程有可能在进入到可执行状态后马上又被执行，另外<font color=blue>yield()方法只能使同优先级或者高优先级的线程得到执行机会</font>，这也和sleep()方法不同。

##### 3、join()方法
> Thread 的非静态方法 join() 让一个线程B“加入”到另外一个线程A的尾部。在A执行完毕之前，B不能工作。

	Thread t = new MyThread();
	t.start();
	t.join();

> 保证当前线程停止执行，直到该线程所加入的线程执行完成为止。然而，如果它加入的线程没有存活，则当前线程不需要停止。

#### 说说 CountDownLatch 原理

> 参考：  
> [分析CountDownLatch的实现原理](https://www.jianshu.com/p/7c7a5df5bda6?ref=myread)  
> [什么时候使用CountDownLatch](http://www.importnew.com/15731.html)  
> [Java并发编程：CountDownLatch、CyclicBarrier和Semaphore](http://www.cnblogs.com/dolphin0520/p/3920397.html)

#### 说说 CyclicBarrier 原理

> 参考：  
> [JUC回顾之-CyclicBarrier底层实现和原理](http://www.cnblogs.com/200911/p/6060195.html)

#### 说说 Semaphore 原理
> Semaphore（信号量） 是用来控制同时访问特定资源的线程数量，它通过协调各个线程，保证合理的使用公共资源。

> 线程可以通过 acquire() 方法来获取信号量的许可。当信号量中没有可用的许可的时候，线程阻塞，直到有可用的许可为止。线程可以通过 release() 方法释放它持有的信号量的许可。

> Semaphore 内部基础AQS的共享模式，所以实现都委托给了Sync类。

> **Semaphore 有两种模式**：  

> _公平模式_：  
> 调用 acquire() 的顺序就是获取许可证的顺序，遵循FIFO；

> _非公平模式_：  
> 为抢占式的，可能一个新的获取线程恰好在一个许可证释放时得到这个许可证，而前面还有等待的线程。

> 更多相关文章：  
> [JAVA多线程–信号量(Semaphore)](https://my.oschina.net/cloudcoder/blog/362974)  
> [JUC回顾之-Semaphore底层实现和原理](https://www.cnblogs.com/200911/p/6060359.html)  

#### 说说 Exchanger 原理
> 主要用于两个工作线程之间交换数据。

> 更多相关文章：  
> [Java Exchanger 原理](https://blog.csdn.net/coslay/article/details/45242581)
> [java.util.concurrent.Exchanger应用范例与原理浅析](http://lixuanbin.iteye.com/blog/2166772)

#### 说说 CountDownLatch 与 CyclicBarrier 区别


> <font color=blue>**CountDownLatch**</font>	&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;
> <font color=green>**CyclicBarrier**</font>  

> <font color=blue>减计数方式</font>	&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;<font color=green>加计数方式</font>  

> <font color=blue>计算为0时释放所有等待的线程	</font>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;	<font color=green>计数达到指定值时释放所有等待线程</font>  

> <font color=blue>计数为0时，无法重置	</font>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;	<font color=green>计数达到指定值时，计数置为0重新开始</font>  

> <font color=blue>调用countDown()方法计数减一，</font>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;<font color=green>调用await()方法计数加1，</font></br><font color=blue>调用await()方法只进行阻塞，</font>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;<font color=green>若加1后的值不等于构造方法的值，</font></br><font color=blue>对计数没任何影响</font>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;	<font color=green>则线程阻塞</font>  

> <font color=blue>不可重复利用</font>&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;	<font color=green>可重复利用</font>  

> [尽量把CyclicBarrier和CountDownLatch的区别说通俗点](http://aaron-han.iteye.com/blog/1591755)

> 两者的使用场景，下面的文章说的很清楚：  
> [CountDownLatch 和 CyclicBarrier 的使用场景](https://blog.csdn.net/zzg1229059735/article/details/61191679)

#### ThreadLocal 原理分析

> [Java并发编程：深入剖析ThreadLocal](https://www.cnblogs.com/dolphin0520/p/3920407.html)

#### ThreadLocal 原理分析；ThreadLocal为什么会出现OOM，出现的深层次原理
> ThreadLocal 是线程的局部变量，是每一个线程所单独持有的，其他线程不能对其进行访问。通常是类中的 private  static 字段，是对该字段初始值的一个拷贝，它们希望将状态与某一个线程（例如用户ID或者事务ID）相关联。

> ThreadLocal 为什么会出现OOM：
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/05.jpg)
          

> ThreadLocal 的实现是这样的：每个 Thread 维护一个 ThreadLocalMap 映射表，这个映射表的 key 是 ThreadLocal 实例本身，value 是真正需要存储的 Object;

> ThreadLocal 里面使用了一个存在弱引用的 map ，map 的类型是 ThreadLocal.ThreadLocalMap。Map 中的 key 为一个 ThreadLocal 实例本身，而这个 key 使用弱引用指向 ThreadLocal 。当 ThreadLocal 实例置为 null 后，没有任何强引用指向 ThreadLocal 实例，所以ThreadLocal 将会被 GC 回收。但是我们的 value 却不能回收，而这块 value 永远不会被访问到。所以存在着内存泄漏。因为存在一条从 Current Thread 链接过来的强引用，只有当 Thread 结束以后， Current Thread 就不会存在栈中，强引用断开，Current Thread、Map Value 将全部GC回收。

> **如何避免内存泄漏**：  
> 每次使用完 ThreadLocal，都调用它的 remove() 方法，清除数据。


#### 讲讲线程池的实现原理
> 提交一个任务到线程池中，线程池的处理流程如下：  

> 1.判断线程池里的核心线程是否都在执行任务，如果不是（核心线程空闲或者还有核心线程没有被创建），则创建一个新的工作线程来执行任务。如果核心线程都在执行任务，则进入下个流程；  
> 2.线程池判断工作队列是否已满，如果工作队列没有满，则将新提交的任务存储到这个工作队列里；如果工作队列满了，则进入下个流程；  
> 3.判断线程池的线程是否都处于工作状态，如果没有，则创建一个新的工作线程来执行任务。如果已经满了，则交给饱和策略来处理这个任务。  

![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/06.jpg)

> 主要是ThreadPoolExecutor的实现原理.  
> [Java并发编程：线程池的使用](http://www.cnblogs.com/dolphin0520/p/3932921.html)

#### 线程池的几种方式

##### newFixedThreadPool(int nThreads)
> 创建一个固定长度的线程池，每当提交一个任务就创建一个线程，直到达到线程池的最大数量，这时线程规模将不再变化，当线程发生未预期的错误而结束时，线程池会补充一个新的线程.  

    ExecutorService executorService = Executors.newFixedThreadPool(3);
	for (int i = 0; i < 10; i++) {
	    final int index = i;
	    executorService.execute(new Runnable() {
	        @Override
	        public void run() {
	            log.info("task:{}",index);
	        }
	    });
	}
	executorService.shutdown();

##### newCachedThreadPool()
> 创建一个可缓存的线程池，如果线程池的规模超过了处理需求，将自动回收空闲线程，而当需求增加时，则可以自动添加新线程，线程池的规模不存在任何限制.  
	
	ExecutorService executorService = Executors.newCachedThreadPool();
	for (int i = 0; i < 10; i++) {
        final int index = i;
        executorService.execute(new Runnable() {
            @Override
            public void run() {
                log.info("task:{}",index);
            }
        });
	}
	executorService.shutdown();

##### newSingleThreadExecutor()
> 这是一个单线程的Executor，它创建单个工作线程来执行任务，如果这个线程异常结束，会创建一个新的来替代它；它的特点是能确保依照任务在队列中的顺序来串行执行.  

    ExecutorService executorService = Executors.newSingleThreadExecutor();
    for (int i = 0; i < 10; i++) {
        final int index = i;
        executorService.execute(new Runnable() {
            @Override
            public void run() {
                log.info("task:{}",index);
            }
        });
    }
    executorService.shutdown();

##### newScheduledThreadPool(int corePoolSize)
> 创建了一个固定长度的线程池，而且以延迟或定时的方式来执行任务，类似于Timer。

    ScheduledExecutorService executorService = Executors.newScheduledThreadPool(5);
 
    // 延迟一秒之后，每隔三秒执行一次
    executorService.scheduleAtFixedRate(new Runnable() {
        @Override
        public void run() {
            log.info("scheduled run");
        }
    },1,3,TimeUnit.SECONDS);
 
    // 也可以使用timer的schedule方法来实现定时功能
    Timer timer = new Timer();
    timer.schedule(new TimerTask() {
        @Override
        public void run() {
            log.info("timer run");
        }
    },new Date(),5*1000);

> **举个栗子**  

	private static final Executor exec=Executors.newFixedThreadPool(50);
	
	Runnable runnable=new Runnable(){
	    public void run(){
	        ...
	    }
	}
	exec.execute(runnable);
	
	Callable<Object> callable=new Callable<Object>() {
	    public Object call() throws Exception {
	        return null;
	    }
	};
	
	Future future=executorService.submit(callable);
	future.get(); // 等待计算完成后，获取结果
	future.isDone(); // 如果任务已完成，则返回 true
	future.isCancelled(); // 如果在任务正常完成前将其取消，则返回 true
	future.cancel(true); // 试图取消对此任务的执行，true中断运行的任务，false允许正在运行	的任务运行完

> **参考：**  
[创建线程池的几种方式](http://blog.csdn.net/cyantide/article/details/50880211)  
[线程池相关概念](https://blog.csdn.net/ibelievesmile/article/details/81099556)

#### 线程的生命周期

> **新建(New)**、**就绪（Runnable）**、**运行（Running）**、**阻塞(Blocked)**和**死亡(Dead)**5种状态.  

> _**生命周期的五种状态**_  
> **新建（new Thread）**  
> 当创建Thread类的一个实例（对象）时，此线程进入新建状态（未被启动）。
> _例如_：  
	
	Thread  t1=new Thread();
	
> **就绪（runnable）**  
> 线程已经被启动，正在等待被分配给CPU时间片，也就是说此时线程正在就绪队列中排队等候得到CPU资源。  
> _例如_：
	
	t1.start();
	
> **运行（running）**  
> 线程获得CPU资源正在执行任务（run()方法），此时除非此线程自动放弃CPU资源或者有优先级更高的线程进入，线程将一直运行到结束。  

> **死亡（dead）**  
> 当线程执行完毕或被其它线程杀死，线程就进入死亡状态，这时线程不可能再进入就绪状态等待执行。  

> _自然终止_：正常运行run()方法后终止.  

> _异常终止_：调用**stop()**方法让一个线程终止运行.  

> **堵塞（blocked）**  
> 由于某种原因导致正在运行的线程让出CPU并暂停自己的执行，即进入堵塞状态。  

> _正在睡眠_：用sleep(long t) 方法可使线程进入睡眠方式。一个睡眠着的线程在指定的时间过去可进入就绪状态。  

> _正在等待_：调用wait()方法。（调用motify()方法回到就绪状态）  

> _被另一个线程所阻塞_：调用suspend()方法。（调用resume()方法恢复）  

> **参考：**  
> [线程的生命周期](https://www.cnblogs.com/langjunnan/p/6444718.html)

#### 锁机制

##### 说说线程安全问题

> 线程安全是指要控制多个线程对某个资源的有序访问或修改，而在这些线程之间没有产生冲突。  

> **在Java里，线程安全一般体现在两个方面**：  
> 1、多个thread对同一个java实例的访问（read和modify）不会相互干扰，它主要体现在关键字synchronized。如ArrayList和Vector，HashMap和Hashtable（后者每个方法前都有synchronized关键字）。如果你在interator一个List对象时，其它线程remove一个element，问题就出现了。  
> 2、每个线程都有自己的字段，而不会在多个线程之间共享。它主要体现在java.lang.ThreadLocal类，而没有Java关键字支持，如像static、transient那样。

##### volatile 实现原理

> [聊聊并发（一）——深入分析Volatile的实现原理](http://www.infoq.com/cn/articles/ftf-java-volatile)

##### 悲观锁 乐观锁

> 乐观锁 悲观锁  
> 是一种思想。可以用在很多方面。  

> **比如数据库方面**  
> 悲观锁就是for update（锁定查询的行）.  
> 乐观锁就是 version字段（比较跟上一次的版本号，如果一样则更新，如果失败则要重复读-比较-写的操作。）.  

> **JDK方面**：  
> 悲观锁就是sync.  
> 乐观锁就是原子类（内部使用CAS实现）.  
> 本质来说，就是悲观锁认为总会有人抢我的。  
> 乐观锁就认为，基本没人抢。  

##### AQS 同步队列
> 用来构建锁或者其他同步组件的基础框架，它使用了一个 int 成员变量表示同步状态，通过内置FIFO队列来完成资源获取线程的排队工作。

##### CAS 乐观锁

> 乐观锁是一种思想，即认为读多写少，遇到并发写的可能性比较低，所以采取在写时先读出当前版本号，然后加锁操作（比较跟上一次的版本号，如果一样则更新），如果失败则要重复读-比较-写的操作。  
CAS是一种更新的原子操作，比较当前值跟传入值是否一样，一样则更新，否则失败。  
CAS顶多算是乐观锁写那一步操作的一种实现方式罢了，不用CAS自己加锁也是可以的。  

##### ABA 问题

> **ABA**：如果另一个线程修改V值假设原来是A，先修改成B，再修改回成A，当前线程的CAS操作无法分辨当前V值是否发生过变化。  
> 参考：  
> [Java CAS 和ABA问题](https://www.cnblogs.com/549294286/p/3766717.html)

##### 乐观锁的业务场景及实现方式

> **乐观锁（Optimistic Lock）**：  
> 每次获取数据的时候，都不会担心数据被修改，所以每次获取数据的时候都不会进行加锁，但是在更新数据的时候需要判断该数据是否被别人修改过。如果数据被其他线程修改，则不进行数据更新，如果数据没有被其他线程修改，则进行数据更新。由于数据没有进行加锁，期间该数据可以被其他线程进行读写操作。  

> **乐观锁**：  
> 比较适合读取操作比较频繁的场景，如果出现大量的写入操作，数据发生冲突的可能性就会增大，为了保证数据的一致性，应用层需要不断的重新获取数据，这样会增加大量的查询操作，降低了系统的吞吐量。  

##### 重入锁的概念；重入锁为什么可以防止死锁
> **重入锁**：指的是以线程为单位，当一个线程获取对象锁之后，这个线程可以再次获取对象上的锁。而其他的线程是不可以的。  
> **死锁**：如果一个进程集合里面的每个进程都在等待这个集合中的其他一个进程（包括自身）才能继续往下执行，若无外力他们将无法推进。这个情况就是死锁。处于死锁状态的进程成为死锁进程。

##### 产生死锁的四个条件
> _1.互斥条件_  
> 进程对所分配到的资源不允许其他进程进行访问，若其他进程访问该资源，只能等待，直至占有该资源的进程使用完成后释放该资源；

> _2.请求和保持条件_  
> 进程获得一定的资源之后，又对其他资源发出请求，但是该资源可能被其他进程占有，此时请求阻塞，但是又对自己获得的的资源保持不放；

> _3.不可剥夺条件_  
> 是指进程已获得的资源，在未完成使用之前，不可被剥夺，只能在使用完成后自己释放；

> _4.环路等待条件_  
> 是指进程发生死锁后，必然存在一个进程 --- 资源之间的环形链。

##### 常见的原子操作类
> [Java 中的原子操作类](https://blog.csdn.net/huzhigenlaohu/article/details/51646455)

##### 如何检查死锁
> 通过 jConsole（JDK 自带的图形化界面工具） 检查死锁.   
> 更多相关文章：  
> [Java--死锁以及死锁的排查](https://cloud.tencent.com/developer/article/1347601)

##### 偏向锁、轻量级锁、重量级锁、自旋锁的概念
> **偏向锁**：  
> 为了在无多线程竞争的情况下尽量减少不必要的轻量级锁执行路径；

> **轻量级锁**：  
> 为了在无多线程竞争的前提下，减少传统的重量级锁使用操作系统互斥量产生的性能消耗；

> **重量级锁**：  
> 通过对象内部的监视器（montior）实现，其中 montior 的本质是依赖于底层操作系统的 Mutex Lock 实现，操作系统实现线程之间的切换需要从用户态到内核态的切换，切换成本非常高；

> **自旋锁**：  
>  就是让该线程等待一段时间，不会被立即挂起，看持有锁的线程是否很快释放锁。

> [锁优化相关知识点](https://blog.csdn.net/shandian000/article/details/54927876/)

#### synchronized 实现原理（对象监视器）
> 依赖 JVM 实现。

> 每个对象都有一个监视器锁（monitor）。当 montior 被占用时，就会处于锁定状态，线程执行 monitorEnter 指令时尝试获取 monitor 的所有权，过程如下：

> 1.如果 monitor 的进入数为0，则该线程进入 monitor ，然后将进入数设置为1，该线程即为 monitor 所有者；  
> 2.如果线程已经占有该 monitor ，只是重新进入，则进入 monitor 的进入数加1；  
> 3.如果其他线程已经占用了 monitor，则该线程进入阻塞状态，直到 monitor 的进入数为0，再重新尝试获取 monitor 的所有权。  

#### synchronized 与 lock 的区别
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/07.png)

#### Java 8 并发包下常见的并发类
> [Java 并发包常用类小结](https://blog.csdn.net/dghafq/article/details/77838531)


## JVM(Java虚拟机)&JDK

### JVM相关

#### JVM 运行时内存区域划分

> **首先了解下什么是 JVM 内存**：

> Java 源代码文件（.java后缀）会被 Java 编译器编译为字节码文件（.class后缀），然后由 JVM 中的类加载器加载各个类的字节码文件，加载完毕之后，交由 JVM 执行引擎执行。在整个程序执行过程中，JVM 会用一段空间来存储程序执行期间需要用到的数据和相关信息，这段空间一般被称作为 Runtime Data Area（运行时数据区），也就是我们常说的 JVM 内存。因此，在 Java 中我们常常说到的内存管理就是针对这块空间进行管理（如何分配和回收空间）。

> 根据《Java 虚拟机规范》的规定，运行时数据区通常包括这几个部分：

> **程序计数器（Program Counter Register）**：  
> 指向当前线程所执行的字节码指令的地址，通常也叫作行号指示器；

> **虚拟机栈（VM Stack）**：  
> 描述的是 Java 方法执行的内存模型，方法执行的同时会创建一个栈帧，用于存储方法中的局部变量表、操作数栈、动态链接、方法的出口等信息，每个方法从调用直到执行完成的过程，就对应着一个栈帧在虚拟机栈中入栈到出栈的过程；

> **本地方法栈（Native Method Stack）**：  
> 跟虚拟机栈类似。区别在于本地方法栈是为 Native 方法服务而虚拟机栈是为 Java 方法服务；

> **方法区（Method Area）**：  
> 与堆（Heap）一样所有线程所共享的内存区域，它用于存储已被虚拟机加载的类信息、常量、静态变量、及时编译器编译后的代码等数据。

> **堆（Heap）**：  
> Java 堆是 Java 虚拟机所管理的内存中最大的一块。Java 堆是被所有线程所共享的一块内存区域，虚拟机启动时创建，几乎所有对象的实例都存储在堆中，所有的对象和数组都要在堆上分配内存。

#### 常见的 GC 回收算法及其含义

> **什么是 GC**：  
> GC 是将 Java 的无用的堆对象进行清理，释放内存，以免发生内存泄漏。

##### 常见的回收算法  

> **标记-清除 算法**：  
> _标记阶段_：先通过根节点，标记所有从根节点开始的可达对象。因此，未被标记的对象就是未被引用的垃圾对象；  
> _清除阶段_：清除所有未被标记的对象；  

> **复制算法（新生代的 GC）**：  
> 将原有的内存空间分为两块，每次只使用其中一块，在垃圾回收时，将正在使用的内存中的存活对象复制到未使用的内存块中，然后清除正在使用的内存块中的所有对象；

> **标记-整理 算法（老年代的 GC）**：  
> _标记阶段_：先通过根节点，标记所有从根节点开始的可达对象。因此，未被标记的对象就是未被引用的垃圾对象；  
> _整理阶段_：将所有的存活对象压缩到内存的一端；之后，清理边界外所有的空间；  

> **分代收集算法**：  
> _存活率低_：少量对象存活，适合用复制算法：在新生代中，每次 GC 时都发现有大批对象死去，只有少量存活（新生代中98%的对象都是 "朝生夕死"），那就选用复制算法，只需要付出少量存活对象的复制成本就可以完成 GC；  
> _存活率高_：大量对象存活，适合用标记-清除/标记-整理：在老年代中，因为对象存活率高，没有额外空间对他进行分配担保，就必须使用 标记-清除/标记-整理 算法进行 GC。

#### 常见的 JVM 性能监控和故障处理工具类

> **jmap**：观察运行中的 JVM 物理内存的占用情况；  
> **jps**：列出所有的 JVM 实例；  
> **jvmtop**：一个轻量级的控制台程序用来监控机器上运行的所有 java 虚拟机；  
> **jstack**：观察 jvm 中当前所有线程的运行情况和线程当前状态；  
> **jstat**：JVM 统计监测工具；  
> **jconsole**：内置 Java 性能分析器。  

#### JVM 性能调优

> **调优的目的**：为了令应用程序使用最小的硬件消耗来承载更大的吞吐。  
> JVM 调优主要是针对垃圾收集器的收集性能优化，令运行在虚拟机上的应用能够使用更少的内存以及延迟获取更大的吞吐量。  
> [JVM 性能调优](https://www.cnblogs.com/csniper/p/5592593.html)

#### 类加载器、双亲委派模型

##### 类加载器
> **启动类加载器（BootStrap ClassLoader）**：负责加载 JAVA-HOME\lib 目录中的，或通过 -Xbootclasspath 参数指定路径中的，且被虚拟机认可（按文件名识别，如 rt、jar ）的类；  
> **扩展类加载器（Extension ClassLoader）**：负责加载 JAVA-HOME\lib\ext 目录中的，或通过 java.ext.dirs 系统变量指定路径中的类库；  
> **应用程序类加载器（Application ClassLoader）**：负责加载用户路径（classpath） 上的类库。  

##### 双亲委派模型
> **工作过程**：如果一个类加载器收到了类加载的请求，它首先不会自己去尝试加载这个类，而是把这个请求委托给父类加载器去完成，每一个层次的类加载器都是如此，因此所有的加载请求最终都应该传送到顶层的启动类加载器中，只有当父类加载器反馈自己无法完成这个加载请求（它的搜索范围中没有找到所需要加载的类）时，子加载器才会尝试自己去加载。  
> **好处**：能够有效确保一个类的全局唯一性，当程序中出现多个限定名相同的类时，类加载器在执行加载时，始终只会加载其中的某一个类；

#### 类加载的过程
##### 加载  
> 加载是类加载过程中的一个阶段，这个阶段会在内存中生成一个代表这个类的 java.lang.class 对象，作为方法区这个类的各种数据的入口。  

##### 链接  
> _验证_：这一阶段的主要目的是为了确保 class 文件的字节流中包含的信息是否符合当前虚拟机的要求，并且不会危害虚拟机自身的安全；  
> _准备_：准备阶段是正式为类变量分配内存并设置类变量的初始值阶段，即在方法区中分配这些变量所使用的内存空间。  
> _解析_：解析阶段是指虚拟机将常量池中的符号引用替换为直接引用的过程。  
> _符号引用_：与虚拟机实现的布局无关，引用的目标并不一定要已经加载到内存中。各种虚拟机实现的内存布局可以各不相同，但是它们能接受的符号引用必须是一直的，因为符号引用的字面量形式明确定义在 Java 虚拟机规范的 Class 文件格式中；  
> _直接引用_：是指向目标的指针，相对偏移量或是一个能间接定位到目标的句柄。如果有了直接引用，那引用的目标必定已经在内存中存在。  

##### 初始化
> 初始化阶段是类加载的最后一个阶段。前面的类加载阶段之后，除了在加载阶段可以自定义类加载器以外，其他操作都是由 JVM 主导。到了初始阶段，才开始真正执行类中定义的 Java 程序代码。

#### 强引用、软引用、弱引用、虚引用
> _强引用_：只要引用存在，垃圾回收器永远不会回收；  
> _软引用_：非必须引用，内存溢出之前进行回收；  
> _弱引用_：第二次垃圾回收时回收；  
> _虚引用_：垃圾回收时回收，无法通过引用取到对象值。  

#### Java 内存模型 JMM
> JMM 解决了 可见性和有序性的问题，而锁解决了原子性的问题。  
> **特性**：  
> _原子性_：指的是一个操作是不可中断的，即使是在多线程环境下，一个操作一旦开始就不会被其他线程影响；  
> _可见性_：指的是当一个线程修改了某个共享变量的值，其他线程是否能够马上得知这个修改的值；  
> _有序性_：指的是数据不相关的变量在并发的情况下，实际执行的结果和单线程的执行结果是一样的，不会因为重排序的问题导致结果不可预知。  

## 核心篇

### 数据存储

#### DDL、DML、DCL 分别指什么
> _DML（data manipulation language）_： 数据库操作语言。就是我们经常用到的 SELECT 、UPDATE 、INSERT 、DELETE 等；  
> _DDL（data definition language）_： 数据库定义语言。就是我们经常用到的 CREATE 、ALTER 、DROP 等。DDL 主要是用在定义或改变表的结构、数据类型、表之间的链接和约束等初始化工作上；  
> _DCL（data control language）_：数据库控制语言。是用来设置或改变数据库用户或角色权限的语句，包括（ GRANT 、DENY 、REVOKE 等）语句。  

#### explain 命令
> explain 命令显示了 Mysql 如何使用索引来处理 SELECT 语句以及连接表。可以帮助选择更好的索引和写出更优化的查询语句。  
> 使用方法：在 SELECT 语句前加上 explain 就可以了。  
> explain 列说明：  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/08.png)
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/09.png)
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/10.png)
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/11.png)

#### 数据库事务 ACID

> **Atomicity（原子性）**：原子性要求每个事务中的所有操作要么全部完成，要么就像全部没有发生一样；如果事务中的部分操作失败了，则整个事务失败，结果就是数据库中的状态保持没变；  
> **Consistency（一致性）**：一致性确保了任何事务都会使数据库从一种合法的状态变为另一种合法的状态；  
> **Isolation（隔离性）**：隔离性保证了并发执行多个事务对系统状态的影响和串行化执行多个事务对系统状态的影响是一样的；  
> **Durability（持久性）**：持久性保证了一个事务一旦被提交以后，其状态就保持不变，甚至是发生了主机断电、崩溃、错误等。  

#### 脏读、幻读、不可重复读
> **脏读**：是指一个事务处理过程中读取了另一个未提交的事务中的数据；  
> **幻读**：是事务非独立执行时发生的一种现象；  
> **不可重复读**：是指在对于数据库中的某个数据，一个事务范围内多次查询却返回了不同的数据值，这是由于在查询间隔，被另一个事务修改并提交了。  

> 幻读和不可重复读都是读取了另一条已经提交的事务（这点就脏读不同），所不同的是不可重复读查询的都是同一个数据项，而幻读针对的是一批数据整体（比如数据的个数）。  

#### 事务的隔离级别
> **Serializable（串行化）**：可避免脏读、不可重复读、幻读的发生；  
> **Repeatable read（可重复读）**：可避免脏读、不可重复读的发生；  
> **Read commited（读已提交）**：可避免脏读的发生；  
> **Read uncommited（读未提交）**：最低级别，任何情况都无法保证。  

> 以上四种级别中，隔离级别最高的是 Serializable ，级别最低的是 Read uncommited 。级别越高，执行效率就越低。

> <font color=red>在 Mysql 数据库默认的隔离级别为 Read commited 级别。</font>

> 更多相关文章：  
> [数据库隔离级别](https://blog.csdn.net/baidu_37107022/article/details/77481670)

#### 数据库的几大范式
> 第一范式：确保每列的原子性；  
> 第二范式：确保表中的每列都和主键相关，要求每个表只描述一件事情；  
> 第三范式：确保每列都和主键列直接相关，而不是间接相关。  

#### 说说分库与分表设计
> **分表**：对于访问极为频繁且数据量巨大的单表来说，我们首先要做的就是减少单表的记录条数，以便减少数据查询所需要的时间，提高数据库的吞吐；  
> **分库**：分表能够解决单表数据量过大带来的查询效率下降的问题，但是却无法给数据库的并发处理能力带来质的提升。所以需要对数据库进行拆分，从而提高数据库的写入能力。  

#### 分库与分表带来的分布式困境与对应之策
> [分库与分表带来的分布式困境与应对之策](http://blog.720ui.com/2017/mysql_core_09_multi_db_table2/#%E6%95%B0%E6%8D%AE%E8%BF%81%E7%A7%BB%E4%B8%8E%E6%89%A9%E5%AE%B9%E9%97%AE%E9%A2%98)

#### 说说 SQL 优化之道
> 1.减少查询字段数；  
> 2.表关联尽量用主键；  
> 3.查询条件尽量避免模糊查询；  
> 4.避免使用排序字段，排序字段尽量使用主键；  
> 5.尽量使用限制查询条件；  
> 6.查询条件使用有效索引。  


#### MySQL 索引使用的注意事项

> 参考：  
> [mysql索引使用技巧及注意事项](https://www.cnblogs.com/heyonggang/p/6610526.html)

#### 说说反模式设计

> 参考：  
> [每个程序员要注意的 9 种反模式](http://blog.jobbole.com/87413/)

#### 说说分库与分表设计

> [分表与分库使用场景以及设计方式](http://blog.csdn.net/winy_lm/article/details/50708493)

#### 分库与分表带来的分布式困境与应对之策

> [服务端指南 数据存储篇 | MySQL（09） 分库与分表带来的分布式困境与应对之策](http://blog.720ui.com/2017/mysql_core_09_multi_db_table2/#%E6%95%B0%E6%8D%AE%E8%BF%81%E7%A7%BB%E4%B8%8E%E6%89%A9%E5%AE%B9%E9%97%AE%E9%A2%98)

#### 说说 SQL 优化之道

> [sql优化的几种方法](http://blog.csdn.net/jie_liang/article/details/77340905)

### MySQL 遇到的死锁问题

> 参考：  
> [Mysql并发时经典常见的死锁原因及解决方法](https://www.cnblogs.com/zejin2008/p/5262751.html)

#### 存储引擎的 InnoDB 与 MyISAM

> 1）InnoDB支持事务，MyISAM不支持，这一点是非常之重要。事务是一种高级的处理方式，如在一些列增删改中只要哪个出错还可以回滚还原，而MyISAM就不可以了。  
> 2）MyISAM适合查询以及插入为主的应用，InnoDB适合频繁修改以及涉及到安全性较高的应用.  
> 3）InnoDB支持外键，MyISAM不支持.  
> 4）从MySQL5.5.5以后，InnoDB是默认引擎.  
> 5）InnoDB不支持FULLTEXT类型的索引.  
> 6）InnoDB中不保存表的行数，如select count() from table时，InnoDB需要扫描一遍整个表来计算有多少行，但是MyISAM只要简单的读出保存好的行数即可。注意的是，当count()语句包含where条件时MyISAM也需要扫描整个表.  
> 7）对于自增长的字段，InnoDB中必须包含只有该字段的索引，但是在MyISAM表中可以和其他字段一起建立联合索引.  
> 8）清空整个表时，InnoDB是一行一行的删除，效率非常慢。MyISAM则会重建表.  
> 9）InnoDB支持行锁（某些情况下还是锁整表，如 update table set a=1 where user like ‘%lee%’.  

> **InnoDB 与 MyISAM 的优缺点**：

> **InnoDb** ：这种类型是事务安全的。  
> _优点_：支持事务，支持外键，并发量较大，适合大量 update；  
> _缺点_：查询数据相对较慢，不适合大量的 select。  
> **MyISAM**：  
> _优点_：查询数据相对较快，适合大量的 select ，可以全文索引；  
> _缺点_：不支持事务，不支持外键，并发量较小，不适合大量 update。  

> **使用场景**：  
> 如果你的应用程序一定要使用事务，毫无疑问你要选择 InnoDb 引擎；  
> 如果你的应用程序对查询性能要求较高，就要使用 MyISAM 引擎。  

> 参考：   
> [MySQL存储引擎之MyIsam和Innodb总结性梳理](https://www.cnblogs.com/wt645631686/p/6868678.html)

#### 数据库索引的原理

> 参考：  
> [http://blog.csdn.net/suifeng3051/article/details/52669644](http://blog.csdn.net/suifeng3051/article/details/52669644)

#### 为什么要用 B-tree

> 鉴于B-tree具有良好的定位特性，其常被用于对检索时间要求苛刻的场合，例如：  
> 1、B-tree索引是数据库中存取和查找文件(称为记录或键值)的一种方法。  
> 2、硬盘中的结点也是B-tree结构的。与内存相比，硬盘必须花成倍的时间来存取一个数据元素，这是因为硬盘的机械部件读写数据的速度远远赶不上纯电子媒体的内存。与一个结点两个分支的二元树相比，B-tree利用多个分支（称为子树）的结点，减少获取记录时所经历的结点数，从而达到节省存取时间的目的。  

#### 索引类别（B+树索引、全文索引、哈希索引）；索引的区别
> **FULLTEXT**：即为全文索引。目前只有 MyISAM 引擎支持；  
> **HASH**：即为哈希索引。HASH 索引可以一次定位，不需要像树形索引那样逐层查找，因此具有极高的效率；  
> **BTREE**：即为B+树索引。BTREE 索引就是一种将索引值按一定的算法，存入一个属性的数据结构中（二叉树），每次查询都是从树的入口 root 开始，依次遍历 node，获取 leaf 。这是 MySQL 里默认和最常用的索引类型。  
 

#### 什么是自适应哈希索引（AHI）
> InnoDB 存储引擎会监控对应表上各索引页的查询。如果观察到建立哈希索引可以带来速度提升，则建立哈希索引，称之为自适应哈希索引（Adaptive Hash Index,AHI）。AHI 是通过缓冲池的 B+ 树页构造而来，因此建立的速度很快，而且不需要对整张表构建哈希索引。InnoDB 存储引擎会自动根据访问的频率和模式来自动地为某些热点页建立哈希索引。

#### 为什么要用 B+tree 作为 MySql 索引的数据结构
> 鉴于 B-TREE 具有良好的定位特性，其常被用于对检索时间要求苛刻的场合，例如：

> 1).B-TREE 索引是数据库中存取和查找文件（称为记录或键值）的一种方法；  
> 2).硬盘中的节点也是 B-TREE 结构的。与内存相比，硬盘必须花成倍的时间来存取一个数据元素，这是因为硬盘的机械部件读取数据的速度远远赶不上纯电子媒体的内存。与一个节点两个分支的二元树相比， B-TREE 利用多个分支（称为子树）的节点，减少获取记录时所经历的节点数，从而达到节省存取时间的目的。

#### 聚集索引与非聚集索引的区别

> 参考：  
> [快速理解聚集索引和非聚集索引](http://blog.csdn.net/zc474235918/article/details/50580639)

#### limit 20000 加载很慢怎么解决

> LIMIT n 等价于 LIMIT 0,n  
> 此题总结一下就是让limit走索引去查询，例如：order by 索引字段，或者limit前面根where条件走索引字段等等。
> 参考：   
> [MYSQL分页limit速度太慢优化方法](http://ourmysql.com/archives/1451)

#### 常见的几种分布式 ID 的设计方案

##### UUID（Universally Unique Identifier)

> 16字节128位，通常以36长度的字符串表示。   
> **优点**：  
> 	本地生成 ID，不需要进行远程调用，延时低，性能高；  
> **缺点**：  
> 1).UUID 过长，很多场景不适用，比如用 UUID 做数据库索引字段；  
> 2).没有排序，无法保证趋势递增。  

##### 数据库自增长序列或字段

> 最常见的方式，利用数据库，全数据库唯一。  
> **优点**：  
> 1).简单，代码方便，性能可以接受；  
> 2).数字 ID 天然排序，对分页或者需要排序的结果很有帮助。  
> **缺点**：  
> 1).不同数据库语法和实现不同，数据库迁移的时候或多数据库版本支持的时候需要处理；  
> 2).在单个数据库或读写分离或一主多从的情况下，只有一个主库可以生成。有单点故障的风险；  
> 3).在性能达不到要求的情况下，比较难于扩展；  
> 4).如果遇见多个系统需要合并或者涉及到数据迁移会相当痛苦；  
> 5).分表分库的时候会有麻烦。  

##### Filcker 方法

> 主要思路采用了 MySql 自增长 ID 的机制（auto_increment + replace into）。  
> **优点**：  
> 充分借助数据库的自增 ID 机制，可靠性高，生成有序的ID；  
> **缺点**：  
> 1).ID 生成性能一般，单台数据库读写性能；  
> 2).依赖数据库，当数据库异常时整个系统不可用。  

##### Redis 生成 ID

> 主要依赖于 Redis 是单线程的，所以也可以用生成全局唯一的 ID 。可以用 Redis 的原子操作 INCR 和 INCRBY 来实现。  
> **优点**：  
> 1).不依赖与数据库，灵活方便，且性能优于数据库；
> 2).数字 ID 天然排序，对分页或者需要排序的结果很有帮助。  
> **缺点**：  
> 1).如果系统中没有 Redis ，还需要引入新的组件，增加系统复杂度；  
> 2).需要编码和配置的工作量比较大。  

##### snowflake 算法

> snowflake 是 Twitter 开源的分布式 ID 生成算法，结果是一个 long 型的 ID。其核心思想是：使用 41bit 作为毫秒数，10bit 作为机器的 ID（5个 bit 是数据中心，5个 bit 是机器 ID），12bit 作为毫秒内的流水号 （意味着每个节点在每毫秒可以产生4096个 ID），最后还有个符号位，永远是0。  
> **优点**：  
> 1).不依赖于数据库，灵活方便，且性能优于数据库；  
> 2).ID 按照时间在单机上是递增的。  
> **缺点**：  
> 在单机上是递增的，但是由于涉及到分布式环境，每台机器上的始终不可能完全同步，也许有时候也会出现不适全局递增的情况。

#### 选择合适的分布式主键方案

> 参考：  
> [分布式系统唯一ID生成方案汇总](http://www.cnblogs.com/haoxinyue/p/5208136.html)

#### 选择合适的数据存储方案

> _**关系型数据库 MySQL**_  
> MySQL 是一个最流行的关系型数据库，在互联网产品中应用比较广泛。一般情况下，MySQL 数据库是选择的第一方案，基本上有 80% ~ 90% 的场景都是基于 MySQL 数据库的。因为，需要关系型数据库进行管理，此外，业务存在许多事务性的操作，需要保证事务的强一致性。同时，可能还存在一些复杂的 SQL 的查询。值得注意的是，前期尽量减少表的联合查询，便于后期数据量增大的情况下，做数据库的分库分表。  

> _**内存数据库 Redis**_  
> 随着数据量的增长，MySQL 已经满足不了大型互联网类应用的需求。因此，Redis 基于内存存储数据，可以极大的提高查询性能，对产品在架构上很好的补充。例如，为了提高服务端接口的访问速度，尽可能将读频率高的热点数据存放在 Redis 中。这个是非常典型的以空间换时间的策略，使用更多的内存换取 CPU 资源，通过增加系统的内存消耗，来加快程序的运行速度。

> 在某些场景下，可以充分的利用 Redis 的特性，大大提高效率。这些场景包括缓存，会话缓存，时效性，访问频率，计数器，社交列表，记录用户判定信息，交集、并集和差集，热门列表与排行榜，最新动态等。

> 使用 Redis 做缓存的时候，需要考虑数据不一致与脏读、缓存更新机制、缓存可用性、缓存服务降级、缓存穿透、缓存预热等缓存使用问题。  

> _**文档数据库 MongoDB**_  
> MongoDB 是对传统关系型数据库的补充，它非常适合高伸缩性的场景，它是可扩展性的表结构。基于这点，可以将预期范围内，表结构可能会不断扩展的 MySQL 表结构，通过 MongoDB 来存储，这就可以保证表结构的扩展性。

> 此外，日志系统数据量特别大，如果用 MongoDB 数据库存储这些数据，利用分片集群支持海量数据，同时使用聚集分析和 MapReduce 的能力，是个很好的选择。  

> MongoDB 还适合存储大尺寸的数据，GridFS 存储方案就是基于 MongoDB 的分布式文件存储系统。

> _**列族数据库 HBase**_  
> HBase 适合海量数据的存储与高性能实时查询，它是运行于 HDFS 文件系统之上，并且作为 MapReduce 分布式处理的目标数据库，以支撑离线分析型应用。在数据仓库、数据集市、商业智能等领域发挥了越来越多的作用，在数以千计的企业中支撑着大量的大数据分析场景的应用。

> _**全文搜索引擎 ElasticSearch**_  
> 在一般情况下，关系型数据库的模糊查询，都是通过 like 的方式进行查询。其中，like “value%” 可以使用索引，但是对于 like “%value%” 这样的方式，执行全表查询，这在数据量小的表，不存在性能问题，但是对于海量数据，全表扫描是非常可怕的事情。ElasticSearch 作为一个建立在全文搜索引擎 Apache Lucene 基础上的实时的分布式搜索和分析引擎，适用于处理实时搜索应用场景。此外，使用 ElasticSearch 全文搜索引擎，还可以支持多词条查询、匹配度与权重、自动联想、拼写纠错等高级功能。因此，可以使用 ElasticSearch 作为关系型数据库全文搜索的功能补充，将要进行全文搜索的数据缓存一份到 ElasticSearch 上，达到处理复杂的业务与提高查询速度的目的。

> ElasticSearch 不仅仅适用于搜索场景，还非常适合日志处理与分析的场景。著名的 ELK 日志处理方案，由 ElasticSearch、Logstash 和 Kibana 三个组件组成，包括了日志收集、聚合、多维度查询、可视化显示等。

#### ObjectId 规则

> 参考：  
> [MongoDB学习笔记~ObjectId主键的设计](http://www.cnblogs.com/lori/p/4409399.html)
> [mongodb中的_id的ObjectId的生成规则](https://www.cnblogs.com/weilunhui/p/6861938.html)

#### 聊聊 MongoDB 使用场景

> 参考：    
> [什么场景应该用 MongoDB ？](https://yq.aliyun.com/articles/64352?utm_campaign=wenzhang&utm_medium=article&utm_source=QQ-qun&utm_content=m_7775)

#### 倒排索引

> 参考：  
> [什么是倒排索引？](https://www.cnblogs.com/zlslch/p/6440114.html)

#### 聊聊 ElasticSearch 使用场景

> 在一般情况下，关系型数据库的模糊查询，都是通过 like 的方式进行查询。其中，like “value%” 可以使用索引，但是对于 like “%value%” 这样的方式，执行全表查询，这在数据量小的表，不存在性能问题，但是对于海量数据，全表扫描是非常可怕的事情。ElasticSearch 作为一个建立在全文搜索引擎 Apache Lucene 基础上的实时的分布式搜索和分析引擎，适用于处理实时搜索应用场景。此外，使用 ElasticSearch 全文搜索引擎，还可以支持多词条查询、匹配度与权重、自动联想、拼写纠错等高级功能。因此，可以使用 ElasticSearch 作为关系型数据库全文搜索的功能补充，将要进行全文搜索的数据缓存一份到 ElasticSearch 上，达到处理复杂的业务与提高查询速度的目的。

### 缓存使用

#### Redis 有哪些类型

> Redis支持五种数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)。  
> 参考：  
> [Redis 数据类型](http://www.runoob.com/redis/redis-data-types.html)

#### Redis 内部结构

> 参考：  
> [redis内部数据结构深入浅出](https://www.cnblogs.com/chenpingzhao/archive/2017/06/10/6965164.html)

#### 聊聊 Redis 使用场景

> 随着数据量的增长，MySQL 已经满足不了大型互联网类应用的需求。因此，Redis 基于内存存储数据，可以极大的提高查询性能，对产品在架构上很好的补充。例如，为了提高服务端接口的访问速度，尽可能将读频率高的热点数据存放在 Redis 中。这个是非常典型的以空间换时间的策略，使用更多的内存换取 CPU 资源，通过增加系统的内存消耗，来加快程序的运行速度。

> 在某些场景下，可以充分的利用 Redis 的特性，大大提高效率。这些场景包括缓存，会话缓存，时效性，访问频率，计数器，社交列表，记录用户判定信息，交集、并集和差集，热门列表与排行榜，最新动态等。  

> 使用 Redis 做缓存的时候，需要考虑数据不一致与脏读、缓存更新机制、缓存可用性、缓存服务降级、缓存穿透、缓存预热等缓存使用问题。

#### Redis 持久化机制

> 参考：  
> [redis的持久化和缓存机制](http://blog.csdn.net/tr1912/article/details/70197085?foxhandler=RssReadRenderProcessHandler)

#### Redis 如何实现持久化

> 参考：  
> [Redis如何实现持久化](http://blog.csdn.net/u013905744/article/details/52787413)

#### Redis 集群方案与实现

> 参考：  
> [redis集群主流架构方案分析](http://blog.csdn.net/u011277123/article/details/55002024)

#### Redis 为什么是单线程的

> 单纯的网络IO来说，量大到一定程度之后，多线程的确有优势——但并不是单纯的多线程，而是每个线程自己有自己的epoll这样的模型，也就是多线程和multiplexing混合。

> 一般这个开头我们都会跟一个“但是”。
但是。

> 还要考虑Redis操作的对象。它操作的对象是内存中的数据结构。如果在多线程中操作，那就需要为这些对象加锁。最终来说，多线程性能有提高，但是每个线程的效率严重下降了。而且程序的逻辑严重复杂化。  

> 要知道Redis的数据结构并不全是简单的Key-Value，还有列表，hash，map等等复杂的结构，这些结构有可能会进行很细粒度的操作，比如在很长的列表后面添加一个元素，在hash当中添加或者删除一个对象，等等。这些操作还可以合成MULTI/EXEC的组。这样一个操作中可能就需要加非常多的锁，导致的结果是同步开销大大增加。这还带来一个恶果就是吞吐量虽然增大，但是响应延迟可能会增加。

> Redis在权衡之后的选择是用单线程，突出自己功能的灵活性。在单线程基础上任何原子操作都可以几乎无代价地实现，多么复杂的数据结构都可以轻松运用，甚至可以使用Lua脚本这样的功能。对于多线程来说这需要高得多的代价。

> 并不是所有的KV数据库或者内存数据库都应该用单线程，比如ZooKeeper就是多线程的，最终还是看作者自己的意愿和取舍。单线程的威力实际上非常强大，每核心效率也非常高，在今天的虚拟化环境当中可以充分利用云化环境来提高资源利用率。多线程自然是可以比单线程有更高的性能上限，但是在今天的计算环境中，即使是单机多线程的上限也往往不能满足需要了，需要进一步摸索的是多服务器集群化的方案，这些方案中多线程的技术照样是用不上的，所以单线程、多进程的集群不失为一个时髦的解决方案。
作者：灵剑
链接：[https://www.zhihu.com/question/23162208/answer/142424042](https://www.zhihu.com/question/23162208/answer/142424042)
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

#### 缓存奔溃

> 参考：  
> [Redis持久化](http://blog.51cto.com/harisxiong/1584795)

#### 缓存降级

> 服务降级的目的，是为了防止Redis服务故障，导致数据库跟着一起发生雪崩问题。因此，对于不重要的缓存数据，可以采取服务降级策略，例如一个比较常见的做法就是，Redis出现问题，不去数据库查询，而是直接返回默认值给用户。

#### 使用缓存的合理性问题

> 参考：  
> [Redis实战（一） 使用缓存合理性](http://blog.csdn.net/diyhzp/article/details/54892358)

### 消息队列

#### 消息队列的使用场景

> 主要解决应用耦合，异步消息，流量削锋等问题.  
> [消息队列使用的四种场景介绍](http://blog.csdn.net/seven__________7/article/details/70225830)

#### 消息的重发补偿解决思路

> 参考：  
> [JMS消息传送机制](http://blog.csdn.net/wangtaomtk/article/details/51531278)

#### 消息的幂等性解决思路

> 参考：  
> [MQ之如何做到消息幂等](https://www.jianshu.com/p/8b77d4583bab?utm_campaign)

#### 消息的堆积解决思路

> 参考：  
> [Sun Java System Message Queue 3.7 UR1 管理指南](https://docs.oracle.com/cd/E19148-01/820-0843/6nci9sed1/index.html)

#### 自己如何实现消息队列

> 参考：  
> [自己动手实现消息队列之JMS](http://blog.csdn.net/liaodehong/article/details/5241)

#### 如何保证消息的有序性

> 参考：  
> [消息队列的exclusive consumer功能是如何保证消息有序和防止脑裂的](https://yq.aliyun.com/articles/73672)

## 框架篇

### Spring

#### BeanFactory 和 ApplicationContext 有什么区别

> beanfactory顾名思义，它的核心概念就是bean工厂，用作于bean生命周期的管理，而applicationcontext这个概念就比较丰富了，单看名字（应用上下文）就能看出它包含的范围更广，它继承自bean factory但不仅仅是继承自这一个接口，还有继承了其他的接口，所以它不仅仅有bean factory相关概念，更是一个应用系统的上下文，其设计初衷应该是一个包罗万象的对外暴露的一个综合的API。

#### Spring Bean 的生命周期

> 参考：  
> [Spring Bean生命周期详解](http://blog.csdn.net/a327369238/article/details/52193822)
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/01.png)

#### Spring IOC 如何实现

> 参考：  
> [Spring：源码解读Spring IOC原理](https://www.cnblogs.com/ITtangtang/p/3978349.html)

#### 说说 Spring AOP

> 参考：  
> [Spring AOP详解](https://www.cnblogs.com/hongwz/p/5764917.html)

#### Spring AOP 实现原理

> 参考：  
> [Spring AOP 实现原理](http://blog.csdn.net/moreevan/article/details/11977115/)

#### 动态代理（cglib 与 JDK）

> java动态代理是利用反射机制生成一个实现代理接口的匿名类，在调用具体方法前调用InvokeHandler来处理。

> 而cglib动态代理是利用asm开源包，对代理对象类的class文件加载进来，通过修改其字节码生成子类来处理。

> 1、如果目标对象实现了接口，默认情况下会采用JDK的动态代理实现AOP.  
> 2、如果目标对象实现了接口，可以强制使用CGLIB实现AOP.  
> 3、如果目标对象没有实现了接口，必须采用CGLIB库，spring会自动在JDK动态代理和CGLIB之间转换.  

> 如何强制使用CGLIB实现AOP？  
> （1）添加CGLIB库，SPRING_HOME/cglib/*.jar  
> （2）在spring配置文件中加入<aop:aspectj-autoproxy proxy-target-class=“true”/>  

> JDK动态代理和CGLIB字节码生成的区别？  
> （1）JDK动态代理只能对实现了接口的类生成代理，而不能针对类.  
> （2）CGLIB是针对类实现代理，主要是对指定的类生成一个子类，覆盖其中的方法.  
> 因为是继承，所以该类或方法最好不要声明成final  
> 参考：  
> [Spring的两种代理JDK和CGLIB的区别浅谈](http://blog.csdn.net/u013126379/article/details/52121096)

#### Spring 事务实现方式

> 参考：  
> [Spring事务管理实现方式之编程式事务与声明式事务详解](http://blog.csdn.net/liaohaojian/article/details/70139151)

#### Spring 事务底层原理

> 参考：  
> [深入理解 Spring 事务原理](http://www.codeceo.com/spring-transactions.html)

#### 如何自定义注解实现功能

> 可以结合spring的AOP，对注解进行拦截，提取注解。  
> 大致流程为：  
> 1.新建一个注解@MyLog，加在需要注解申明的方法上面.  
> 2.新建一个类MyLogAspect，通过@Aspect注解使该类成为切面类。  
> 3.通过@Pointcut 指定切入点 ，这里指定的切入点为MyLog注解类型，也就是被@MyLog注解修饰的方法，进入该切入点。  
> 4.MyLogAspect中的方法通过加通知注解（@Before、@Around、@AfterReturning、@AfterThrowing、@After等各种通知）指定要做的业务操作。  

#### Spring MVC 运行流程

> **一、先用文字描述**  
> 1.用户发送请求到DispatchServlet.  
> 2.DispatchServlet根据请求路径查询具体的Handler.  
> 3.HandlerMapping返回一个HandlerExcutionChain给DispatchServlet（HandlerExcutionChain：Handler和Interceptor集合）.  
> 4.DispatchServlet调用HandlerAdapter适配器.  
> 5.HandlerAdapter调用具体的Handler处理业务.  
> 6.Handler处理结束返回一个具体的ModelAndView给适配器（ModelAndView:model–>数据模型，view–>视图名称）.  
> 7.适配器将ModelAndView给DispatchServlet.  
> 8.DispatchServlet把视图名称给ViewResolver视图解析器.  
> 9.ViewResolver返回一个具体的视图给DispatchServlet.  
> 10.渲染视图.  
> 11.展示给用户.  

> **二、画图解析**  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/02.png)

> **SpringMvc的配置**  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/03.png)

#### Spring MVC 启动流程


> 参考：  
> [SpringMVC启动过程详解（li）](https://www.cnblogs.com/RunForLove/p/5688731.html)

#### Spring 的单例实现原理

> 参考：  
> [Spring的单例模式底层实现](http://blog.csdn.net/cs408/article/details/48982085)

#### Spring 框架中用到了哪些设计模式

> **Spring框架中使用到了大量的设计模式，下面列举了比较有代表性的**：  
> 代理模式—在AOP和remoting中被用的比较多。  
> 单例模式—在spring配置文件中定义的bean默认为单例模式。  
> 模板方法—用来解决代码重复的问题。比如. RestTemplate, JmsTemplate, JpaTemplate。  
> 工厂模式—BeanFactory用来创建对象的实例。  
> 适配器–spring aop  
> 装饰器–spring data  hashmapper  
> 观察者-- spring 时间驱动模型  
> 回调–Spring ResourceLoaderAware回调接口  
> 前端控制器–spring用前端控制器DispatcherServlet对请求进行分发  

#### Spring 其他产品（Srping Boot、Spring Cloud、Spring Secuirity、Spring Data、Spring AMQP 等）

> 参考：  
> [说一说Spring家族](https://www.jianshu.com/p/b3e4aaa83a7d)

### Netty

#### 为什么选择 Netty

> Netty 是业界最流行的 NIO 框架之一，它的健壮性、功能、性能、可定制性和可扩展性在同类框架中都是首屈一指的，它已经得到成百上千的商用项目验证，例如 Hadoop 的 RPC 框架 Avro 使用 Netty 作为通信框架。很多其它业界主流的 RPC 和分布式服务框架，也使用 Netty 来构建高性能的异步通信能力。

> **Netty 的优点总结如下**：  
> 1.API 使用简单，开发门槛低；  
> 2.功能强大，预置了多种编解码功能，支持多种主流协议；  
> 3.定制能力强，可以通过 ChannelHandler 对通信框架进行灵活的扩展；  
> 4.性能高，通过与其它业界主流的 NIO 框架对比，Netty 的综合性能最优；  
> 5.社区活跃，版本迭代周期短，发现的 BUG 可以被及时修复，同时，更多的新功能会被加入；  
> 6.经历了大规模的商业应用考验，质量得到验证。在互联网、大数据、网络游戏、企业应用、电信软件等众多行业得到成功商用，证明了它完全满足不同行业的商用标准。  

> 正是因为这些优点，Netty 逐渐成为 Java NIO 编程的首选框架。

#### 说说业务中，Netty 的使用场景

> [有关“为何选择Netty”的11个疑问及解答](http://www.52im.net/thread-163-1-1.html)

#### 原生的 NIO 在 JDK 1.7 版本存在 epoll bug

> 它会导致Selector空轮询，最终导致CPU 100%。官方声称在JDK1.6版本的update18修复了该问题，但是直到JDK1.7版本该问题仍旧存在，只不过该BUG发生概率降低了一些而已，它并没有被根本解决。该BUG以及与该BUG相关的问题单可以参见以下链接内容。

> [http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6403933](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=6403933)  
> [http://bugs.java.com/bugdatabase/view_bug.do?bug_id=2147719](http://bugs.java.com/bugdatabase/view_bug.do?bug_id=2147719)

> 异常堆栈如下：

	java.lang.Thread.State: RUNNABLE  
	        at sun.nio.ch.EPollArrayWrapper.epollWait(Native Method)  
	        at sun.nio.ch.EPollArrayWrapper.poll(EPollArrayWrapper.java:210)  
	        at sun.nio.ch.EPollSelectorImpl.doSelect(EPollSelectorImpl.java:65)  
	        at sun.nio.ch.SelectorImpl.lockAndDoSelect(SelectorImpl.java:69)  
	        - locked <0x0000000750928190> (a sun.nio.ch.Util$2)  
	        - locked <0x00000007509281a8> (a java.util.Collections$ UnmodifiableSet)  
	        - locked <0x0000000750946098> (a sun.nio.ch.EPollSelectorImpl)  
	        at sun.nio.ch.SelectorImpl.select(SelectorImpl.java:80)  
	        at net.spy.memcached.MemcachedConnection.handleIO(Memcached Connection.java:217)  
	        at net.spy.memcached.MemcachedConnection.run(MemcachedConnection. java:836) 

#### 什么是TCP 粘包/拆包
> 参考：  
> [TCP粘包，拆包及解决方法](https://blog.insanecoder.top/tcp-packet-splice-and-split-issue/)

#### TCP粘包/拆包的解决办法

> 参考：  
> [TCP粘包，拆包及解决方法](https://blog.insanecoder.top/tcp-packet-splice-and-split-issue/)

#### Netty 线程模型

> 参考：  
> [Netty4实战第十五章：选择正确的线程模型](http://blog.csdn.net/wangjinnan16/article/details/78377642)

#### 说说 Netty 的零拷贝

> 参考：  
> [理解Netty中的零拷贝（Zero-Copy）机制](https://my.oschina.net/plucury/blog/192577)

#### Netty 内部执行流程

> 参考：  
> [Netty：数据处理流程](https://www.cnblogs.com/f1194361820/p/5656440.html)

#### Netty 重连实现

> 参考：  
> [Netty Client 重连实现](http://www.importnew.com/25046.html)

## 微服务篇

### 微服务

#### 前后端分离是如何做的

> 参考：  
> [实现前后端分离的心得](http://blog.jobbole.com/111624/)

#### 微服务哪些框架

> Spring Cloud、Dubbo、Hsf等.  

#### 你怎么理解 RPC 框架

> RPC的目的是让你在本地调用远程的方法，而对你来说这个调用是透明的，你并不知道这个调用的方法是部署哪里。通过RPC能解耦服务，这才是使用RPC的真正目的。

#### 说说 RPC 的实现原理

> 参考：  
> [你应该知道的 RPC 原理](http://blog.jobbole.com/92290/)  
> [从零开始实现RPC框架 - RPC原理及实现](http://blog.csdn.net/top_code/article/details/54615853)

#### 说说 Dubbo 的实现原理

> dubbo提供功能来讲， 提供基础功能-RPC调用 提供增值功能SOA服务治理.  
> dubbo启动时查找可用的远程服务提供者，调用接口时不是最终调用本地实现，而是通过拦截调用（又用上JDK动态代理功能）过程经过一系列的的序列化、远程通信、协议解析最终调用到远程服务提供者.  
> 参考：  
> [Dubbo解析及原理浅析](http://blog.csdn.net/chao_19/article/details/51764150)

#### 你怎么理解 RESTful

> REST 是一种软件架构风格、设计风格，它是一种面向资源的网络化超媒体应用的架构风格。它主要是用于构建轻量级的、可维护的、可伸缩的 Web 服务。基于 REST 的服务被称为 RESTful 服务。REST 不依赖于任何协议，但是几乎每个 RESTful 服务使用 HTTP 作为底层协议，RESTful使用http method标识操作，例如：  
[http://127.0.0.1/user/1]() GET  根据用户id查询用户数据.  
[http://127.0.0.1/user]()  POST 新增用户.  
[http://127.0.0.1/user]()  PUT 修改用户信息.  
[http://127.0.0.1/user]()  DELETE 删除用户信息.  

![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_01/04.png)

#### 说说如何设计一个良好的 API

> 参考：  
> [如何设计一个良好的API?](http://www.jdon.com/48452)

#### 如何理解 RESTful API 的幂等性

> 参考：  
> [如何理解RESTful的幂等性](http://blog.csdn.net/garfielder007/article/details/55684420)

#### 如何保证接口的幂等性

> 参考：  
> [后端接口的幂等性](http://blog.csdn.net/jks456/article/details/71453053)

#### 说说 CAP 定理、 BASE 理论

> 参考：  
> [CAP原理和BASE思想](http://www.jdon.com/37625)

#### 怎么考虑数据一致性问题

> 参考：  
> [分布式系统事务一致性解决方案](http://www.infoq.com/cn/articles/solution-of-distributed-system-transaction-consistency)

#### 说说最终一致性的实现方案

> 可以结合MQ实现最终一致性，例如电商系统，把生成订单数据的写操作逻辑通过事务控制，一些无关紧要的业务例如日志处理，通知，通过异步消息处理，最终到请求落地。  
> 参考：  
> [系统分布式情况下最终一致性方案梳理](http://iamzhongyong.iteye.com/blog/2240891)

#### 你怎么看待微服务

> 小：微服务体积小.  
> 独：能够独立的部署和运行。  
> 轻：使用轻量级的通信机制和架构。  
> 松：各服务之间是松耦合的。  

#### 微服务与 SOA 的区别

> 可以把微服务当做去除了ESB的SOA。ESB是SOA架构中的中心总线，设计图形应该是星形的，而微服务是去中心化的分布式软件架构。  
> 参考：  
> [SOA 与 微服务的区别](https://www.cnblogs.com/ynuo/p/5913955.html)

#### 如何拆分服务

> 参考：  
> [微服务架构(二): 如何把应用分解成多个服务](http://blog.csdn.net/u012422829/article/details/68951579?utm_source=itdadao&utm_medium=referral)

### 微服务如何进行数据库管理

> 参考：  
> [在微服务中如何管理数据](http://www.infoq.com/cn/news/2017/07/managing-data-in-microservices)

#### 如何应对微服务的链式调用异常

> 参考：  
> [踢开绊脚石：微服务难点之服务调用的解决方案](https://segmentfault.com/a/1190000011578125)

#### 对于快速追踪与定位问题

> 参考：  
> [微服务架构下，如何实现分布式跟踪？](http://www.infoq.com/cn/articles/how-to-realize-distributed-tracking/)

#### 微服务的安全

> 参考：  
> [论微服务安全](https://segmentfault.com/a/1190000005891501)

### 分布式

#### 谈谈业务中使用分布式的场景

##### 一、解决java集群的session共享的解决方案：

> 1.客户端cookie加密。（一般用于内网中企业级的系统中，要求用户浏览器端的cookie不能禁用，禁用的话，该方案会失效）。  
> 2.集群中，各个应用服务器提供了session复制的功能，tomcat 和 jboss 都实现了这样的功能。<font color=blue>特点：性能随着服务器增加急剧下降，容易引起广播风暴；</font> session 数据需要序列化，影响性能。  
> 3.session的持久化，使用数据库来保存session。就算服务器宕机也没事儿，数据库中的session照样存在。<font color=blue>特点：每次请求session都要读写数据库，会带来性能开销。</font>使用内存数据库，会提高性能，但是宕机会丢失数据(像支付宝的宕机，有同城灾备、异地灾备)。  
> 4.使用共享存储来保存 session。和数据库类似，就算宕机了也没有事儿。其实就是专门搞一台服务器，全部对session落地。<font color=blue>特点：频繁的进行序列化和反序列化会影响性能。</font>  
> 5.使用memcached来保存session。本质上是内存数据库的解决方案。<font color=blue>特点：存入memcached的数据需要序列化，效率极低。</font>  

##### 二、分布式事务的解决方案:

> 1.TCC解决方案：try confirm cancel。  
> 参考：  
> [为什么说传统分布式事务不再适用于微服务架构？](http://blog.csdn.net/jek123456/article/details/54666545)

#### Session 分布式方案

> 1.客户端cookie加密。（一般用于内网中企业级的系统中，要求用户浏览器端的cookie不能禁用，禁用的话，该方案会失效）。  
> 2.集群中，各个应用服务器提供了session复制的功能，tomcat和jboss都实现了这样的功能。特点：性能随着服务器增加急剧下降，容易引起广播风暴；session数据需要序列化，影响性能。  
> 3.session的持久化，使用数据库来保存session。就算服务器宕机也没事儿，数据库中的session照样存在。特点：每次请求session都要读写数据库，会带来性能开销。使用内存数据库，会提高性能，但是宕机会丢失数据(像支付宝的宕机，有同城灾备、异地灾备)。  
> 4.使用共享存储来保存session。和数据库类似，就算宕机了也没有事儿。其实就是专门搞一台服务器，全部对session落地。特点：频繁的进行序列化和反序列化会影响性能。  
> 5.使用memcached来保存session。本质上是内存数据库的解决方案。特点：存入memcached的数据需要序列化，效率极低。  

#### 分布式锁的场景

> 比如交易系统的金额修改，同一时间只能又一个人操作，比如秒杀场景，同一时间只能一个用户抢到，比如火车站抢票等等.  

#### 分布式锁的实现方案

> 1.基于数据库实现分布式锁.  
> 2.基于缓存实现分布式锁.  
> 3.基于Zookeeper实现分布式锁.  

> 参考：  
> [分布式锁的多种实现方式](https://www.cnblogs.com/yuyutianxia/p/7149363.html)

#### 分布式事务

> 参考：  
> [深入理解分布式事务,高并发下分布式事务的解决方案](http://blog.csdn.net/mine_song/article/details/64118963)

#### 集群与负载均衡的算法与实现

> 参考：  
> [负载均衡算法及手段](https://www.cnblogs.com/data2value/p/6107450.html)

#### 说说分库与分表设计

> 参考：  
> [分表与分库使用场景以及设计方式](http://blog.csdn.net/winy_lm/article/details/50708493)

#### 分库与分表带来的分布式困境与应对之策

> 参考：  
> [服务端指南 数据存储篇 | MySQL（09） 分库与分表带来的分布式困境与应对之策](http://blog.720ui.com/2017/mysql_core_09_multi_db_table2/)

## 安全&性能

### 安全问题

#### 安全要素与 STRIDE 威胁

> 参考：  
> [http://blog.720ui.com/2017/security_stride/](http://blog.720ui.com/2017/security_stride/)

#### 防范常见的 Web 攻击

##### XSS攻击

> **跨站脚本攻击**  
> _是什么_：攻击者向有XSS漏洞的网站中输入恶意的HTML代码，当其浏览器浏览该网站时，这段HTML代码会自- - 动执行。（理论上所有可以输入的地方没有对输入的数据进行处理，都会存在XSS攻击）;  
> _危害_： 盗取用户cookie，破坏页面结构，重定向到其他网站;  
> _防御_：对用户输入的信息进行处理，只允许合法的值;  

##### CSRF攻击
> **跨站请求伪造**  
> _是什么_：攻击者盗用了你的身份，以你的名义发送恶意请求;  
> _危害_：以你的名义发送邮件，盗取帐号，购买东西等;  
> _原理_： 首先个登录某网站，并在本地生成cookie;然后在不登出的情况下，访问危害网站。  
> _防御_： 可以从服务端和客户端两方面进行考虑。但是在服务端的效果好。  
> 1).随机的cookie。 
> 2).添加验证码。  
> 3).不同的表单包含一个不同的伪随机值。  
> _注意_：如果用户在一个站点上同时打开了两个不同的表单。CSRF保护措施不应该影响到他对任何表单的提交   

##### SQL注入
> _是什么_：通过sql命令伪装成正常的http请求参数，传递到服务端，服务器执行sql命令造成对数据库进行攻击.  
> _原理_：sql语句伪造参数，然后在对参数机型拼接后形成破坏性的sql语句，最后导致数据库收到攻击.  
> _防御_：  
> 1).对参数进行转义.  
> 2).数据库中的密码不应明文存储，可以对密码使用md5进行加密。  

##### DDOS攻击（分布式拒绝服务攻击）
> _是什么_：简单来说就是ifasong大量的请求使服务器瘫痪。  
> _被攻击的原因_：服务器带宽不足，不能挡住攻击者的攻击流量。  
> _防御_：  
> 1).最直接的方法就是增加带宽;  
> 2).使用硬件防火墙;  
> 3).优化资源使用提高 web server 的负载能力.  

> 来源：[https://blog.csdn.net/wen_special/article/details/80461394](https://blog.csdn.net/wen_special/article/details/80461394)  

#### 服务端通信安全攻防

##### Base64加密传输
> Base64是网络上最常见的用于传输8Bit字节代码的编码方式之一，但是它其实并不是一种用于安全领域的加密解密算法。

> 但是，Base64编码的数据并不会被人用肉眼所直观的理解，所以也有人使用Base64来进行加密解密，这里所说的加密与解密实际是指编码和解码的过程。

> 这种，加密传输的安全性是非常低的，Base64加密非常容易被人识别并解码。

##### DES对称加密
> DES也是一种非常常用的加密方案，我们会将敏感的信息在通信过程中通过DES进行加密传输，然后在客户端和服务端直接进行解码。

> 此时，作为读者的你，可能会有个疑问，那如何保管密钥呢？其实，想想，答案就复出水面了，因为客户端和服务端都需要进行解码，所以两者都要存一份密钥。其实，还有一种方案是通过服务端下发，但是下发的时候通信的安全性也是没有很好的保障。

> 所以，DES对称加密也是存在一定的安全隐患：密钥可能会泄漏。这边，举个真实的案例，某个APP的资源不错，同事想抓包分析下其服务端通信的信息结构，但是发现它既然全部采用了DES加密方案，本来想放弃了，但是我们又回头想想客户端肯定需要密钥对接口的加密的内容做解码才能正常展现，那么密钥肯定在app包中，因此我们又对app进行了反编译，结果成功的获取到了密钥，对服务端通信的加密信息进行了解码。

##### AES对称加密
> AES和DES类似，相较于DES算法而言，AES算法有着更高的速度和资源使用效率，安全级别也较之更高。一般情况下，用于文件的加密。我们之前做个不准确测试，AES和DES分别对一个大文件加密，AES的速度大概是DES的5倍。（因为基于工具和环境问题，这个数据不是很准确哟）。

> 仍然存在一个相同的问题：密钥可能会泄漏。因此，保管好密钥很关键。

##### 升级到HTTPS
> 这个可以参考上篇博客《HTTPS原理剖析与项目场景》的内容。

> _HTTPS的价值在于_：  
> 1).内容加密，第三方无法窃听。  
> 2).身份认证，一旦被篡改，通信双方会立刻发现。  
> 3).数据完整性。防止内容冒充或者篡改。  

> 这个方案，没法保护敏感数据，如果需要对敏感数据进行加密，还是需要考虑加密方案。

##### URL签名
> 基于OAuth2协议，进行URL签名。这个方案，有很多话题可以分享，后面另开一篇来详细讲解。
值得注意的是，URL签名只能垂直权限管理，但没法保护敏感数据，如果需要对敏感数据进行保护，还是需要考虑加密方案。

##### 双向RSA加密
> RSA双向认证，就是用对方的公钥加密是为了保密，这个只有对方用私钥能解密。用自己的私钥加密是为了防抵赖，能用我的公钥解开，说明这是我发来的。

> 例如，支付宝的支付接口就是非常典型的RSA双向认证的安全方案。此外，我们之前的教育资源、敏感验证码出于安全性考虑都借鉴了这个方案。  
> 来源：[http://blog.720ui.com/2016/security_data_transmission/](http://blog.720ui.com/2016/security_data_transmission/)

#### HTTPS 原理剖析

> 参考：[https://www.cnblogs.com/zery/p/5164795.html](https://www.cnblogs.com/zery/p/5164795.html)

#### HTTPS 降级攻击

> 参考：[http://blog.720ui.com/2016/security_https_tls/](http://blog.720ui.com/2016/security_https_tls/)

#### 授权与认证

> 参考：[https://blog.csdn.net/gdp12315_gu/article/details/79905424](https://blog.csdn.net/gdp12315_gu/article/details/79905424)

#### 基于角色的访问控制

> 参考：[https://blog.csdn.net/yin767833376/article/details/64907383](https://blog.csdn.net/yin767833376/article/details/64907383)

#### 基于数据的访问控制

> 基于角色的访问控制，只验证访问数据的角色，但是没有对角色内的用户做细分。举个例子，用户甲与用户乙都具有同一个角色，但是如果只建立基于角色的访问控制，那么用户甲可以对用户乙的数据进行任意操作，从而发生了越权访问。因此，在业务场景中仅仅使用基于角色的访问控制是不够的，还需要引入基于数据的访问控制。如果将基于角色的访问控制视为一种垂直权限控制，那么，基于数据的访问控制就是一种水平权限控制。在业务场景中，往往对基于数据的访问控制不够重视，举个例子，评论功能是一个非常常见的功能，用户可以在客户端发起评论，回复评论，查看评论，删除评论等操作。一般情况下，只有本人才可以删除自己的评论，如果此时，业务层面没有建立数据的访问控制，那么用户甲可以试图绕过客户端，通过调用服务端RESTful API 接口，猜测评论 ID 并修改评论 ID 就可以删除别人的评论。事实上，这是非常严重的越权操作。除此之外，用户之间往往也存在一些私有的数据，而这些私有的数据在正常情况下，只有用户自己才能访问。

> 基于数据的访问控制，需要业务层面去处理，但是这个也是最为经常遗落的安全点，需要引起重视。这里，再次使用删除评论的案例，通过 Java 语言进行介绍。在这个案例中，核心的代码片段在于，判断当前用户是否是评论的创建者，如果是则通过，不是则报出没有权限的错误码。那么，这样就可以很好地防止数据的越权操作。

	@RestController
	@RequestMapping(value = {"/v1/c/apps"})
	public class AppCommentController{
	    @Autowired
	    private AppCommentService appCommentService;
	 
	    @RequestMapping(value = "/{appId:\\d+}/comments/{commentId:\\d+}”, method = RequestMethod.DELETE)
	    public void deleteAppCommentInfo(@PathVariable Long appId, @PathVariable Long commentId, @AuthenticationPrincipal UserInfo userInfo) {
	        AppComment appComment = this.appCommentService.checkCommentInfo(commentId);
	 
	        // 判断当前用户是否是评论的创建者，如果是则通过，不是则报出没有权限的错误码。
	        if(!appComment.getUserId().equals(Long.valueOf(userInfo.getUserId()))){
	            throw new BusinessException(ErrorCode.ACCESS_DENIED);
	        }
	 
	        this.appCommentService.delete(commentId);
	    }
	}

> 总结下，基于角色的访问控制是一种垂直权限控制，通过建立用户与角色的对应关系，使得不同角色之间具有高低之分。用户根据拥有的角色进行操作与资源访问。基于数据的访问控制是一种水平权限控制，它对角色内的用户做细分，确保用户的数据不能越权操作。基于数据的访问控制，需要业务层面去处理，但是这个也是最为经常遗落的安全点，需要引起重视。

### 性能优化

#### 性能指标有哪些

> **1．响应时间（Response time）**  
> 响应时间就是用户感受软件系统为其服务所耗费的时间，对于网站系统来说，响应时间就是从点击了一个页面计时开始，到这个页面完全在浏览器里展现计时结束的这一段时间间隔，看起来很简单，但其实在这段响应时间内，软件系统在幕后经过了一系列的处理工作，贯穿了整个系统节点。根据“管辖区域”不同，响应时间可以细分为：  
> （1）服务器端响应时间，这个时间指的是服务器完成交易请求执行的时间，不包括客户端到服务器端的反应（请求和耗费在网络上的通信时间），这个服务器端响应时间可以度量服务器的处理能力。  
> （2）网络响应时间，这是网络硬件传输交易请求和交易结果所耗费的时间。  
> （3）客户端响应时间，这是客户端在构建请求和展现交易结果时所耗费的时间，对于普通的瘦客户端Web应用来说，这个时间很短，通常可以忽略不计；但是对于胖客户端Web应用来说，比如Java applet、AJAX，由于客户端内嵌了大量的逻辑处理，耗费的时间有可能很长，从而成为系统的瓶颈，这是要注意的一个地方。  

> 那么客户感受的响应时间其实是等于客户端响应时间+服务器端响应时间+网络响应时间。细分的目的是为了方便定位性能瓶颈出现在哪个节点上（何为性能瓶颈，下一节中介绍）。

> **2．吞吐量（Throughput）**  
> 吞吐量是我们常见的一个软件性能指标，对于软件系统来说，“吞”进去的是请求，“吐”出来的是结果，而吞吐量反映的就是软件系统的“饭量”，也就是系统的处理能力，具体说来，就是指软件系统在每单位时间内能处理多少个事务/请求/单位数据等。但它的定义比较灵活，在不同的场景下有不同的诠释，比如数据库的吞吐量指的是单位时间内，不同SQL语句的执行数量；而网络的吞吐量指的是单位时间内在网络上传输的数据流量。吞吐量的大小由负载（如用户的数量）或行为方式来决定。举个例子，下载文件比浏览网页需要更高的网络吞吐量。  

> **3．资源使用率（Resource utilization）**  
> 常见的资源有：CPU占用率、内存使用率、磁盘I/O、网络I/O。  
> 我们将在Analysis结果分析一章中详细介绍如何理解和分析这些指标。  

> **4．点击数（Hits per second）**  
> 点击数是衡量Web Server处理能力的一个很有用的指标。需要明确的是：点击数不是我们通常理解的用户鼠标点击次数，而是按照客户端向Web Server发起了多少次http请求计算的，一次鼠标可能触发多个http请求，这需要结合具体的Web系统实现来计算。

> **5．并发用户数（Concurrent users）**  
> 并发用户数用来度量服务器并发容量和同步协调能力。在客户端，指：<font color=blue>一批用户同时执行一个操作。</font> 并发数反映了软件系统的并发处理能力，和吞吐量不同的是，它大多是占用套接字、句柄等操作系统资源。  

> 另外，度量软件系统的性能指标还有系统恢复时间等，其实凡是用户有关资源和时间的要求都可以被视作性能指标，都可以作为软件系统的度量，而性能测试就是为了验证这些性能指标是否被满足。  
> 参考：[https://www.douban.com/note/168911628/](https://www.douban.com/note/168911628/)  

#### 如何发现性能瓶颈

> 参考：[https://www.testwo.com/blog/8207](https://www.testwo.com/blog/8207)

#### 性能调优的常见手段

> **1.尽量在合适的场合使用单例**  
> 使用单例可以减轻加载的负担，缩短加载的时间，提高加载的效率，但并不是所有地方都适用于单例，简单来说，单例主要适用于以下三个方面：  
> 第一，控制资源的使用，通过线程同步来控制资源的并发访问；  
> 第二，控制实例的产生，以达到节约资源的目的；  
> 第三，控制数据共享，在不建立直接关联的条件下，让多个不相关的进程或线程之间实现通信。  

> **2.尽量避免随意使用静态变量**  
> 要知道，当某个对象被定义为stataic变量所引用，那么gc通常是不会回收这个对象所占有的内存，如:  

	public class A{
	    static B b = new B();
	}
	
> 此时静态变量b的生命周期与A类同步，如果A类不会卸载，那么b对象会常驻内存，直到程序终止。

> **3.尽量避免过多过常的创建Java对象**  
> 尽量避免在经常调用的方法，循环中new对象，由于系统不仅要花费时间来创建对象，而且还要花时间对这些对象进行垃圾回收和处理，在我们可以控制的范围内，最大限度的重用对象，最好能用基本的数据类型或数组来替代对象。

> **4.尽量使用final修饰符**  
> 带有final修饰符的类是不可派生的。在Java核心API中，有许多应用final的例子，例如java.lang.String。为String类指定final防止了使用者覆盖length()方法。另外，如果一个类是final的，则该类所有方法都是final的。Java编译器会寻找机会内联（inline）所有的final方法（这和具体的编译器实现有关）。此举能够使性能平均提高50%。  

> **5.尽量使用局部变量**  
> 调用方法时传递的参数以及在调用中创建的临时变量都保存在栈（Stack）中，速度较快。其他变量，如静态变量、实例变量等，都在堆（Heap）中创建，速度较慢。

> **6.尽量处理好包装类型和基本类型两者的使用场所**  
> 虽然包装类型和基本类型在使用过程中是可以相互转换，但它们两者所产生的内存区域是完全不同的，基本类型数据产生和处理都在栈中处理，包装类型是对象，是在堆中产生实例。  
> 在集合类对象，有对象方面需要的处理适用包装类型，其他的处理提倡使用基本类型。  

> **7.慎用synchronized，尽量减小synchronize的方法**  
> 都知道，实现同步是要很大的系统开销作为代价的，甚至可能造成死锁，所以尽量避免无谓的同步控制。synchronize方法被调用时，直接会把当前对象锁了，在方法执行完之前其他线程无法调用当前对象的其他方法。所以synchronize的方法尽量小，并且应尽量使用方法同步代替代码块同步。  
> 使用synchronized关键字并不一定都是锁定当前对象的，要看具体的锁是什么。如果是在方法上加的synchronized，则是以对象本身为锁的，如果是静态方法则锁的粒度是类。

> **8.尽量使用StringBuilder和StringBuffer进行字符串连接**  
> 这个就不多讲了。

> **9.尽量不要使用finalize方法**  
> 实际上，将资源清理放在finalize方法中完成是非常不好的选择，由于GC的工作量很大，尤其是回收Young代内存时，大都会引起应用程序暂停，所以再选择使用finalize方法进行资源清理，会导致GC负担更大，程序运行效率更差。

> **10.尽量使用基本数据类型代替对象**  
	
	String str = “hello”;
	
> 上面这种方式会创建一个“hello”字符串，而且JVM的字符缓存池还会缓存这个字符串；

	String str = new String(“hello”);

> 此时程序除创建字符串外，str所引用的String对象底层还包含一个char[]数组，这个char[]数组依次存放了h,e,l,l,o

> **11.单线程应尽量使用HashMap、ArrayList**  
> HashTable、Vector等使用了同步机制，降低了性能。

> **12.尽量合理的创建HashMap**  
> 当你要创建一个比较大的hashMap时，充分利用另一个构造函数:  

	public HashMap(int initialCapacity, float loadFactor);
	
> 避免HashMap多次进行了hash重构,扩容是一件很耗费性能的事，在默认中: <font color=blue> initialCapacity 只有16 </font>，而 <font color=blue> loadFactor 是 0.75 </font>，需要多大的容量，你最好能准确的估计你所需要的最佳大小，同样的 Hashtable，Vectors 也是一样的道理。

> **13.尽量减少对变量的重复计算**  
> 如：  

	for(int i=0;i<list.size();i++)
> 应该改为：  

	for(int i=0,len=list.size();i<len;i++)

> 并且在循环中应该避免使用复杂的表达式，在循环中，循环条件会被反复计算，如果不使用复杂表达式，而使循环条件值不变的话，程序将会运行的更快。

> **14.尽量避免不必要的创建**  
> 如：  
	
	A a = new A();
	if(i==1){
	    list.add(a);
	}
> 应该改为：  
	
	if(i==1){
	    A a = new A();
	    list.add(a);
	}

> **15.尽量在finally块中释放资源**  
> 程序中使用到的资源应当被释放，以避免资源泄漏。这最好在finally块中去做。不管程序执行的结果如何(try的时候线程不挂掉)，finally块总是会执行的，以确保资源的正确关闭。

> **16.尽量使用移位来代替’a/b’的操作**  
> "/"是一个代价很高的操作，使用移位的操作将会更快和更有效  
> 如：  
	
	int num = a / 4;
	int num = a / 8;
> 应该改为：  
	
	int num = a >> 2;
	int num = a >> 3;
> 但注意的是使用移位应添加注释，因为移位操作不直观，比较难理解  

> **17.尽量使用移位来代替’a*b’的操作**  
> 同样的，对于’*'操作，使用移位的操作将会更快和更有效。 
> 如：  
	
	int num = a * 4;
	int num = a * 8;
> 应该改为：  
	
	int num = a << 2;
	int num = a << 3;

> **18.尽量确定StringBuffer的容量**  
> StringBuffer 的构造器会创建一个默认大小（通常是16）的字符数组。在使用中，如果超出这个大小，就会重新分配内存，创建一个更大的数组，并将原先的数组复制过来，再丢弃旧的数组。在大多数情况下，你可以在创建 StringBuffer的时候指定大小，这样就避免了在容量不够的时候自动增长，以提高性能。  
> 如：  
	
	StringBuffer buffer = new StringBuffer(1000);

> **19.尽量早释放无用对象的引用**  
> 大部分时，方法局部引用变量所引用的对象 会随着方法结束而变成垃圾，因此，大部分时候程序无需将局部、引用变量显式设为null。  
> 例如：  

	Public void test(){
	    Object obj = new Object();
	    ……
	    Obj=null;
	}
> 上面这个就没必要了，随着方法test()的执行完成，程序中obj引用变量的作用域就结束了。但是如果是改成下面：  

	Public void test(){
	    Object obj = new Object();
	    ……
	    Obj=null;
	    //执行耗时，耗内存操作；或调用耗时，耗内存的方法
	    ……
	}
> 这时候就有必要将obj赋值为null，可以尽早的释放对Object对象的引用。  
> 但是如果 Object obj = new Object(); 如果这对象并不是大对象，这有必要吗？Obj=null;只是告诉jvm这个对象已经成为垃圾，至于什么时候回收，还不能确定！ 这可读性也不好！

> **20.尽量避免使用二维数组**  
> 二维数组占用的内存空间比一维数组多得多，大概10倍以上。  

> **21.尽量避免使用split**  
> 除非是必须的，否则应该避免使用split，split由于支持正则表达式，所以效率比较低，如果是频繁的几十，几百万的调用将会耗费大量资源，如果确实需要频繁的调用split，可以考虑使用apache的StringUtils.split(string,char)，频繁split的可以缓存结果。  

> **22.ArrayList & LinkedList**  
> 一个是线性表，一个是链表，一句话，随机查询尽量使用ArrayList，ArrayList优于LinkedList，LinkedList还要移动指针，添加删除的操作LinkedList优于ArrayList，ArrayList还要移动数据，不过这是理论性分析，事实未必如此，重要的是理解好两者的数据结构，对症下药。

> **23.尽量使用System.arraycopy()代替通过循环来复制数组**  
> System.arraycopy() 要比通过循环来复制数组快的多。 

> **24.尽量缓存经常使用的对象**  
> 尽可能将经常使用的对象进行缓存，可以使用数组或 HashMap 的容器来进行缓存，但这种方式可能导致系统占用过多的缓存，性能下降，推荐可以使用一些第三方的开源工具，如：EhCache，Oscache 进行缓存，他们基本都实现了FIFO/FLU等缓存算法。

> **25.尽量避免非常大的内存分配**  
> 有时候问题不是由当时的堆状态造成的，而是因为分配失败造成的。分配的内存块都必须是连续的，而随着堆越来越满，找到较大的连续块越来越困难。

> **26.慎用异常**  
> 当创建一个异常时，需要收集一个栈跟踪(stack track)，这个栈跟踪用于描述异常是在何处创建的。构建这些栈跟踪时需要为运行时栈做一份快照，正是这一部分开销很大。当需要创建一个 Exception 时，JVM 不得不说：先别动，我想就您现在的样子存一份快照，所以暂时停止入栈和出栈操作。栈跟踪不只包含运行时栈中的一两个元素，而是包含这个栈中的每一个元素。  
> 如果您创建一个 Exception ，就得付出代价。好在捕获异常开销不大，因此可以使用 try-catch 将核心内容包起来。从技术上讲，您甚至可以随意地抛出异常，而不用花费很大的代价。招致性能损失的并不是 throw 操作---尽管在没有预先创建异常的情况下就抛出异常是有点不寻常。真正要花代价的是创建异常。幸运的是，好的编程习惯已教会我们，不应该不管三七二十一就抛出异常。异常是为异常的情况而设计的，使用时也应该牢记这一原则。

#### 说说你在项目中如何进行性能调优

> 1.尽量使用缓存，这里不是指的比如ORM框架 Hibernate 的一级缓存和二级缓存，而是独立的缓存服务器，它是存储于内存中的；比如用户缓存，基本配置信息缓存等，它一般是在系统中经常要查的一些信息，在这里我们可以使用缓存，我们项目中常用的比如redis，memcache。这样可以大量减少与数据库的交互，提高性能。  

> 2.统计的功能尽量做缓存，或按每天一统计或定时统计相关报表，避免需要时进行实时统计的功能。

> 3.能使用静态页面的地方尽量使用，减少容器的解析（尽量将动态内容生成静态html来显示）。  

> 4.对于一个系统内如果有过多图片加载显示时我们最好设计成用一台单独的服务器来存储，这样就会减少应用服务器的压力，提高性能；如果用了负载均衡更是弥补了图片不能同步的问题。

> 5.可以对WEB容器进行优化，开发中我们常用的有tomcat，weblogic 对于WEB容器我们要考虑的有JVM的使用率、空闲线程数、队列长度和吞吐量这些方面，所以我们加大内存使用率 调整线程数的值可以提高系统性能。  

> 6.优化数据库查询语句，比如尽量不要用通配符 * ；少用 in 和 not in ；where条件内尽量不要用 != / <> 这样会导致放弃使用索引。  

> 7.优化数据库结构，多做索引，主键尽量不要用自增的，减少冗余字段，提高查询效率。对于大数据量我们还可以进表拆分 ORACLE 超过100W条查询效率就会很慢。  

> 8.负载均衡，我们常用的并发能力较强的前置代理服务器比如 nginx、apache 这里 nginx 并发量是高于 apache 的 它可以实现动静分离、反向代理，而且体积相对来说较小。

> 9.采用多台服务器集群的方式来解决单台的瓶颈问题。 

> 10.分布式部署：我们把不同的应用部署在不同的服务器，运用相关机制统一调度所有的应用程序，这样就可以提高系统性能也解决了单存储服务器的瓶颈问题。  

## 工程篇

### 需求分析

#### 你如何对需求原型进行理解和拆分

#### 说说你对功能性需求的理解

#### 说说你对非功能性需求的理解

#### 你针对产品提出哪些交互和改进意见

#### 你如何理解用户痛点

### 设计能力

#### 说说你在项目中使用过的 UML 图

#### 你如何考虑组件化

#### 你如何考虑服务化

#### 你如何进行领域建模

#### 你如何划分领域边界

#### 说说你项目中的领域建模

#### 说说概要设计

### 设计模式

#### 你项目中有使用哪些设计模式

#### 说说常用开源框架中设计模式使用分析

#### 说说你对设计原则的理解

#### 23种设计模式的设计理念

#### 设计模式之间的异同，例如策略模式与状态模式的区别

#### 设计模式之间的结合，例如策略模式+简单工厂模式的实践

#### 设计模式的性能，例如单例模式哪种性能更好。

### 业务工程

#### 你系统中的前后端分离是如何做的

#### 说说你的开发流程

#### 你和团队是如何沟通的

#### 你如何进行代码评审

#### 说说你对技术与业务的理解

#### 说说你在项目中经常遇到的 Exception

#### 说说你在项目中遇到感觉最难Bug，怎么解决的

#### 说说你在项目中遇到印象最深困难，怎么解决的

#### 你觉得你们项目还有哪些不足的地方

#### 你是否遇到过 CPU 100% ，如何排查与解决

#### 你是否遇到过 内存 OOM ，如何排查与解决

#### 说说你对敏捷开发的实践

#### 说说你对开发运维的实践

#### 介绍下工作中的一个对自己最有价值的项目，以及在这个过程中的角色

### 软实力

#### 说说你的亮点

#### 说说你最近在看什么书

#### 说说你觉得最有意义的技术书籍

#### 工作之余做什么事情

#### 说说个人发展方向方面的思考

#### 说说你认为的服务端开发工程师应该具备哪些能力

#### 说说你认为的架构师是什么样的，架构师主要做什么

#### 说说你所理解的技术专家















