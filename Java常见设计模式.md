# Java常见设计模式

> 文章参考资料来源：[RUNOOB.COM](http://www.runoob.com/design-pattern/design-pattern-tutorial.html)。本文仅用作自主学习资料积累，不另作他用！

+ **设计模式简介：**

> 设计模式（Design pattern）代表了最佳的实践，通常被有经验的面向对象的软件开发人员所采用。设计模式是软件开发人员在软件开发过程中面临的一般问题的解决方案。这些解决方案是众多软件开发人员经过相当长的一段时间的试验和错误总结出来的。

> 设计模式是一套被反复使用的、多数人知晓的、经过分类编目的、代码设计经验的总结。使用设计模式是为了重用代码、让代码更容易被他人理解、保证代码可靠性。 毫无疑问，设计模式于己于他人于系统都是多赢的，设计模式使代码编制真正工程化，设计模式是软件工程的基石，如同大厦的一块块砖石一样。项目中合理地运用设计模式可以完美地解决很多问题，每种模式在现实中都有相应的原理来与之对应，每种模式都描述了一个在我们周围不断重复发生的问题，以及该问题的核心解决方案，这也是设计模式能被广泛应用的原因。

+ **设计模式六大原则**

>**1、开闭原则（Open Close Principle）**  
开闭原则的意思是：对扩展开放，对修改关闭。在程序需要进行拓展的时候，不能去修改原有的代码，实现一个热插拔的效果。简言之，是为了使程序的扩展性好，易于维护和升级。想要达到这样的效果，我们需要使用接口和抽象类，后面的具体设计中我们会提到这点。

>**2、里氏代换原则（Liskov Substitution Principle）**  
里氏代换原则是面向对象设计的基本原则之一。 里氏代换原则中说，任何基类可以出现的地方，子类一定可以出现。LSP 是继承复用的基石，只有当派生类可以替换掉基类，且软件单位的功能不受到影响时，基类才能真正被复用，而派生类也能够在基类的基础上增加新的行为。里氏代换原则是对开闭原则的补充。实现开闭原则的关键步骤就是抽象化，而基类与子类的继承关系就是抽象化的具体实现，所以里氏代换原则是对实现抽象化的具体步骤的规范。

>**3、依赖倒转原则（Dependence Inversion Principle）**  
这个原则是开闭原则的基础，具体内容：针对接口编程，依赖于抽象而不依赖于具体。

>**4、接口隔离原则（Interface Segregation Principle）**  
这个原则的意思是：使用多个隔离的接口，比使用单个接口要好。它还有另外一个意思是：降低类之间的耦合度。由此可见，其实设计模式就是从大型软件架构出发、便于升级和维护的软件设计思想，它强调降低依赖，降低耦合。

>**5、迪米特法则，又称最少知道原则（Demeter Principle）**  
最少知道原则是指：一个实体应当尽量少地与其他实体之间发生相互作用，使得系统功能模块相对独立。

>**6、合成复用原则（Composite Reuse Principle）**  
合成复用原则是指：尽量使用合成/聚合的方式，而不是使用继承。

+ **设计模式之间的关系：**
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/01.jpg)

<!--目录结构-->

[toc]


## 一、创建型模式（Creational Patterns
> 这些设计模式提供了一种在创建对象的同时隐藏创建逻辑的方式，而不是使用 new 运算符直接实例化对象。这使得程序在判断针对某个给定实例需要创建哪些对象时更加灵活。

### 1.1 单利模式（Singleton Pattern）
>单例模式（Singleton Pattern）是 Java 中最简单的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。
 这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。这个类提供了一种访问其唯一的对象的方式，可以直接访问，不需要实例化该类的对象。
 
>注意：

> 1、单例类只能有一个实例。<br>
 2、单例类必须自己创建自己的唯一实例。<br>
 3、单例类必须给所有其他对象提供这一实例。<br>

>**_介绍_**

>**意图：**保证一个类仅有一个实例，并提供一个访问它的全局访问点。  
**主要解决：**一个全局使用的类频繁地创建与销毁。  
**何时使用：**当您想控制实例数目，节省系统资源的时候。  
**如何解决：**判断系统是否已经有这个单例，如果有则返回，如果没有则创建。  
**关键代码：**构造函数是私有的。  
>**应用实例：**  
>1、一个班级只有一个班主任。  
>2、Windows 是多进程多线程的，在操作一个文件的时候，就不可避免地出现多个进程或线程同时操作一个文件的现象，所以所有文件的处理必须通过唯一的实例来进行。  
>3、一些设备管理器常常设计为单例模式，比如一个电脑有两台打印机，在输出的时候就要处理不能两台打印机打印同一个文件。  
>**优点：**  
>1、在内存里只有一个实例，减少了内存的开销，尤其是频繁的创建和销毁实例（比如管理学院首页页面缓存）。  
>2、避免对资源的多重占用（比如写文件操作）。  
>**缺点：**  
>没有接口，不能继承，与单一职责原则冲突，一个类应该只关心内部逻辑，而不关心外面怎么样来实例化。  
>**使用场景：**  
>1、要求生产唯一序列号。  
>2、WEB 中的计数器，不用每次刷新都在数据库里加一次，用单例先缓存起来。  
>3、创建的一个对象需要消耗的资源过多，比如 I/O 与数据库的连接等。  
>**注意事项：** getInstance() 方法中需要使用同步锁 synchronized (Singleton.class) 防止多线程同时进入造成 instance 被多次实例化。  

>**_实现_**

>我们将创建一个 SingleObject 类。SingleObject 类有它的私有构造函数和本身的一个静态实例。
SingleObject 类提供了一个静态方法，供外界获取它的静态实例。SingletonPatternDemo，我们的演示类使用 SingleObject 类来获取 SingleObject 对象。
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/02.jpg)

>**_步骤 1_**  
> 创建一个 Singleton 类。

    SingleObject.java
    public class SingleObject {
     
       //创建 SingleObject 的一个对象
       private static SingleObject instance = new SingleObject();
     
       //让构造函数为 private，这样该类就不会被实例化
       private SingleObject(){}
     
       //获取唯一可用的对象
       public static SingleObject getInstance(){
          return instance;
       }
     
       public void showMessage(){
          System.out.println("Hello World!");
       }
    }
    
>**_步骤 2_**  
> 从 singleton 类获取唯一的对象。

    SingletonPatternDemo.java
    public class SingletonPatternDemo {
       public static void main(String[] args) {
     
          //不合法的构造函数
          //编译时错误：构造函数 SingleObject() 是不可见的
          //SingleObject object = new SingleObject();
     
          //获取唯一可用的对象
          SingleObject object = SingleObject.getInstance();
     
          //显示消息
          object.showMessage();
       }
    }
    
>**_步骤 3_**  
> 执行程序，输出结果：

    Hello World!

>**_*单例模式的几种实现方式*_**

>单例模式的实现有多种方式，如下所示：

>**_1、懒汉式，线程不安全_**

>**是否 Lazy 初始化：是**

>**是否多线程安全：否**

>**实现难度：易**

>描述：这种方式是最基本的实现方式，这种实现最大的问题就是不支持多线程。因为没有加锁 synchronized，所以严格意义上它并不算单例模式。  
这种方式 lazy loading 很明显，不要求线程安全，在多线程不能正常工作。

>**实例**

    public class Singleton {  
        private static Singleton instance;  
        private Singleton (){}  
      
        public static Singleton getInstance() {  
	        if (instance == null) {  
	            instance = new Singleton();  
	        }  
	        return instance;  
        }  
    }
    
>接下来介绍的几种实现方式都支持多线程，但是在性能上有所差异。

>**_2、懒汉式，线程安全_**

> **是否 Lazy 初始化：是**

> **是否多线程安全：是**

> **实现难度：易**

> 描述：这种方式具备很好的 lazy loading，能够在多线程中很好的工作，但是，效率很低，99% 情况下不需要同步。  
> 优点：第一次调用才初始化，避免内存浪费。  
> 缺点：必须加锁 synchronized 才能保证单例，但加锁会影响效率。  
>getInstance() 的性能对应用程序不是很关键（该方法使用不太频繁）。

> **实例**

	public class Singleton {  
	    private static Singleton instance;  
	    private Singleton (){}  
	    public static synchronized Singleton getInstance() {  
		    if (instance == null) {  
		        instance = new Singleton();  
		    }  
		    return instance;  
	    }  
	}
	
> **_3、饿汉式_**

> **是否 Lazy 初始化：否**

> **是否多线程安全：是**

> **实现难度：易**

> 描述：这种方式比较常用，但容易产生垃圾对象。
> 优点：没有加锁，执行效率会提高。
> 缺点：类加载时就初始化，浪费内存。
> 它基于 classloader 机制避免了多线程的同步问题，不过，instance 在类装载时就实例化，虽然导致类装载的原因有很多种，在单例模式中大多数都是调用 getInstance 方法， 但是也不能确定有其他的方式（或者其他的静态方法）导致类装载，这时候初始化 instance 显然没有达到 lazy loading 的效果。

> **实例**
	
	public class Singleton {  
	    private static Singleton instance = new Singleton();  
	    private Singleton (){}  
	    public static Singleton getInstance() {  
	    	return instance;  
	    }  
	}
	
> **_4、双检锁/双重校验锁（DCL，即 double-checked locking）_**

> **JDK 版本：JDK1.5 起**

> **是否 Lazy 初始化：是**

> **是否多线程安全：是**

> **实现难度：较复杂**

>描述：这种方式采用双锁机制，安全且在多线程情况下能保持高性能。  
>getInstance() 的性能对应用程序很关键。

> **实例**
	
	public class Singleton {  
	    private volatile static Singleton singleton;  
	    private Singleton (){}  
	    public static Singleton getSingleton() {  
		    if (singleton == null) {  
		        synchronized (Singleton.class) {  
			        if (singleton == null) {  
			            singleton = new Singleton();  
			        }  
		        }  
		    }  
	    	return singleton;  
	    }  
	}
	
> **_5、登记式/静态内部类_**

> **是否 Lazy 初始化：是**

> **是否多线程安全：是**

> **实现难度：一般**

>描述：这种方式能达到双检锁方式一样的功效，但实现更简单。对静态域使用延迟初始化，应使用这种方式而不是双检锁方式。这种方式只适用于静态域的情况，双检锁方式可在实例域需要延迟初始化时使用。
这种方式同样利用了 classloader 机制来保证初始化 instance 时只有一个线程，它跟第 3 种方式不同的是：第 3 种方式只要 Singleton 类被装载了，那么 instance 就会被实例化（没有达到 lazy loading 效果），而这种方式是 Singleton 类被装载了，instance 不一定被初始化。因为 SingletonHolder 类没有被主动使用，只有通过显式调用 getInstance 方法时，才会显式装载 SingletonHolder 类，从而实例化 instance。想象一下，如果实例化 instance 很消耗资源，所以想让它延迟加载，另外一方面，又不希望在 Singleton 类加载时就实例化，因为不能确保 Singleton 类还可能在其他的地方被主动使用从而被加载，那么这个时候实例化 instance 显然是不合适的。这个时候，这种方式相比第 3 种方式就显得很合理。

> **实例**

	public class Singleton {  
	    private static class SingletonHolder {  
	    	 private static final Singleton INSTANCE = new Singleton();  
	    }  
	    private Singleton (){}  
	    public static final Singleton getInstance() {  
	    	 return SingletonHolder.INSTANCE;  
	    }  
	}
	
> **_6、枚举_**

> **JDK 版本：JDK1.5 起**

> **是否 Lazy 初始化：否**

> **是否多线程安全：是**

> **实现难度：易**

> 描述：这种实现方式还没有被广泛采用，但这是实现单例模式的最佳方法。它更简洁，自动支持序列化机制，绝对防止多次实例化。
这种方式是 Effective Java 作者 Josh Bloch 提倡的方式，它不仅能避免多线程同步问题，而且还自动支持序列化机制，防止反序列化重新创建新的对象，绝对防止多次实例化。不过，由于 JDK1.5 之后才加入 enum 特性，用这种方式写不免让人感觉生疏，在实际工作中，也很少用。
不能通过 reflection attack 来调用私有构造方法。

> **实例**

	public enum Singleton {  
	    INSTANCE;  
	    public void whateverMethod() {  
	    }  
	}
	
> **经验之谈：**一般情况下，不建议使用第 1 种和第 2 种懒汉方式，建议使用第 3 种饿汉方式。只有在要明确实现 lazy loading 效果时，才会使用第 5 种登记方式。如果涉及到反序列化创建对象时，可以尝试使用第 6 种枚举方式。如果有其他特殊的需求，可以考虑使用第 4 种双检锁方式。

### 1.2 工厂方法模式（Factory Pattern）
> 工厂模式（Factory Pattern）是 Java 中最常用的设计模式之一。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。  
> 在工厂模式中，我们在创建对象时不会对客户端暴露创建逻辑，并且是通过使用一个共同的接口来指向新创建的对象。

> **_介绍_**

> **意图：**定义一个创建对象的接口，让其子类自己决定实例化哪一个工厂类，工厂模式使其创建过程延迟到子类进行。  
> **主要解决：**主要解决接口选择的问题。  
> **何时使用：**我们明确地计划不同条件下创建不同实例时。  
> **如何解决：**让其子类实现工厂接口，返回的也是一个抽象的产品。  
> **关键代码：**创建过程在其子类执行。  
> **应用实例：**  
> 1、您需要一辆汽车，可以直接从工厂里面提货，而不用去管这辆汽车是怎么做出来的，以及这个汽车里面的具体实现。   
> 2、Hibernate 换数据库只需换方言和驱动就可以。  
> **优点：**   
> 1、一个调用者想创建一个对象，只要知道其名称就可以了。  
> 2、扩展性高，如果想增加一个产品，只要扩展一个工厂类就可以。  
> 3、屏蔽产品的具体实现，调用者只关心产品的接口。  
> **缺点：**  
> 每次增加一个产品时，都需要增加一个具体类和对象实现工厂，使得系统中类的个数成倍增加，在一定程度上增加了系统的复杂度，同时也增加了系统具体类的依赖。这并不是什么好事。  
> **使用场景：**  
> 1、日志记录器：记录可能记录到本地硬盘、系统事件、远程服务器等，用户可以选择记录日志到什么地方。  
> 2、数据库访问，当用户不知道最后系统采用哪一类数据库，以及数据库可能有变化时。  
> 3、设计一个连接服务器的框架，需要三个协议，"POP3"、"IMAP"、"HTTP"，可以把这三个作为产品类，共同实现一个接口。  
> **注意事项：**  
> 作为一种创建类模式，在任何需要生成复杂对象的地方，都可以使用工厂方法模式。有一点需要注意的地方就是复杂对象适合使用工厂模式，而简单对象，特别是只需要通过 new 就可以完成创建的对象，无需使用工厂模式。如果使用工厂模式，就需要引入一个工厂类，会增加系统的复杂度。

> **_实现_**  
> 我们将创建一个 Shape 接口和实现 Shape 接口的实体类。下一步是定义工厂类 ShapeFactory。

> FactoryPatternDemo，我们的演示类使用 ShapeFactory 来获取 Shape 对象。它将向 ShapeFactory 传递信息（CIRCLE / RECTANGLE / SQUARE），以便获取它所需对象的类型。

> 工厂模式的 UML 图
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/03.jpg)

> **_步骤 1_**  
> 创建一个接口:

	Shape.java
	public interface Shape {
	   void draw();
	}
	
> **_步骤 2_**  
> 创建实现接口的实体类。

	Rectangle.java
	public class Rectangle implements Shape {
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Rectangle::draw() method.");
	   }
	}
	
	Square.java
	public class Square implements Shape {
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Square::draw() method.");
	   }
	}
	
	Circle.java
	public class Circle implements Shape {
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Circle::draw() method.");
	   }
	}
	
> **_步骤 3_**  
> 创建一个工厂，生成基于给定信息的实体类的对象。

	ShapeFactory.java
	public class ShapeFactory {
	    
	   //使用 getShape 方法获取形状类型的对象
	   public Shape getShape(String shapeType){
	      if(shapeType == null){
	         return null;
	      }        
	      if(shapeType.equalsIgnoreCase("CIRCLE")){
	         return new Circle();
	      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
	         return new Rectangle();
	      } else if(shapeType.equalsIgnoreCase("SQUARE")){
	         return new Square();
	      }
	      return null;
	   }
	}
	
> **_步骤 4_**  
> 使用该工厂，通过传递类型信息来获取实体类的对象。

	FactoryPatternDemo.java
	public class FactoryPatternDemo {
	 
	   public static void main(String[] args) {
	      ShapeFactory shapeFactory = new ShapeFactory();
	 
	      //获取 Circle 的对象，并调用它的 draw 方法
	      Shape shape1 = shapeFactory.getShape("CIRCLE");
	 
	      //调用 Circle 的 draw 方法
	      shape1.draw();
	 
	      //获取 Rectangle 的对象，并调用它的 draw 方法
	      Shape shape2 = shapeFactory.getShape("RECTANGLE");
	 
	      //调用 Rectangle 的 draw 方法
	      shape2.draw();
	 
	      //获取 Square 的对象，并调用它的 draw 方法
	      Shape shape3 = shapeFactory.getShape("SQUARE");
	 
	      //调用 Square 的 draw 方法
	      shape3.draw();
	   }
	}
	
> **_步骤 5_**  
> 执行程序，输出结果：

	Inside Circle::draw() method.
	Inside Rectangle::draw() method.
	Inside Square::draw() method.

### 1.3 抽象工厂模式（Abstract Factory Pattern）

> 抽象工厂模式（Abstract Factory Pattern）是围绕一个超级工厂创建其他工厂。该超级工厂又称为其他工厂的工厂。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。

> 在抽象工厂模式中，接口是负责创建一个相关对象的工厂，不需要显式指定它们的类。每个生成的工厂都能按照工厂模式提供对象。

> **_介绍_**  

> **意图：**提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类。  
> **主要解决：**主要解决接口选择的问题。  
> **何时使用：**系统的产品有多于一个的产品族，而系统只消费其中某一族的产品。  
> **如何解决：**在一个产品族里面，定义多个产品。  
> **关键代码：**在一个工厂里聚合多个同类产品。  
> **应用实例：**  
> 工作了，为了参加一些聚会，肯定有两套或多套衣服吧，比如说有商务装（成套，一系列具体产品）、时尚装（成套，一系列具体产品），甚至对于一个家庭来说，可能有商务女装、商务男装、时尚女装、时尚男装，这些也都是成套的，即一系列具体产品。假设一种情况（现实中是不存在的，要不然，没法进入共产主义了，但有利于说明抽象工厂模式），在您的家中，某一个衣柜（具体工厂）只能存放某一种这样的衣服（成套，一系列具体产品），每次拿这种成套的衣服时也自然要从这个衣柜中取出了。用 OO 的思想去理解，所有的衣柜（具体工厂）都是衣柜类的（抽象工厂）某一个，而每一件成套的衣服又包括具体的上衣（某一具体产品），裤子（某一具体产品），这些具体的上衣其实也都是上衣（抽象产品），具体的裤子也都是裤子（另一个抽象产品）。  
> **优点：**  
> 当一个产品族中的多个对象被设计成一起工作时，它能保证客户端始终只使用同一个产品族中的对象。  
> **缺点：**  
> 产品族扩展非常困难，要增加一个系列的某一产品，既要在抽象的 Creator 里加代码，又要在具体的里面加代码。  
> **使用场景：**  
> 1、QQ 换皮肤，一整套一起换。  
> 2、生成不同操作系统的程序。  
> **注意事项：**  
> 产品族难扩展，产品等级易扩展。

**_实现_**  
> 我们将创建 Shape 和 Color 接口和实现这些接口的实体类。下一步是创建抽象工厂类 AbstractFactory。接着定义工厂类 ShapeFactory 和 ColorFactory，这两个工厂类都是扩展了 AbstractFactory。然后创建一个工厂创造器/生成器类 FactoryProducer。

> AbstractFactoryPatternDemo，我们的演示类使用 FactoryProducer 来获取 AbstractFactory 对象。它将向 AbstractFactory 传递形状信息 Shape（CIRCLE / RECTANGLE / SQUARE），以便获取它所需对象的类型。同时它还向 AbstractFactory 传递颜色信息 Color（RED / GREEN / BLUE），以便获取它所需对象的类型。

> 抽象工厂模式的 UML 图
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/04.jpg)

> **_步骤 1_**  
> 为形状创建一个接口。

	Shape.java
	public interface Shape {
	   void draw();
	}

> **_步骤 2_**  
> 创建实现接口的实体类。
	
	Rectangle.java
	
	Rectangle.java
	public class Rectangle implements Shape {
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Rectangle::draw() method.");
	   }
	}
	Square.java
	public class Square implements Shape {
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Square::draw() method.");
	   }
	}
	Circle.java
	public class Circle implements Shape {
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Circle::draw() method.");
	   }
	}

> **_步骤 3_**  
> 为颜色创建一个接口。

	Color.java
	public interface Color {
	   void fill();
	}

> **_步骤4_**  
> 创建实现接口的实体类。
	
	Red.java
	public class Red implements Color {
	 
	   @Override
	   public void fill() {
	      System.out.println("Inside Red::fill() method.");
	   }
	}
	
	Green.java
	public class Green implements Color {
	 
	   @Override
	   public void fill() {
	      System.out.println("Inside Green::fill() method.");
	   }
	}
	
	Blue.java
	public class Blue implements Color {
	 
		@Override
	   public void fill() {
	      System.out.println("Inside Blue::fill() method.");
	   }
	}

> **_步骤 5_**  
> 为 Color 和 Shape 对象创建抽象类来获取工厂。

	AbstractFactory.java
	public abstract class AbstractFactory {
	   public abstract Color getColor(String color);
	   public abstract Shape getShape(String shape) ;
	}

> **_步骤 6_**  
> 创建扩展了 AbstractFactory 的工厂类，基于给定的信息生成实体类的对象。
	
	ShapeFactory.java
	public class ShapeFactory extends AbstractFactory {
	    
	   @Override
	   public Shape getShape(String shapeType){
	      if(shapeType == null){
	         return null;
	      }        
	      if(shapeType.equalsIgnoreCase("CIRCLE")){
	         return new Circle();
	      } else if(shapeType.equalsIgnoreCase("RECTANGLE")){
	         return new Rectangle();
	      } else if(shapeType.equalsIgnoreCase("SQUARE")){
	         return new Square();
	      }
	      return null;
	   }
	   
	   @Override
	   public Color getColor(String color) {
	      return null;
	   }
	}
	
	ColorFactory.java
	public class ColorFactory extends AbstractFactory {
	    
	   @Override
	   public Shape getShape(String shapeType){
	      return null;
	   }
	   
	   @Override
	   public Color getColor(String color) {
	      if(color == null){
	         return null;
	      }        
	      if(color.equalsIgnoreCase("RED")){
	         return new Red();
	      } else if(color.equalsIgnoreCase("GREEN")){
	         return new Green();
	      } else if(color.equalsIgnoreCase("BLUE")){
	         return new Blue();
	      }
	      return null;
	   }
	}

> **_步骤 7_**  
> 创建一个工厂创造器/生成器类，通过传递形状或颜色信息来获取工厂。
	
	FactoryProducer.java
	public class FactoryProducer {
	   public static AbstractFactory getFactory(String choice){
	      if(choice.equalsIgnoreCase("SHAPE")){
	         return new ShapeFactory();
	      } else if(choice.equalsIgnoreCase("COLOR")){
	         return new ColorFactory();
	      }
	      return null;
	   }
	}

> **_步骤 8_**  
> 使用 FactoryProducer 来获取 AbstractFactory，通过传递类型信息来获取实体类的对象。

	AbstractFactoryPatternDemo.java
	public class AbstractFactoryPatternDemo {
	   public static void main(String[] args) {
	 
	      //获取形状工厂
	      AbstractFactory shapeFactory = FactoryProducer.getFactory("SHAPE");
	 
	      //获取形状为 Circle 的对象
	      Shape shape1 = shapeFactory.getShape("CIRCLE");
	 
	      //调用 Circle 的 draw 方法
	      shape1.draw();
	 
	      //获取形状为 Rectangle 的对象
	      Shape shape2 = shapeFactory.getShape("RECTANGLE");
	 
	      //调用 Rectangle 的 draw 方法
	      shape2.draw();
	      
	      //获取形状为 Square 的对象
	      Shape shape3 = shapeFactory.getShape("SQUARE");
	 
	      //调用 Square 的 draw 方法
	      shape3.draw();
	 
	      //获取颜色工厂
	      AbstractFactory colorFactory = FactoryProducer.getFactory("COLOR");
	 
	      //获取颜色为 Red 的对象
	      Color color1 = colorFactory.getColor("RED");
	 
	      //调用 Red 的 fill 方法
	      color1.fill();
	 
	      //获取颜色为 Green 的对象
	      Color color2 = colorFactory.getColor("Green");
	 
	      //调用 Green 的 fill 方法
	      color2.fill();
	 
	      //获取颜色为 Blue 的对象
	      Color color3 = colorFactory.getColor("BLUE");
	 
	      //调用 Blue 的 fill 方法
	      color3.fill();
	   }
	}
	
> **_步骤 9_**  
> 执行程序，输出结果：

	Inside Circle::draw() method.
	Inside Rectangle::draw() method.
	Inside Square::draw() method.
	Inside Red::fill() method.
	Inside Green::fill() method.
	Inside Blue::fill() method.

> **_看完还不明白？_**  
> 下面例子中鼠标，键盘，耳麦为产品，惠普，戴尔为工厂。

> **简单工厂模式**
> 简单工厂模式不是 23 种里的一种，简而言之，就是有一个专门生产某个产品的类。  
> 比如下图中的鼠标工厂，专业生产鼠标，给参数 0，生产戴尔鼠标，给参数 1，生产惠普鼠标。
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/05.png)

> **工厂模式**
> 工厂模式也就是鼠标工厂是个父类，有生产鼠标这个接口。  
> 戴尔鼠标工厂，惠普鼠标工厂继承它，可以分别生产戴尔鼠标，惠普鼠标。  
> 生产哪种鼠标不再由参数决定，而是创建鼠标工厂时，由戴尔鼠标工厂创建。  
> 后续直接调用鼠标工厂.生产鼠标()即可  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/06.png)

> **抽象工厂模式**
> 抽象工厂模式也就是不仅生产鼠标，同时生产键盘。  
> 也就是 PC 厂商是个父类，有生产鼠标，生产键盘两个接口。  
> 戴尔工厂，惠普工厂继承它，可以分别生产戴尔鼠标+戴尔键盘，和惠普鼠标+惠普键盘。  
> 创建工厂时，由戴尔工厂创建。  
> 后续工厂.生产鼠标()则生产戴尔鼠标，工厂.生产键盘()则生产戴尔键盘。  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/07.png)

> _在抽象工厂模式中，假设我们需要增加一个工厂_

> 假设我们增加华硕工厂，则我们需要增加华硕工厂，和戴尔工厂一样，继承 PC 厂商。  
> 之后创建华硕鼠标，继承鼠标类。创建华硕键盘，继承键盘类即可。  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/08.png)

> _在抽象工厂模式中，假设我们需要增加一个产品_

> 假设我们增加耳麦这个产品，则首先我们需要增加耳麦这个父类，再加上戴尔耳麦，惠普耳麦这两个子类。  
> 之后在PC厂商这个父类中，增加生产耳麦的接口。最后在戴尔工厂，惠普工厂这两个类中，分别实现生产戴尔耳麦，惠普耳麦的功能。 以上。  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/09.png)


### 1.4 建造者模式（Builder Pattern）

> 建造者模式（Builder Pattern）使用多个简单的对象一步一步构建成一个复杂的对象。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。
> 一个 Builder 类会一步一步构造最终的对象。该 Builder 类是独立于其他对象的。

> **_介绍_**  
> **意图：**将一个复杂的构建与其表示相分离，使得同样的构建过程可以创建不同的表示。  
> **主要解决：**主要解决在软件系统中，有时候面临着"一个复杂对象"的创建工作，其通常由各个部分的子对象用一定的算法构成；由于需求的变化，这个复杂对象的各个部分经常面临着剧烈的变化，但是将它们组合在一起的算法却相对稳定。  
> **何时使用：**一些基本部件不会变，而其组合经常变化的时候。  
> **如何解决：**将变与不变分离开。  
> **关键代码：**建造者：创建和提供实例，导演：管理建造出来的实例的依赖关系。  
> **应用实例：**  
> 1、去肯德基，汉堡、可乐、薯条、炸鸡翅等是不变的，而其组合是经常变化的，生成出所谓的"套餐"。  
> 2、JAVA 中的 StringBuilder。  
> **优点：**  
> 1、建造者独立，易扩展。  
> 2、便于控制细节风险。  
> **缺点：**  
> 1、产品必须有共同点，范围有限制。  
> 2、如内部变化复杂，会有很多的建造类。  
> **使用场景：**  
> 1、需要生成的对象具有复杂的内部结构。  
> 2、需要生成的对象内部属性本身相互依赖。  
> **注意事项：**  
> 与工厂模式的区别是：建造者模式更加关注与零件装配的顺序。

> **_实现_**  
> 我们假设一个快餐店的商业案例，其中，一个典型的套餐可以是一个汉堡（Burger）和一杯冷饮（Cold drink）。汉堡（Burger）可以是素食汉堡（Veg Burger）或鸡肉汉堡（Chicken Burger），它们是包在纸盒中。冷饮（Cold drink）可以是可口可乐（coke）或百事可乐（pepsi），它们是装在瓶子中。  
> 我们将创建一个表示食物条目（比如汉堡和冷饮）的 Item 接口和实现 Item 接口的实体类，以及一个表示食物包装的 Packing 接口和实现 Packing 接口的实体类，汉堡是包在纸盒中，冷饮是装在瓶子中。  
> 然后我们创建一个 Meal 类，带有 Item 的 ArrayList 和一个通过结合 Item 来创建不同类型的 Meal 对象的 MealBuilder。BuilderPatternDemo，我们的演示类使用 MealBuilder 来创建一个 Meal。

> 建造者模式的 UML 图
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/10.jpg)

> **_步骤 1_**  
> 创建一个表示食物条目和食物包装的接口。

	Item.java
	public interface Item {
	   public String name();
	   public Packing packing();
	   public float price();    
	}
	
	Packing.java
	public interface Packing {
	   public String pack();
	}

> **_步骤 2_**  
> 创建实现 Packing 接口的实体类。

	Wrapper.java
	public class Wrapper implements Packing {
	 
	   @Override
	   public String pack() {
	      return "Wrapper";
	   }
	}
	
	Bottle.java
	public class Bottle implements Packing {
	 
	   @Override
	   public String pack() {
	      return "Bottle";
	   }
	}

> **_步骤 3_**  
> 创建实现 Item 接口的抽象类，该类提供了默认的功能。

	Burger.java
	public abstract class Burger implements Item {
	 
	   @Override
	   public Packing packing() {
	      return new Wrapper();
	   }
	 
	   @Override
	   public abstract float price();
	}
	
	ColdDrink.java
	public abstract class ColdDrink implements Item {
	 
	    @Override
	    public Packing packing() {
	       return new Bottle();
	    }
	 
	    @Override
	    public abstract float price();
	}

> **_步骤 4_**  
> 创建扩展了 Burger 和 ColdDrink 的实体类。
	
	VegBurger.java
	public class VegBurger extends Burger {
	 
	   @Override
	   public float price() {
	      return 25.0f;
	   }
	 
	   @Override
	   public String name() {
	      return "Veg Burger";
	   }
	}
	
	ChickenBurger.java
	public class ChickenBurger extends Burger {
	 
	   @Override
	   public float price() {
	      return 50.5f;
	   }
	 
	   @Override
	   public String name() {
	      return "Chicken Burger";
	   }
	}
	
	Coke.java
	public class Coke extends ColdDrink {
	 
	   @Override
	   public float price() {
	      return 30.0f;
	   }
	 
	   @Override
	   public String name() {
	      return "Coke";
	   }
	}
	
	Pepsi.java
	public class Pepsi extends ColdDrink {
	 
	   @Override
	   public float price() {
	      return 35.0f;
	   }
	 
	   @Override
	   public String name() {
	      return "Pepsi";
	   }
	}

> **_步骤 5_**  
> 创建一个 Meal 类，带有上面定义的 Item 对象。
	
	Meal.java
	import java.util.ArrayList;
	import java.util.List;
	 
	public class Meal {
	   private List<Item> items = new ArrayList<Item>();    
	 
	   public void addItem(Item item){
	      items.add(item);
	   }
	 
	   public float getCost(){
	      float cost = 0.0f;
	      for (Item item : items) {
	         cost += item.price();
	      }        
	      return cost;
	   }
	 
	   public void showItems(){
	      for (Item item : items) {
	         System.out.print("Item : "+item.name());
	         System.out.print(", Packing : "+item.packing().pack());
	         System.out.println(", Price : "+item.price());
	      }        
	   }    
	}

> **_步骤 6_**  
> 创建一个 MealBuilder 类，实际的 builder 类负责创建 Meal 对象。

	MealBuilder.java
	public class MealBuilder {
	 
	   public Meal prepareVegMeal (){
	      Meal meal = new Meal();
	      meal.addItem(new VegBurger());
	      meal.addItem(new Coke());
	      return meal;
	   }   
	 
	   public Meal prepareNonVegMeal (){
	      Meal meal = new Meal();
	      meal.addItem(new ChickenBurger());
	      meal.addItem(new Pepsi());
	      return meal;
	   }
	}

> **_步骤 7_**  
> BuiderPatternDemo 使用 MealBuider 来演示建造者模式（Builder Pattern）。

	BuilderPatternDemo.java
	public class BuilderPatternDemo {
	   public static void main(String[] args) {
	      MealBuilder mealBuilder = new MealBuilder();
	 
	      Meal vegMeal = mealBuilder.prepareVegMeal();
	      System.out.println("Veg Meal");
	      vegMeal.showItems();
	      System.out.println("Total Cost: " +vegMeal.getCost());
	 
	      Meal nonVegMeal = mealBuilder.prepareNonVegMeal();
	      System.out.println("\n\nNon-Veg Meal");
	      nonVegMeal.showItems();
	      System.out.println("Total Cost: " +nonVegMeal.getCost());
	   }
	}

> **_步骤 8_**  
> 执行程序，输出结果：

	Veg Meal
	Item : Veg Burger, Packing : Wrapper, Price : 25.0
	Item : Coke, Packing : Bottle, Price : 30.0
	Total Cost: 55.0
	
	
	Non-Veg Meal
	Item : Chicken Burger, Packing : Wrapper, Price : 50.5
	Item : Pepsi, Packing : Bottle, Price : 35.0
	Total Cost: 85.5

### 1.5 原型模式（Prototype Pattern）

> 原型模式（Prototype Pattern）是用于创建重复的对象，同时又能保证性能。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。  
> 这种模式是实现了一个原型接口，该接口用于创建当前对象的克隆。当直接创建对象的代价比较大时，则采用这种模式。例如，一个对象需要在一个高代价的数据库操作之后被创建。我们可以缓存该对象，在下一个请求时返回它的克隆，在需要的时候更新数据库，以此来减少数据库调用。  

> **_介绍_**  
> **意图：**用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。  
> **主要解决：**在运行期建立和删除原型。  

> **何时使用：**  
> 1、当一个系统应该独立于它的产品创建，构成和表示时。  
> 2、当要实例化的类是在运行时刻指定时，例如，通过动态装载。  
> 3、为了避免创建一个与产品类层次平行的工厂类层次时。  
> 4、当一个类的实例只能有几个不同状态组合中的一种时,建立相应数目的原型并克隆它们可能比每次用合适的状态手工实例化该类更方便一些。  
> **如何解决：**利用已有的一个原型对象，快速地生成和原型对象一样的实例。  

> **关键代码：**  
> 1、实现克隆操作，在 JAVA 继承 Cloneable，重写 clone()，在 .NET 中可以使用 Object 类的 MemberwiseClone() 方法来实现对象的浅拷贝或通过序列化的方式来实现深拷贝。  
> 2、原型模式同样用于隔离类对象的使用者和具体类型（易变类）之间的耦合关系，它同样要求这些"易变类"拥有稳定的接口。  
> **应用实例：**  
> 1、细胞分裂。  
> 2、JAVA 中的 Object clone() 方法。  
> **优点：**  
> 1、性能提高。  
> 2、逃避构造函数的约束。  
> **缺点：**  
1、配备克隆方法需要对类的功能进行通盘考虑，这对于全新的类不是很难，但对于已有的类不一定很容易，特别当一个类引用不支持串行化的间接对象，或者引用含有循环结构的时候。  
2、必须实现 Cloneable 接口。  
> **使用场景：**  
> 1、资源优化场景。  
> 2、类初始化需要消化非常多的资源，这个资源包括数据、硬件资源等。  
> 3、性能和安全要求的场景。  
> 4、通过 new 产生一个对象需要非常繁琐的数据准备或访问权限，则可以使用原型模式。  
> 5、一个对象多个修改者的场景。  
> 6、一个对象需要提供给其他对象访问，而且各个调用者可能都需要修改其值时，可以考虑使用原型模式拷贝多个对象供调用者使用。   
> 7、在实际项目中，原型模式很少单独出现，一般是和工厂方法模式一起出现，通过 clone 的方法创建一个对象，然后由工厂方法提供给调用者。原型模式已经与 Java 融为浑然一体，大家可以随手拿来使用。  
> **注意事项：**与通过对一个类进行实例化来构造新对象不同的是，原型模式是通过拷贝一个现有对象生成新对象的。浅拷贝实现 Cloneable，重写，深拷贝是通过实现 Serializable 读取二进制流。

> **_实现_**  
> 我们将创建一个抽象类 Shape 和扩展了 Shape 类的实体类。下一步是定义类 ShapeCache，该类把 shape 对象存储在一个 Hashtable 中，并在请求的时候返回它们的克隆。  
> PrototypePatternDemo，我们的演示类使用 ShapeCache 类来获取 Shape 对象。  

> 原型模式的 UML 图
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/11.jpg)

> **_步骤 1_**  
> 创建一个实现了 Cloneable 接口的抽象类。

	Shape.java
	public abstract class Shape implements Cloneable {
	   
	   private String id;
	   protected String type;
	   
	   abstract void draw();
	   
	   public String getType(){
	      return type;
	   }
	   
	   public String getId() {
	      return id;
	   }
	   
	   public void setId(String id) {
	      this.id = id;
	   }
	   
	   public Object clone() {
	      Object clone = null;
	      try {
	         clone = super.clone();
	      } catch (CloneNotSupportedException e) {
	         e.printStackTrace();
	      }
	      return clone;
	   }
	}

> **_步骤 2_**  
> 创建扩展了上面抽象类的实体类。

	Rectangle.java
	public class Rectangle extends Shape {
	 
	   public Rectangle(){
	     type = "Rectangle";
	   }
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Rectangle::draw() method.");
	   }
	}
	
	Square.java
	public class Square extends Shape {
	 
	   public Square(){
	     type = "Square";
	   }
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Square::draw() method.");
	   }
	}
	
	Circle.java
	public class Circle extends Shape {
	 
	   public Circle(){
	     type = "Circle";
	   }
	 
	   @Override
	   public void draw() {
	      System.out.println("Inside Circle::draw() method.");
	   }
	}

> **_步骤 3_**  
> 创建一个类，从数据库获取实体类，并把它们存储在一个 Hashtable 中。

	ShapeCache.java
	import java.util.Hashtable;
	 
	public class ShapeCache {
	    
	   private static Hashtable<String, Shape> shapeMap 
	      = new Hashtable<String, Shape>();
	 
	   public static Shape getShape(String shapeId) {
	      Shape cachedShape = shapeMap.get(shapeId);
	      return (Shape) cachedShape.clone();
	   }
	 
	   // 对每种形状都运行数据库查询，并创建该形状
	   // shapeMap.put(shapeKey, shape);
	   // 例如，我们要添加三种形状
	   public static void loadCache() {
	      Circle circle = new Circle();
	      circle.setId("1");
	      shapeMap.put(circle.getId(),circle);
	 
	      Square square = new Square();
	      square.setId("2");
	      shapeMap.put(square.getId(),square);
	 
	      Rectangle rectangle = new Rectangle();
	      rectangle.setId("3");
	      shapeMap.put(rectangle.getId(),rectangle);
	   }
	}

> **_步骤 4_**  
> PrototypePatternDemo 使用 ShapeCache 类来获取存储在 Hashtable 中的形状的克隆。

	PrototypePatternDemo.java
	public class PrototypePatternDemo {
	   public static void main(String[] args) {
	      ShapeCache.loadCache();
	 
	      Shape clonedShape = (Shape) ShapeCache.getShape("1");
	      System.out.println("Shape : " + clonedShape.getType());        
	 
	      Shape clonedShape2 = (Shape) ShapeCache.getShape("2");
	      System.out.println("Shape : " + clonedShape2.getType());        
	 
	      Shape clonedShape3 = (Shape) ShapeCache.getShape("3");
	      System.out.println("Shape : " + clonedShape3.getType());        
	   }
	}

> **_步骤 5_**  
> 执行程序，输出结果：

	Shape : Circle
	Shape : Square
	Shape : Rectangle

## 二、结构型模式（Structural Patterns）
> 这些设计模式关注类和对象的组合。继承的概念被用来组合接口和定义组合对象获得新功能的方式。

### 2.1 适配器模式（Adapter Pattern）

（暂无）

### 2.2 装饰器模式（Decorator Pattern）

（暂无）

### 2.3 代理模式（Proxy Pattern）

> 在代理模式（Proxy Pattern）中，一个类代表另一个类的功能。这种类型的设计模式属于结构型模式。  
> 在代理模式中，我们创建具有现有对象的对象，以便向外界提供功能接口。

> **_介绍_**  
> **意图**：为其他对象提供一种代理以控制对这个对象的访问。  
> **主要解决**：在直接访问对象时带来的问题，比如说：要访问的对象在远程的机器上。在面向对象系统中，有些对象由于某些原因（比如对象创建开销很大，或者某些操作需要安全控制，或者需要进程外的访问），直接访问会给使用者或者系统结构带来很多麻烦，我们可以在访问此对象时加上一个对此对象的访问层。  
> **何时使用**：想在访问一个类时做一些控制。  
> **如何解决**：增加中间层。  
> **关键代码**：实现与被代理类组合。  
> **应用实例**： 1、Windows 里面的快捷方式。 2、猪八戒去找高翠兰结果是孙悟空变的，可以这样理解：把高翠兰的外貌抽象出来，高翠兰本人和孙悟空都实现了这个接口，猪八戒访问高翠兰的时候看不出来这个是孙悟空，所以说孙悟空是高翠兰代理类。 3、买火车票不一定在火车站买，也可以去代售点。 4、一张支票或银行存单是账户中资金的代理。支票在市场交易中用来代替现金，并提供对签发人账号上资金的控制。 5、spring aop。  
> **优点**： 1、职责清晰。 2、高扩展性。 3、智能化。  
> **缺点**： 1、由于在客户端和真实主题之间增加了代理对象，因此有些类型的代理模式可能会造成请求的处理速度变慢。 2、实现代理模式需要额外的工作，有些代理模式的实现非常复杂。  
> **使用场景**：按职责来划分，通常有以下使用场景： 1、远程代理。 2、虚拟代理。 3、Copy-on-Write 代理。 4、保护（Protect or Access）代理。 5、Cache代理。 6、防火墙（Firewall）代理。 7、同步化（Synchronization）代理。 8、智能引用（Smart Reference）代理。  
> **注意事项**： 1、和适配器模式的区别：适配器模式主要改变所考虑对象的接口，而代理模式不能改变所代理类的接口。 2、和装饰器模式的区别：装饰器模式为了增强功能，而代理模式是为了加以控制。  

> **_实现_**  
> 我们将创建一个 Image 接口和实现了 Image 接口的实体类。ProxyImage 是一个代理类，减少 RealImage 对象加载的内存占用。  
> ProxyPatternDemo，我们的演示类使用 ProxyImage 来获取要加载的 Image 对象，并按照需求进行显示。

> 代理模式的 UML 图
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/DesignModel/12.jpg)

> **_步骤 1_**  
> 创建一个接口。

	Image.java
	public interface Image {
	   void display();
	}

> **_步骤 2_**  
> 创建实现接口的实体类。

	RealImage.java
	public class RealImage implements Image {
	 
	   private String fileName;
	 
	   public RealImage(String fileName){
	      this.fileName = fileName;
	      loadFromDisk(fileName);
	   }
	 
	   @Override
	   public void display() {
	      System.out.println("Displaying " + fileName);
	   }
	 
	   private void loadFromDisk(String fileName){
	      System.out.println("Loading " + fileName);
	   }
	}
	
	ProxyImage.java
	public class ProxyImage implements Image{
	 
	   private RealImage realImage;
	   private String fileName;
	 
	   public ProxyImage(String fileName){
	      this.fileName = fileName;
	   }
	 
	   @Override
	   public void display() {
	      if(realImage == null){
	         realImage = new RealImage(fileName);
	      }
	      realImage.display();
	   }
	}

> **_步骤 3_**  
> 当被请求时，使用 ProxyImage 来获取 RealImage 类的对象。

	ProxyPatternDemo.java
	public class ProxyPatternDemo {
	   
	   public static void main(String[] args) {
	      Image image = new ProxyImage("test_10mb.jpg");
	 
	      // 图像将从磁盘加载
	      image.display(); 
	      System.out.println("");
	      // 图像不需要从磁盘加载
	      image.display();  
	   }
	}
	
> **_步骤 4_**  
> 执行程序，输出结果：

	Loading test_10mb.jpg
	Displaying test_10mb.jpg
	
	Displaying test_10mb.jpg

### 2.4 外观模式（Facade Pattern）

### 2.5 桥接模式（Bridge Pattern）

### 2.6 组合模式（Composite Pattern）

### 2.7 享元模式（Flyweight Pattern）

## 三、行为型模式（Behavioral Patterns）
> 这些设计模式特别关注对象之间的通信。

### 3.1 策略模式（Strategy Pattern）

### 3.2 模板方法模式（Template Pattern）

### 3.3 观察者模式（Observer Pattern）

### 3.4 迭代器模式（Iterator Pattern）

### 3.5 责任链模式（Chain of Responsibility Pattern）

### 3.6 命令模式（Command Pattern）

### 3.7 备忘录模式（Memento Pattern）

### 3.8 状态模式（State Pattern）

### 3.9 访问者模式

### 3.10 中介者模式

### 3.11 解释器模式

## 四、J2EE 模式
>这些设计模式特别关注表示层。这些模式是由 Sun Java Center 鉴定的。

### MVC 模式（MVC Pattern）

### 业务代表模式（Business Delegate Pattern）
    
### 组合实体模式（Composite Entity Pattern）
    
### 数据访问对象模式（Data Access Object Pattern）
    
### 前端控制器模式（Front Controller Pattern）
    
### 拦截过滤器模式（Intercepting Filter Pattern）
    
### 服务定位器模式（Service Locator Pattern）
    
### 传输对象模式（Transfer Object Pattern）


