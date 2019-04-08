## Java知识要点（基础篇）

<!--目录结构-->

[toc]

### 基本功

+ **面向对象的特征**  

_答_：  

面向对象的三大特征：封装、继承、多态。 
  
_解析_：  
#### 封装：  

##### 1、概念：  
> 将类的某些信息隐藏在类内部，不允许外部程序直接访问，而是通过该类提供的方法来实现对隐藏信息的操作和访问。  
	
##### 2、好处：  
> - 只能通过规定的方法访问数据。  
> - 隐藏类的实例细节，方便修改和实现。  
	
##### 3、封装的实现步骤  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/01.png)
  
> **需要注意**：对封装的属性不一定要通过get/set方法，其他方法也可以对封装的属性进行操作。当然最好使用get/set方法，比较标准。
	
##### A、访问修饰符  
　![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/02.png)
> 从表格可以看出从上到下封装性越来越差。

##### B、this关键字  
	
> 1.this关键字代表当前对象  
　　this.属性 --> 操作当前对象的属性  
　　this.方法 --> 调用当前对象的方法。  
> 2.封装对象的属性的时候，经常会使用this关键字  
> 3.当getter和setter函数参数名和成员函数名重合的时候，可以使用this区别。如：
	![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/03.png)

##### C、Java 中的内部类  
> 内部类（ Inner Class ）就是定义在另外一个类里面的类。与之对应，包含内部类的类被称为外部类。  

> 那么问题来了：那为什么要将一个类定义在另一个类里面呢？清清爽爽的独立的一个类多好啊！！  

> 答：内部类的主要作用如下：  
1. 内部类提供了更好的封装，可以把内部类隐藏在外部类之内，不允许同一个包中的其他类访问该类。  
2. 内部类的方法可以直接访问外部类的所有数据，包括私有的数据。  
3. 内部类所实现的功能使用外部类同样可以实现，只是有时使用内部类更方便。
  
> 内部类可分为以下几种：  
成员内部类  
静态内部类  
方法内部类  
匿名内部类  　
	
#### 继承：  

##### 1、继承的概念
> 继承是类与类的一种关系，是一种“is a”的关系。比如“狗”继承“动物”，这里动物类是狗类的父类或者基类，狗类是动物类的子类或者派生类。如下图所示：
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/04.png)

> 注：java中的继承是单继承，即一个类只有一个父类。

##### 2、继承的好处
> 子类拥有父类的所有属性和方法（除了private修饰的属性不能拥有）从而实现了代码的复用；　

##### 3、语法规则，只要在子类加上extends关键字继承相应的父类就可以了：
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/05.png)

##### A、方法的重写
> 子类如果对继承的父类的方法不满意（不适合），可以自己编写继承的方法，这种方式就称为方法的重写。当调用方法时会优先调用子类的方法。

> 重写要注意：  
a、返回值类型  
b、方法名  
c、参数类型及个数  

> 都要与父类继承的方法相同，才叫方法的重写。

> _**重载和重写的区别**_：

> **方法重载**：在同一个类中处理不同数据的多个相同方法名的多态手段。  
> **方法重写**：相对继承而言，子类中对父类已经存在的方法进行区别化的修改。

##### B、继承的初始化顺序
> 1、初始化父类再初始化子类.  
> 2、先执行初始化对象中属性，再执行构造方法中的初始化。  

> 基于上面两点，我们就知道实例化一个子类，java程序的执行顺序是：  
> **父类对象属性初始化---->父类对象构造方法---->子类对象属性初始化--->子类对象构造方法**

> 下面有个形象的图：
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/06.png)

##### C、final关键字
> 使用final关键字做标识有“最终的”含义。

> 1. final 修饰类，则该类不允许被继承。

> 2. final 修饰方法，则该方法不允许被覆盖(重写)。

> 3. final 修饰属性，则该类的该属性不会进行隐式的初始化，所以 该final 属性的初始化属性必须有值，或在构造方法中赋值(但只能选其一，且必须选其一，因为没有默认值！)，且初始化之后就不能改了，只能赋值一次。

> 4. final 修饰变量，则该变量的值只能赋一次值，在声明变量的时候才能赋值，即变为常量。

##### D、super关键字
> 在对象的内部使用，可以代表父类对象。  
1、访问父类的属性：super.age  
2、访问父类的方法：super.eat()  

> **super的应用**：

> 首先我们知道子类的构造的过程当中必须调用父类的构造方法。其实这个过程已经隐式地使用了我们的super关键字。  
> 这是因为如果子类的构造方法中没有显示调用父类的构造方法，则系统默认调用父类无参的构造方法。  
> 那么如果自己用super关键字在子类里调用父类的构造方法，则必须在子类的构造方法中的第一行。  
> 要注意的是：如果子类构造方法中既没有显示调用父类的构造方法，而父类没有无参的构造方法，则编译出错。  
> （补充说明，虽然没有显示声明父类的无参的构造方法，系统会自动默认生成一个无参构造方法，但是，如果你声明了一个有参的构造方法，而没有声明无参的构造方法，这时系统不会自动默认生成一个无参构造方法，此时称为父类没有无参的构造方法。）

##### E、Object类
> Object类是所有类的父类，如果一个类没有使用extends关键字明确标识继承另一个类，那么这个类默认继承Object类。

> Object类中的方法，适合所有子类！！！

> 那么Object类中有什么主要的方法呢？

> **1、toString()**  
> a. 在Object类里面定义toString()方法的时候返回的对象的哈希code码(对象地址字符串)。  

> 我们可以发现，如果我们直接用System.out.print（对象）输出一个对象，则运行结果输出的是对象的对象地址字符串，也称为哈希code码。
> 如：
	
	com.hy.cll@1314520
	
> 哈希码是通过哈希算法生成的一个字符串，它是用来唯一区分我们对象的地址码，就像我们的身份证一样。　　

> b. 可以通过重写toString()方法表示出对象的属性。

> 如果我们希望输出一个对象的时候，不是它的哈希码，而是它的各个属性值，那我们可以通过重写toString()方法表示出对象的属性。

> **2、equals()**  
> a、equals（）----返回值是布尔类型。

> b、默认的情况下，比较的是对象的引用是否指向同一块内存地址-------对象实例化时，即给对象分配内存空间，该内存空间的地址就是内存地址。使用方法如：
	
	dog.equals(dog2);

> c、 如果是两个对象，但想判断两个对象的属性是否相同，则重写equals（）方法。

> 以Dog类为例，重写后的equals（）方法如下（当然你可以根据自己想比较的属性来重写，这里我以age属性是否相同来重写equals（）方法）：  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/07.png)

> 上面有四个判断，它们的含义分别是：  
> 1.判断地址是否相同----if (this == obj)，相同则返回true.  
> 2.判断对象是否为空----if (obj == null)，为空则返回false.  
> 3.getClass（）可以得到类对象，判断类型是否一样-----if (getClass() != obj.getClass())，不一样则返回false.  
> 4.判断属性值是否一样----if (age != other.age)，不一样返回false.  
> 5.如果地址相同，<font color=blue>对象不为空，类型一样，属性值一样</font>则返回true.  

> 这里要注意的是，理解obj.getClass()得到的<font color=blue>类对象</font>和<font color=blue>类_的_对象</font>的区别，以下用图形表示：  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/08.png)

> 可以看到，对于<font color=blue>类对象</font>我们关心它属于哪个类，拥有什么属性和方法，比如我和你都是属于“人”这个类对象；而<font color=blue>类_的_对象</font>则是一个类的实例化的具体的一个对象。比如我和你是两个不同的人。

#### 多态：  

> 面向对象的最后一个特性就是多态，那么什么是多态呢？**<font color=blue>多态就是对象的多种形态。</font>**

java里的多态主要表现在两个方面：

##### 1.引用多态  　　
> 父类的引用可以指向本类的对象；  
> 父类的引用可以指向子类的对象；  

> 这两句话是什么意思呢，让我们用代码来体验一下，首先我们创建一个父类Animal和一个子类Dog，在主函数里如下所示：  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/09.png)

> 注意：我们不能使用一个子类的引用来指向父类的对象，如：![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/10.png)

> 这里我们必须深刻理解引用多态的意义，才能更好记忆这种多态的特性。为什么子类的引用不能用来指向父类的对象呢？我在这里通俗给大家讲解一下：就以上面的例子来说，我们能说“狗是一种动物”，但是不能说“动物是一种狗”，狗和动物是父类和子类的继承关系，它们的从属是不能颠倒的。当父类的引用指向子类的对象时，该对象将只是看成一种特殊的父类（里面有重写的方法和属性），反之，一个子类的引用来指向父类的对象是不可行的！！

##### 2.方法多态
> 根据上述创建的两个对象：本类对象和子类对象，同样都是父类的引用，当我们指向不同的对象时，它们调用的方法也是多态的。

> 创建本类对象时，调用的方法为<font color=blue>本类方法</font>；

> 创建子类对象时，调用的方法为<font color=blue>子类重写的方法或者继承的方法</font>；

> 使用多态的时候要注意：<font color=blue>如果我们在子类中编写一个独有的方法（没有继承父类的方法），此时就不能通过父类的引用创建的子类对象来调用该方法！！！</font>

> <font color=blue>**注意： 继承是多态的基础。**</font>

##### A、引用类型转换　
> 了解了多态的含义后，我们在日常使用多态的特性时经常需要进行引用类型转换。

> 引用类型转换：

> **1. 向上类型转换(隐式/自动类型转换)**，是小类型转换到大类型。  
> 就以上述的父类Animal和一个子类Dog来说明，当父类的引用可以指向子类的对象时，就是向上类型转换。如：
	
	Dog dog = new Dog();
	Animal animal = dog; // 自动类型提升，向上类型转换
	
> **2. 向下类型转换(强制类型转换)**，是大类型转换到小类型(有风险,可能出现数据溢出)。  
> 将上述代码再加上一行，我们再次将父类转换为子类引用，那么会出现错误，编译器不允许我们直接这么做，虽然我们知道这个父类引用指向的就是子类对象，但是编译器认为这种转换是存在风险的。如：
	
	Dog dog = new Dog();
	Animal animal = dog; // 自动类型提升，向上类型转换
	Dog dog2 = animal; // animal 编译报错
	
> 那么我们该怎么解决这个问题呢，我们可以在animal前加上（Dog）来强制类型转换。如：
	
	Dog dog = new Dog();
	Animal animal = dog; // 自动类型提升，向上类型转换
	Dog dog2 = (Dog) animal; // 向下类型转换，强制类型转换

> 但是如果父类引用没有指向该子类的对象，则不能向下类型转换，虽然编译器不会报错，但是运行的时候程序会出错，如：
	
	Dog dog2 = (Dog) new Animal();

> 其实这就是上面所说的子类的引用指向父类的对象，而强制转换类型也不能转换！！  
> 还有一种情况是父类的引用指向其他子类的对象，则不能通过强制转为该子类的对象。如：

	Dog dog = new Dog();
	Animal animal = dog; // 自动类型提升，向上类型转换
	Dog dog2 = (Dog) animal; // 向下类型转换，强制类型转换
	Cat cat = (Cat) animal; // 1.编译时是 Cat 类型；2.运行时是 Dog 类型。

> 这是因为我们在编译的时候进行了强制类型转换，编译时的类型是我们强制转换的类型，所以编译器不会报错，而当我们运行的时候，程序给animal开辟的是Dog类型的内存空间，这与Cat类型内存空间不匹配，所以无法正常转换。这两种情况出错的本质是一样的，所以我们在使用强制类型转换的时候要特别注意这两种错误！！下面有个更安全的方式来实现向下类型转换。。。。

> **3. instanceof 运算符**，来解决引用对象的类型，避免类型转换的安全性问题。

> instanceof 是 Java 的一个二元操作符，和==，>，<是同一类东东。由于它是由字母组成的，所以也是Java的保留关键字。<font color=blue>它的作用是测试它左边的对象是否是它右边的类的实例</font>，返回boolean类型的数据。

> 我们来使用instanceof运算符来规避上面的错误，代码修改如下：

	Dog dog = new Dog();
	Animal animal = dog; // 自动类型提升，向上类型转换
	Dog dog2 = (Dog) animal; // 向下类型转换，强制类型转换
	if (animal instanceof Cat) {
		Cat cat = (Cat) animal; // 1.编译时是 Cat 类型；2.运行时是 Dog 类型。
	}
	
> 利用if语句和instanceof运算符来判断两个对象的类型是否一致。

> **补充说明**：在比较一个对象是否和另一个对象属于同一个类实例的时候，我们通常可以采用instanceof和getClass两种方法通过两者是否相等来判断，但是两者在判断上面是有差别的。Instanceof进行类型检查规则是: <font color=blue>你属于该类吗？或者你属于该类的派生类吗？</font>而通过getClass获得类型信息采用==来进行检查是否相等的操作是<font color=blue>严格的判断,不会存在继承方面的考虑</font>；

> **总结**：在写程序的时候，如果要进行类型转换，我们最好使用instanceof运算符来判断它左边的对象是否是它右边的类的实例，再进行强制转换。

##### B、抽象类
> 定义：抽象类前使用abstract关键字修饰，则该类为抽象类。  

> 使用抽象类要注意以下几点：  
> 1. 抽象类是约束子类必须有什么方法，而并不关注子类如何实现这些方法。  
> 2. 抽象类应用场景：  
> a. 在某些情况下，某个父类只是知道其子类应该包含怎样的方法，但无法准确知道这些子类如何实现这些方法(可实现动态多态)。  
> b. 从多个具有相同特征的类中抽象出一个抽象类，以这个抽象类作为子类的模板，从而避免子类设计的随意性。  
> 3. 抽象类定义抽象方法，只有声明，不需要实现。抽象方法没有方法体以分号结束，抽象方法必须用abstract关键字来修饰。如:  

	public abstract class hy {
		public abstract void cll(); // 抽象方法，方法体以分号结束，只有声明，没有实现
	}

> 4、包含抽象方法的类是抽象类。<font color=blue>抽象类中可以包含普通的方法，也可以没有抽象方法</font>。如：
	
	public abstract class hy {
		//抽象类可以有非抽象的方法
		public void cllSay() {
			System.out.println("I Love You");
		}
	}

> 5、抽象类不能直接创建，可以定义引用变量来指向子类对象，来实现抽象方法。以上述的Telephone抽象类为例：　　　　　

	public abstract class Telephone {
		public abstract void call(); //抽象方法，方法体以分号结束，只有声明，不需要实现
		public void message(){
			System.out.println("我是抽象类的普通方法");
		} //抽象类中包含普通的方法
	}

	public class Phone extends Telephone { 
		public void call() {//继承抽象类的子类必须重写抽象方法
			// TODO Auto-generated method stub
			System.out.println("我重写了抽象类的方法");
		}  
	}
	
> 以上是Telephone抽象类和子类Phone的定义，下面我们看main函数里：  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/11.png)

> 运行结果（排错之后）：  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/12.png)

##### C、接口
**1、概念**  
> 接口可以理解为一种特殊的类，由全局常量和公共的抽象方法所组成。也可理解为一个特殊的抽象类，因为它含有抽象方法。

> 如果说类是一种具体实现体，而接口定义了某一批类所需要遵守的规范，接口不关心这些类的内部数据，也不关心这些类里方法的实现细节，它只规定这些类里必须提供的某些方法。（这里与抽象类相似）

> **2.接口定义的基本语法**

	[修饰符] [abstract] interface 接口名 [extends父接口1,2....]（多继承）{
		
		0…n常量 (public static final)                                          
		
		0…n 抽象方法(public abstract)                                      
	
	}                                                                                             

> 其中[ ]里的内容表示可选项，可以写也可以不写;接口中的属性都是常量，即使定义时不添加public static final 修饰符，系统也会自动加上；接口中的方法都是抽象方法，即使定义时不添加public abstract修饰符，系统也会自动加上。

> **3.使用接口**  
> 一个类可以实现一个或多个接口，实现接口使用implements关键字。java中一个类只能继承一个父类，是不够灵活的，通过实现多个接口可以补充。

> **继承父类实现接口的语法为：**

	[修饰符] class 类名 extends 父类 implements 接口1，接口2...{
	
		类体部分//如果继承了抽象类，需要实现继承的抽象方法；要实现接口中的抽象方法
	
	}

> 注意：如果要继承父类，继承父类必须在实现接口之前,即extends关键字必须在implements关键字前.  
> 补充说明：通常我们在命名一个接口时，经常以I开头，用来区分普通的类。如：IPlayGame.  

> 以下我们来补充在上述抽象类中的例子，我们之前已经定义了一个抽象类Telephone和子类Phone，这里我们再创建一个IPlayGame的接口，然后在原来定义的两个类稍作修改，代码如下：

	public interface IPlayGame {
		public void paly();//abstract 关键字可以省略，系统会自动加上
		public String name="游戏名字";//static final关键字可以省略，系统会自动加上
	}
	
	public class Phone extends Telephone implements IPlayGame{
	
		public void call() {//继承抽象类的子类必须重写抽象方法
			// TODO Auto-generated method stub
			System.out.println("我重写了抽象类的方法");
		}
	
		@Override
		public void paly() {
			// TODO Auto-generated method stub
			System.out.println("我重写了接口的方法");
		}    
	}


	public class train {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			IPlayGame i=new Phone();//用接口的引用指向子类的对象
			i.paly();//调用接口的方法
			System.out.println(i.name);//输出接口的常量
		}
	}

> 运行结果：  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/13.png)

> **4.接口和匿名内部类配合使用**  
> 接口在使用过程中还经常和匿名内部类配合使用。匿名内部类就是没有没名字的内部类，多用于关注实现而不关注实现类的名称。

> 语法格式：

	Interface i =new interface(){
		Public void method{
			System.out.println(“利用匿名内部类实现接口1”);
		}
	};
	i.method();

> 还有一种写法：（直接把方法的调用写在匿名内部类的最后）

	Interface i =new interface(){
		Public void method{
			System.out.println(“利用匿名内部类实现接口1”);
		}
	}.method();

#### 抽象类和接口的区别

> **（1）语法层面上的区别**  
> 1.一个类只能继承一个抽象类，而一个类却可以实现多个接口。  
> 2.抽象类中的成员变量可以是各种类型的，而接口中的成员变量只能是public static final类型的；且必须给其初值，所以实现类中不能重新定义，也不能改变其值；抽象类中的变量默认是 friendly 型，其值可以在子类中重新定义，也可以重新赋值。  
> 3.抽象类中可以有非抽象方法，接口中则不能有非抽象方法。  
> 4.接口可以省略abstract 关键字，抽象类不能。  
> 5.接口中不能含有静态代码块以及静态方法，而抽象类可以有静态代码块和静态方法；  

> **（2）设计层面上的区别**

> 1）<font color=blue>抽象类是对一种事物的抽象，即对类抽象，而接口是对行为的抽象。</font>抽象类是对整个类整体进行抽象，包括属性、行为，但是接口却是对类局部（行为）进行抽象。举个简单的例子，飞机和鸟是不同类的事物，但是它们都有一个共性，就是都会飞。那么在设计的时候，可以将飞机设计为一个类Airplane，将鸟设计为一个类Bird，但是不能将 飞行 这个特性也设计为类，因此它只是一个行为特性，并不是对一类事物的抽象描述。此时可以将 飞行 设计为一个接口Fly，包含方法fly( )，然后Airplane和Bird分别根据自己的需要实现Fly这个接口。然后至于有不同种类的飞机，比如战斗机、民用飞机等直接继承Airplane即可，对于鸟也是类似的，不同种类的鸟直接继承Bird类即可。从这里可以看出，继承是一个 "是不是"的关系，而 接口 实现则是 "有没有"的关系。如果一个类继承了某个抽象类，则子类必定是抽象类的种类，而接口实现则是有没有、具备不具备的关系，比如鸟是否能飞（或者是否具备飞行这个特点），能飞行则可以实现这个接口，不能飞行就不实现这个接口。  

> 2）<font color=blue>设计层面不同，抽象类作为很多子类的父类，它是一种模板式设计。</font>而接口是一种行为规范，它是一种辐射式设计。什么是模板式设计？最简单例子，大家都用过ppt里面的模板，如果用模板A设计了ppt B和ppt C，ppt B和ppt C公共的部分就是模板A了，如果它们的公共部分需要改动，则只需要改动模板A就可以了，不需要重新对ppt B和ppt C进行改动。而辐射式设计，比如某个电梯都装了某种报警器，一旦要更新报警器，就必须全部更新。也就是说对于抽象类，如果需要添加新的方法，可以直接在抽象类中添加具体的实现，子类可以不进行变更；而对于接口则不行，如果接口进行了变更，则所有实现这个接口的类都必须进行相应的改动。

> 下面看一个网上流传最广泛的例子：门和警报的例子：门都有open( )和close( )两个动作，此时我们可以定义通过抽象类和接口来定义这个抽象概念：

	abstract class Door {
		public abstract void open();
		public abstract void close();
	}

> 或者：

	interface Door {
		public abstract void open();
		public abstract void close();
	}
	
> 但是现在如果我们需要门具有报警alarm( )的功能，那么该如何实现？下面提供两种思路：

> 1）将这三个功能都放在抽象类里面，但是这样一来所有继承于这个抽象类的子类都具备了报警功能，但是有的门并不一定具备报警功能；

> 2）将这三个功能都放在接口里面，需要用到报警功能的类就需要实现这个接口中的open( )和close( )，也许这个类根本就不具备open( )和close( )这两个功能，比如火灾报警器。

> 从这里可以看出， Door的open() 、close()和alarm()根本就属于两个不同范畴内的行为，open()和close()属于门本身固有的行为特性，而alarm()属于延伸的附加行为。因此最好的解决办法是单独将报警设计为一个接口，包含alarm()行为,Door设计为单独的一个抽象类，包含open和close两种行为。再设计一个报警门继承Door类和实现Alarm接口。

	interface Alram {
		void alarm();
	}

	abstract class Door {
		void open();
		void close();
	}

	class AlarmDoor extends Door implements Alarm {
		void oepn() {
			//....
		}
		void close() {
			//....
		}
		void alarm() {
			//....
		}
	}
	
+ **final, finally, finalize 的区别**  

	_答_：
	
> 1.**final: 可以修饰class、方法、变量**  
	  &emsp;&emsp;&emsp;final修饰的class无法被继承扩展。  
	  &emsp;&emsp;&emsp;final修饰的方法，无法被重写(overide)。  
	  &emsp;&emsp;&emsp;final修饰的变量，无法被更改。  
> 2.**finally: 用于try-catch，保证发生异常时会进行清理工作，如释放资源、执行unlock等操作。**  
> 3.**finalize：java.lang.Object的方法，本意是在GC前做一些回收工作，但是会造成性能急剧下降。**  
	  &emsp;&emsp;&emsp;JDK9中已经被废弃。  
	  &emsp;&emsp;&emsp;执行时间不确定。  
	  &emsp;&emsp;&emsp;严重影响GC性能(40~50倍)。  

_解析_：  

#### Final

##### 1.1 修饰类

> 　　当用final修饰类的时，表明该类不能被其他类所继承。当我们需要让一个类永远不被继承，此时就可以用final修饰，但要注意：

> <font color=red>final类中所有的成员方法都会隐式的定义为final方法。</font>

##### 1.2 修饰方法

> 使用final方法的原因主要有两个：

> 　　(1) 把方法锁定，以防止继承类对其进行更改。

> 　　(2) 效率，在早期的java版本中，会将final方法转为内嵌调用。但若方法过于庞大，可能在性能上不会有多大提升。因此在最近版本中，不需要final方法进行这些优化了。

> <font color=blue>final方法意味着“最后的、最终的”含义，即此方法不能被重写。</font>

> <font color=red>注意：若父类中final方法的访问权限为private，将导致子类中不能直接继承该方法，因此，此时可以在子类中定义相同方法名的函数，此时不会与重写final的矛盾，而是在子类中重新地定义了新方法。</font>  
> 如以下代码示例：

	class A{
	    private final void getName(){
	
	    }
	}

	public class B extends A{
	    public void getName(){
	
	    }
	
	    public static void main(String[]args){
	        System.out.println("OK");
	    }
	}

##### 1.3 修饰变量

>  　　final成员变量表示常量，只能被赋值一次，赋值后其值不再改变。类似于C++中的const。

> 　　当final修饰一个基本数据类型时，表示该基本数据类型的值一旦在初始化后便不能发生变化；如果final修饰一个引用类型时，则在对其初始化之后便不能再让其指向其他对象了，但该引用所指向的对象的内容是可以发生变化的。本质上是一回事，因为引用的值是一个地址，final要求值，即地址的值不发生变化。　

> 　　<font color=blue>**final修饰一个成员变量（属性），必须要显示初始化。**</font>这里有两种初始化方式，**一种是在变量声明的时候初始化；第二种方法是在声明变量的时候不赋初值，但是要在这个变量所在的类的所有的构造函数中对这个变量赋初值。**

> 　　当函数的参数类型声明为final时，说明该参数是只读型的。即你可以读取使用该参数，但是无法改变该参数的值。
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/14.png)

> 　　在java中，String被设计成final类，那为什么平时使用时，String的值可以被改变呢？

> 　　字符串常量池是java堆内存中一个特殊的存储区域，当我们建立一个String对象时，假设常量池不存在该字符串，则创建一个，若存在则直接引用已经存在的字符串。当我们对String对象值改变的时候，例如 String a="A"; a="B" 。a是String对象的一个引用（我们这里所说的String对象其实是指字符串常量），当a=“B”执行时，并不是原本String对象("A")发生改变，而是创建一个新的对象("B")，令a引用它。

##### Final常见问题：

> **1、final的作用?**

> 可以修饰class、方法、变量.  
&emsp;&emsp;&emsp;final修饰的class无法被继承扩展.  
&emsp;&emsp;&emsp;final修饰的方法，无法被重写(overide).  
&emsp;&emsp;&emsp;final修饰的变量，无法被更改.  

> **2、final的好处?**

> 保护代码，避免以外的编程错误。  
防止别人去修改核心内容，导致功能不正确以及避免潜在的安全隐患.  

> **3、final能有助于JVM将方法内联，改善编译器进行条件编译的能力，从而提高性能？**

> 错误!  
1. 这种结论是基于猜测和假设   
1. 现代高性能的虚拟机，如HotSpot非常智能，并不是通过final来判断是否能内联。  

> **4、final修饰的变量就是常量？**

> 错误！  

> 1-修饰的基本数据类型，一旦赋值就无法改变。该变量必须要先初始化。  

	final int a = 10;

> 2-修饰的引用类型，可以间接修改。包括List等。

	final StringBuilder a = new StringBuilder("aaaa");
	StringBuilder b = a;
	b.append(" 间接修改了final的引用a所指向的内容");
	System.out.println(a+""); // 结果为： aaaa 间接修改了final的引用所指向的内容

> **5、如何创建一个immutable(不可变)的List？**

> final不具备immutable的特性：

	final List<String> list = new ArrayList<>();
	list.add("Hello");
	list.add("final 阻止不了我");

> 利用Connections生成不可修改的集合：

	List<String> immutable = Collections.unmodifiableList(list);
	immutable.add("添加内容会报错");

> 实现immutable Class

> **6、如何实现immutable(不可改变)的类?**

> final修饰class：避免通过扩展来绕开限制。  
private和final修饰所有成员变量，并且不要实现setter方法。  
使用深拷贝来构造对象：不采用直接复制，避免被间接修改内容。  
getter等方法采用copy-on-write原则：将内容copy一份提供出去。  

> **7、匿名内部类中访问的局部变量为什么要用final？**

> Java内部类会去copy一份变量，而不是采用局部变量。  
> final能保证数据一致。  

#### Finally

> 　finally作为异常处理的一部分，它只能用在try/catch语句中，并且附带一个语句块，表示这段语句最终一定会被执行（不管有没有抛出异常），经常被用在需要释放资源的情况下。（×）（这句话其实存在一定的问题）

> 　　很多人都认为finally语句块一定会执行，但真的是这样么？答案是否定的，例如下面这个例子：  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/15.png)

> 当我们去掉注释的三行语句，执行结果为：
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/16.png)

>  　　为什么在以上两种情况下都没有执行finally语句呢，说明什么问题？

> 　　只有与finally对应的try语句块得到执行的情况下，finally语句块才会执行。以上两种情况在执行try语句块之前已经返回或抛出异常，所以try对应的finally语句并没有执行。

> 　　但是，在某些情况下，即使try语句执行了，finally语句也不一定执行。例如以下情况：
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/17.png)

> 　　finally 语句块还是没有执行，为什么呢？因为我们在 try 语句块中执行了 System.exit (0) 语句，终止了 Java 虚拟机的运行。那有人说了，在一般的 Java 应用中基本上是不会调用这个 System.exit(0) 方法的。OK ！没有问题，我们不调用 System.exit(0) 这个方法，那么 finally 语句块就一定会执行吗？

> 　　再一次让大家失望了，答案还是否定的。当一个线程在执行 try 语句块或者 catch 语句块时被打断（interrupted）或者被终止（killed），与其相对应的 finally 语句块可能不会执行。还有更极端的情况，就是在线程运行 try 语句块或者 catch 语句块时，突然死机或者断电，finally 语句块肯定不会执行了。可能有人认为死机、断电这些理由有些强词夺理，没有关系，我们只是为了说明这个问题。

> **易错点**

> 　　在try-catch-finally语句中执行return语句。我们看如下代码：
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/18.png)

> 　　答案：4,4,4  。    为什么呢？

> 　　首先finally语句在改代码中一定会执行，从运行结果来看，每次return的结果都是4（即finally语句），仿佛其他return语句被屏蔽掉了。

> 　　事实也确实如此，因为finally用法特殊，所以会撤销之前的return语句，继续执行最后的finally块中的代码。 

##### Finally 常见问题

> **1、finally的作用？**

> 用于try-catch，保证发生异常时会进行清理工作，如释放资源、执行unlock等操作。  
推荐使用Java 7的try-with-resources来替代finally，能有效避免finally丢失异常的情况。try-with-resources，采用语法糖来实现，编码量少且规范。  

> **2、不要在finally处理会返回的数值、对象。**

> **3、在try中调用break、continue、return都会进入finally（注：正常情况）**

> **4、不要在try中去return返回值，否则一定要保证finally不会修改返回值(数值、对象)。**

> **5、try中有return，也一定会去执行finally。（注：正常情况）**

> **6、finally和return、System.exit(1)的关系**

> finally前执行return，还是会执行finally的内容。
finally前执行System.exit(1)，会立即退出，不会执行finally，然而这种场景并没有什么用。

> **7、finally在哪些情况中不会执行？**

> System.exit(-1)：异常退出  
> try-catch中无限循环  
> finally所处于的线程被杀死  


#### Finalize

> finalize()是在java.lang.Object里定义的，也就是说每一个对象都有这么个方法。这个方法在gc启动，该对象被回收的时候被调用。其实gc可以回收大部分的对象（凡是new出来的对象，gc都能搞定，一般情况下我们又不会用new以外的方式去创建对象），所以一般是不需要程序员去实现finalize的。   
特殊情况下，需要程序员实现finalize，当对象被回收的时候释放一些资源，比如：一个socket链接，在对象初始化时创建，整个生命周期内有效，那么就需要实现finalize，关闭这个链接。 
> 　　使用finalize还需要注意一个事，调用super.finalize();

> 　　一个对象的finalize()方法只会被调用一次，而且finalize()被调用不意味着gc会立即回收该对象，所以有可能调用finalize()后，该对象又不需要被回收了，然后到了真正要被回收的时候，因为前面调用过一次，所以不会调用finalize()，产生问题。 所以，推荐不要使用finalize()方法，它跟析构函数不一样。

##### Finalize 常见问题

> **1、finalize的作用**

> 1.本意是在GC前进行资源回收。  

> 2.实际上Object.finalize()在Java 9中已经被废弃。  

> 3._缺点非常明显：_   

> 1）无法保证finalize什么时候执行、是否满足预期。  
> 2）会影响性能，且容易导致死锁等各种问题。 
 
> 4.除了try-catch-finally和resources两种方法，还可以利用Java 9的cleaner机制。  

> _致命缺点：_  
> **2、finalize的性能极差**  
> 1.在专门的benchmark上测试，finalize在GC时间上，大约有40~50倍的性能差距。极差！  
> 2.即使使用System.runFialization()也没有多大用途，finalize拖慢GC回收，甚至可能会导致OOM。  

> **3、finalize会掩盖资源回收时的异常信息**

> 根据JDK的源码: java.lang.ref.Finalizer
资源回收时出现的异常，会通过Throwable捕获，并且不作任何处理！

	try{
	    // 资源回收工作
	}catch (Throwable x){
	    // 居然吞掉了Throwable
	    super.clear();
	}

> _**替代品：Cleaner机制**_  

> **4、有什么机制可以替换掉finalize？**  
> 1.Java 平台正逐渐使用java.lang.ref.Cleaner来替换掉原有的finalize实现。  
> 2.Cleaner的实现利用了幻想引用(PhantomReference)，采用一种常见的post-mortem清理机制。  
> 3.Cleaner利用幻想引用和引用队列，保证了对象销毁前的清理工作，比如关闭文件描述符等。
> 4.比finalize更加轻量、更加可靠。

> **5、Cleaner的优点**  
> 每个Cleaner的操作都是独立的，有自己的运行线程，可以避免意外死锁等问题。

> **6、Cleaner依旧有缺陷**  
> 如果由于一些原因导致幻想引用堆积，同样会出现问题。只适合作为最后的手段。

> _有关Cleaner，参见Java9中的Cleaner机制_

+ **int 和 Integer 有什么区别**  
	_答_：
> 1、Integer是int的包装类，int则是java的一种基本数据类型。  
> 2、Integer变量必须实例化后才能使用，而int变量不需要。  
> 3、Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值。  
> 4、Integer的默认值是null，int的默认值是0。  
	
	_解析_：  
	
##### 关于Integer和int的比较 

> 1、由于Integer变量实际上是对一个Integer对象的引用，所以两个通过new生成的Integer变量永远是不相等的（因为new生成的是两个对象，其内存地址不同）。  

	Integer i = new Integer(100);
	Integer j = new Integer(100);
	System.out.print(i == j); //false

> 2、Integer变量和int变量比较时，只要两个变量的值是向等的，则结果为true（因为包装类Integer和基本数据类型int比较时，java会自动拆包装为int，然后进行比较，实际上就变为两个int变量的比较）

	Integer i = new Integer(100);
	int j = 100；
	System.out.print(i == j); //true
	
> 3、非new生成的Integer变量和new Integer()生成的变量比较时，结果为false。（因为非new生成的Integer变量指向的是java常量池中的对象，而new Integer()生成的变量指向堆中新建的对象，两者在内存中的地址不同）

	Integer i = new Integer(100);
	Integer j = 100;
	System.out.print(i == j); //false
	
> 4、对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则比较结果为false

	Integer i = 100;
	Integer j = 100;
	System.out.print(i == j); //true
	Integer i = 128;
	Integer j = 128;
	System.out.print(i == j); //false
	
> 对于第4条的原因：  
java在编译Integer i = 100 ;时，会翻译成为Integer i = Integer.valueOf(100)；，而java API中对Integer类型的valueOf的定义如下：  

	public static Integer valueOf(int i){
	    assert IntegerCache.high >= 127;
	    if (i >= IntegerCache.low && i <= IntegerCache.high){
	        return IntegerCache.cache[i + (-IntegerCache.low)];
	    }
	    return new Integer(i);
	}
	
> java对于-128到127之间的数，会进行缓存，Integer i = 127时，会将127进行缓存，下次再写Integer j = 127时，就会直接从缓存中取，就不会new了。

> **以上的情况总结如下：**

> 1，无论如何，Integer与new Integer不会相等。不会经历拆箱过程，new出来的对象存放在堆，而非new的Integer常量则在常量池（在方法区），他们的内存地址不一样，所以为false。

> 2，两个都是非new出来的Integer，如果数在-128到127之间，则是true,否则为false。因为java在编译Integer i = 128的时候,被翻译成：Integer i = Integer.valueOf(128);而valueOf()函数会对-128到127之间的数进行缓存。

> 3，两个都是new出来的,都为false。还是内存地址不一样。

> 4，int和Integer(无论new否)比，都为true，因为会把Integer自动拆箱为int再去比。


+ **重载和重写的区别**  
	_答_：  
	
> 方法的<font color=blue>重载</font>和<font color=blue>重写</font>都是实现多态的方式，区别在于前者实现的是编译时的多态性，而后者实现的是运行时的多态性。重载发生在一个类中，同名的方法如果有不同的参数列表（参数类型不同、参数个数不同或者二者都不同）则视为重载；重写发生在子类与父类之间，重写要求子类被重写方法与父类被重写方法有相同的参数列表，有兼容的返回类型，比父类被重写方法更好访问，不能比父类被重写方法声明更多的异常（里氏代换原则）。重载对返回类型没有特殊的要求，不能根据返回类型进行区分。
	
> 方法**重载**是指同一个类中的多个方法具有相同的名字,但这些方法具有不同的参数列表,即参数的数量或参数类型不能完全相同。  

> 方法**重写**是存在子父类之间的,子类定义的方法与父类中的方法具有相同的方法名字,相同的参数表和相同的返回类型。  
> 注:   
(1)子类中不能重写父类中的final方法。  
(2)子类中必须重写父类中的abstract方法。
  
_解析_：

#### 重载(Overload)

> 在一个类中，同名的方法如果有不同的参数列表（参数类型不同、参数个数不同甚至是参数顺序不同）则视为重载。同时，重载对返回类型没有要求，可以相同也可以不同，但不能通过返回类型是否相同来判断重载。 

	public class Father {
		
	    public void sayHello() {
	        System.out.println("Hello");
	    }
	
	    public void sayHello(String name) {
	        System.out.println("Hello" + " " + name);
	    }
	    
	    public int sayHello(String name, String sex) {
	    	System.out.println("Hello" + " " + name + " sex" + sex);
	    	return 1;
	    }
	}

> **重载 总结**：  
> 1.重载(Overload)是<font color=blue>一个类中多态性的一种表现。</font>调用方法时通过传递给它们的不同参数个数和参数类型来决定具体使用哪个方法, 这就是多态性；  
> 2.重载要求同名方法的参数列表不同(参数类型，参数个数甚至是参数顺序)；  
> 3.重载的时候，返回值类型可以相同也可以不相同。无法以返回类型作为重载函数的区分标准；  
> 4.不能通过访问权限、返回类型、抛出的异常进行重载；  
> 5.方法的异常类型和数目不会对重载造成影响；  
> 6.对于继承来说，如果某一方法在父类中是访问权限是priavte，那么就不能在子类对其进行重载，如果定义的话，也只是定义了一个新方法，而不会达到重载的效果。  

> **重载的规则**：  
1）、必须具有不同的参数列表；  
2）、可以有不同的返回类型，只要参数列表不同就可以了；  
3）、可以有不同的访问修饰符；  
4）、可以抛出不同的异常；  

#### 重写(Override)

> （1） 父类与子类之间的多态性，对父类的函数进行重新定义。是运行时的多样性。如果在子类中定义某方法与其父类有相同的名称和参数，我们说该方法被重写 (Override)。在Java中，子类可继承父类中的方法，而不需要重新编写相同的方法。但有时子类并不想原封不动地继承父类的方法，而是想作一定的修改，这就需要采用方法的重写。方法重写又称方法覆盖。   
> （2）若子类中的方法与父类中的某一方法具有相同的方法名、参数列表和兼容的返回类型，则新方法将覆盖原有的方法。如需父类中原有的方法，可使用super关键字，该关键字引用了当前类的父类。   
> （3）子类函数的访问修饰权限不能少于父类的。  

> 重载，但是子类的返回类型是父类被重写方法的子类，即重写返回方法兼容，编译通过。如下：

	class Parent {
	
	    public Parent make(int i) {
	        System.out.println("Parent int: "+i);
	        return null;
	    }
	}
	
	class Child extends Parent{
	
	    @Override
	    public Parent make(int i) {
	        System.out.println("Child int: "+i);
	        return null;
	    }
	}
	
	public class OverrideTest { 
	    public static void main(String []args){
	        Parent p = new Parent();
	        Child c = new Child();
	        p.make(1);                  //Parent int: 1
	        p.make(new Integer(1));     //Parent int: 1
	        c.make(1);                  //Child int: 1
	        c.make(new Integer(1));     //Child int: 1
	    }
	}

> 突然想到一道int和Integer的面试题，Integer的自动拆箱与装箱，不知道如果把Child的方法参数由int改成Integer会如何，发现编译出错，可见参数列表需要完全相同。如下：

	class Parent {
	
	    public Parent make(int i) {
	        System.out.println("Parent int: "+i);
	        return null;
	    }   
	}
	
	class Child extends Parent{
	
	    @Override
	    public Child make(Integer i) {      //编译出错
	        System.out.println("Child Integer: "+i);
	        return null;
	    }
	}

> 不重写make(int)方法，另写一个make(Integer)方法（此处应该算重载了，继承了父类的make(int)方法，而make(Integer)参数列表不同）。  
> 此时c.make(new Integer(1))则调用Child.make(Integer)方法，不会拆包并调用父类Father.make(int)方法。如下：  

	class Parent {
	
	    public Parent make(int i) {
	        System.out.println("Parent int: "+i);
	        return null;
	    }   
	}
	
	class Child extends Parent{
	
	    public Child make(Integer i) {      
	        System.out.println("Child Integer: "+i);
	        return null;
	    }
	}
	
	public class OverrideTest { 
	    public static void main(String []args){
	        Parent p = new Parent();
	        Child c = new Child();
	        p.make(1);                  //Parent int: 1
	        p.make(new Integer(1));     //Parent int: 1
	        c.make(1);                  //Parent int: 1
	        c.make(new Integer(1));     //Child Integer: 1
	    }
	}

> 重写make(int)方法，并编写make(Integer)方法。此处Child.make(Integer)和Child.make(int)重载，上面是Child继承自Father的make(int)和Child自己的make(int)重载。示例代码如下：

	class Parent {
	
	    public Parent make(int i) {
	        System.out.println("Parent int: "+i);
	        return null;
	    }   
	}
	
	class Child extends Parent{
	
	    @Override
	    public Parent make(int i) {
	        System.out.println("Child int: "+i);
	        return null;
	    }
	
	    public Child make(Integer i) {      
	        System.out.println("Child Integer: "+i);
	        return null;
	    }
	}
	
	public class OverrideTest { 
	    public static void main(String []args){
	        Parent p = new Parent();
	        Child c = new Child();
	        p.make(1);                  //Parent int: 1
	        p.make(new Integer(1));     //Parent int: 1
	        c.make(1);                  //Child int: 1
	        c.make(new Integer(1));     //Child Integer: 1
	    }
	}

> **重写（覆盖）的规则**：  
> 1、重写方法的参数列表必须完全与被重写的方法的相同,否则不能称其为重写而是重载；  
> 2、重写方法的访问修饰符一定要大于(或等于)被重写方法的访问修饰符（public>protected>default>private）；  
> 3、重写的方法的返回值类型必须和被重写的方法的返回值类型一致或者兼容；  
> 4、重写的方法所抛出的异常必须和被重写的方法所抛出的异常一致，或者是其子类；  
> 5、被重写的方法不能为private，否则在其子类中只是新定义了一个方法，并没有对其进行重写；  
> 6、静态方法不能被重写为非静态的方法（会编译出错）；  
> 7、父类方法被final时，无论该方法被public、protected及默认所修饰，子类均不能重写该方法。  

> **重写 (Override) 总结**：  
> 1.发生在父类与子类之间。  
> 2.方法名，参数列表，返回类型（除过子类中方法的返回类型是父类中返回类型的子类）必须相同。  
> 3.访问修饰符的限制一定要大于被重写方法的访问修饰符（public>protected>default>private)。     
> 4.重写方法一定不能抛出新的检查异常或者比被重写方法申明更加宽泛的检查型异常。  


+ **抽象类和接口有什么区别**  
	_答_：  
> 1.抽象类描述的是“是不是”的问题，而接口描述的是“有没有”的问题；  
> 2.在Java中类的继承是“单继承”，可以“多对一”，但是不允许“一对多”。而一个类却可以同时实现多个接口；
	
	_解析_：

#### 抽象类  

> 用abstract修饰的类叫做抽象类。  
> 抽象类是用来捕捉子类的通用特性的。  
> 在讲抽象类之前有必要强调一下**abstract**修饰符：  
>      1.abstract修饰的类为抽象类，此类不能有对象，（无法对此类进行实例化，说白了就是不能new）；  
>      2.abstract修饰的方法为抽象方法，此方法不能有方法体（就是什么内容不能有）；

> **关于抽象类的使用特点：**  
>     1.抽象类不能有对象，（不能用new此关键字来创建抽象类的对象）；  
>     2.有抽象方法的类一定是抽象类，但是抽象类中不一定有抽象方法；  
>     3.抽象类中的抽象方法必须在子类中被重写。  

> 同学们可能会问到：**抽象类不能被“new”，抽象方法必须重写，那么定义它们做什么嘞？**  
>        答：抽象类生来就注定它是要被继承的，如果没有任何一个类去继承它的话，那么也就失去了它的意义；抽象方法生来就是要被重写的，而且是必须重写。（只要继承了某个抽象类，就必须去重写此抽象类中含有的抽象方法）

> 它不能被实例化，只能被用作子类的超类。抽象类是被用来创建继承层级里子类的模板。以JDK中的GenericServlet为例：  

	
		public abstract class GenericServlet implements Servlet, ServletConfig, Serializable {    
		
			// abstract method
			abstract void service(ServletRequest req, ServletResponse res); 
			
			void init() {
			// Its implementation
			}
			// other method related to Servlet
		}

> 当HttpServlet类继承GenericServlet时，它提供了service方法的实现：

	public class HttpServlet extends GenericServlet {
	    void service(ServletRequest req, ServletResponse res) {
	        // implementation
	    }
	 
	    protected void doGet(HttpServletRequest req, HttpServletResponse resp) {
	        // Implementation
	    }
	 
	    protected void doPost(HttpServletRequest req, HttpServletResponse resp) {
	        // Implementation
	    }
	 
	    // some other methods related to HttpServlet
	}
	
#### 接口

> 接口就是一个规范和抽象类比较相似。它只管做什么，不管怎么做。通俗的讲，接口就是某个事物对外提供的一些功能的声明，其定义和类比较相似，只不过是通过interface关键字来完成。

> **其中重要的几个知识点：**  
>    1.接口中的所有属性默认为：public static final xxxx；(当接口中声明的属性，在继承接口的类中修改属性值的时候会出现编译异常："**The final field xxx.xx cannot be assigned**")  
>    2.接口中的所有方法默认为：public abstract xxxx；(当给接口中声明的方法写上方法体的时候会出现编译异常：“**Abstract methods do not specify a body**”)  
>    3.接口不再像类一样用关键字 extends去“**继承**”，而是用 implements 去“**实现**”，也就是说类和接口的关系叫做实现，（例如：A类实现了B接口，那么A成为了B接口的实现类。而类与类之间的继承的话，叫做A类继承了B类，其中B类即为A类的父类）。实现接口与类的继承比较相似。

> 接口是抽象方法的集合。如果一个类实现了某个接口，那么它就继承了这个接口的抽象方法。这就像契约模式，如果实现了这个接口，那么就必须确保使用这些方法。接口只是一种形式，接口自身不能做任何事情。以Externalizable接口为例：

	public interface Externalizable extends Serializable {
 
	    void writeExternal(ObjectOutput out) throws IOException;
	 
	    void readExternal(ObjectInput in) throws IOException, ClassNotFoundException;
	}

> 当你实现这个接口时，你就需要实现上面的两个方法：

	public class Employee implements Externalizable {
 
	    int employeeId;
	    String employeeName;
	 
	    @Override
	    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
	        employeeId = in.readInt();
	        employeeName = (String) in.readObject();
	 
	    }
	 
	    @Override
	    public void writeExternal(ObjectOutput out) throws IOException {
	 
	        out.writeInt(employeeId);
	        out.writeObject(employeeName);
	    }
	}

> **抽象类和接口的对比**  
![avatar](https://github.com/hyblogs/blogs/blob/master/Java_Images/Interview_02/19.png)

> **什么时候使用抽象类和接口**  
> 1.如果你拥有一些方法并且想让它们中的一些有默认实现，那么使用抽象类吧。  
> 2.如果你想实现多重继承，那么你必须使用接口。由于Java不支持多继承，子类不能够继承多个类，但可以实现多个接口。因此你就可以使用接口来解决它。（存在异议，关联到多态，继承的意义，谨慎使用这句话）  
> 3.如果基本功能在不断改变，那么就需要使用抽象类。如果不断改变基本功能并且使用接口，那么就需要改变所有实现了该接口的类。  
> 4.简单说明：类是对事物的抽象，抽象类是对类的抽象，接口是对抽象类的抽象。接口用于抽象事物的特性，抽象类用于代码复用.  

> **Java8中的默认方法和静态方法**  
> Oracle已经开始尝试向接口中引入默认方法和静态方法，以此来减少抽象类和接口之间的差异。现在，我们可以为接口提供默认实现的方法了并且不用强制子类来实现它。

+ **说说反射的用途及实现**  
_答_：  
> 反射最重要的用途就是开发各种通用框架。

_解析_：  

> 资料参考来源:https://www.cnblogs.com/xylgp/p/6256582.html , https://blog.csdn.net/jinknow/article/details/80246715

> **反射机制**：JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。

> **java反射框架主要提供以下功能：**

> 1.在运行时判断任意一个对象所属的类。 
> 2.在运行时构造任意一个类的对象。  
> 3.在运行时判断任意一个类所具有的成员变量和方法（通过反射甚至可以调用private方法）。  
> 4.在运行时调用任意一个对象的方法。  

> **主要用途：**

> 　　反射最重要的用途就是开发各种通用框架。

> **基本反射功能的实现(反射相关的类一般都在java.lang.relfect包里)：**

> _获的class对象_  
使用Class类的forName静态方法，例如：Class.forName("xxxx");  
直接获取某一个类的class，例如Object.class;  
调用某个对象的getClass()方法，例如：new Object().getClass();  

> _判断是否为某个类的实例_  
用isstanceof关键字来判断是否为某个类的实例.  

> _创建实例_  
> 使用Class对象的newInstance()方法创建Class对象对应类的实例。  
先通过Class对象获取指定的构造器Constructor，再调用ConStructor对象的newInstance()方法创建实例。  

> _获取方法_  
getDeclareMethods().  
获取构造器信息.  
getConstructors().  
获取类的成员变量（字段）信息.  
getFields();访问共有的成员变量.  
getDeclareFields();得到所有的字段，包括公共，保护，默认（包）和私有变量，但不包括继承的字段。  

> _调用方法_  
invoke();  
利用反射创建数组.  
Array.newInstance().  

> **1、Class类理解**  
> _基础_：Class类实例是Java运行时的类(enum/interface/annotation/class)，每个Java类运行时在JVM中表现为一个class对象.  
> _JVM中表现class对象的类型_：boolean，byte，char，short，int，long，float，double，void，array，enum，interface，annotation，class.  

> **2、获取Class类对象--实例化**  
> a、类名.class  
> b、类型.getClass()  
> c、Class.forClass("路径/类名")  

> **3、常用API**  

	public static Class<?> forName(String className) ：natice 方法，动态加载类
	public T newInstance() ：根据对象的class新建一个对象，用于反射
	public ClassLoader getClassLoader() ：获得类的类加载器Bootstrap
	public String getName() ：获取类或接口的名字(包名、类名)。记住enum为类，annotation为接口
	public String getSimpleName()：获取类或接口的名字（类名）
	public native Class getSuperclass()：获取类的父类，继承了父类则返回父类，否则返回java.lang.Object
	public java.NET.URL getResource(String name) ：根据字符串获得资源
	public Constructor<?>[] getConstructors() ：获得所有的构造函数。
	public boolean isEnum() ：判断是否为枚举类型。
	public native boolean isArray() ：判断是否为数组类型。
	public native boolean isPrimitive() ：判断是否为基本类型。
	public boolean isAnnotation() ：判断是否为注解类型。
	public Package getPackage() ：反射中获得package，如java.lang.Object 的package为java.lang。
	public native int getModifiers() ： 反射中获得修饰符，如public static void等 。
	public Field getField(String name)：反射中获得域成员。
	public Field[] getFields() :获得域数组成员。    
	public Method[] getMethods() ：获得方法。
	public Method getDeclaredMethod(String name, Class<?>... parameterTypes)：加个Declared代表本类，继承，父类均不包括。
	public Constructor<?>[] getConstructors() ：获得所有的构造函数。

> **4.操作实例**
	
	import java.lang.reflect.Constructor;
	import java.lang.reflect.Field;
	import java.lang.reflect.InvocationTargetException;
	import java.lang.reflect.Method;
	import java.lang.reflect.Modifier;
	import org.junit.Test;
	import com.common.model.user.UserInfo;
	
	/**
	 * 反射测试
	 */
	//@RunWith(SpringJUnit4ClassRunner.class)  
	//@ContextConfiguration(locations = {"classpath*:spring/spring-context.xml"})
	public class ReflectTest extends BaseTest{
	
	    @Test
	    public void test(){
	        try {
	            UserInfo info = new UserInfo();
	            //获取Class实例和类名
	            System.out.println("--------------获取Class实例和类名--------------");
	            Class<?> class1 = UserInfo.class;
	            Class<?> class2 = info.getClass();
	            Class<?> class3 = Class.forName("com.common.model.user.UserInfo");
	            
	            System.out.println("class1--包名、类名:"+class1.getName());
	            System.out.println("class2--包名、类名:"+class2.getName());
	            System.out.println("class3--包名、类名:"+class3.getName());
	            System.out.println("class3--类名:"+class3.getSimpleName());
	            
	            
	            //获取父类及继承的接口
	            System.out.println("---------------获取父类及继承的接口-------------");
	            Class<?> parentClass = class1.getSuperclass();
	            System.out.println("父类："+parentClass.getName());
	            Class<?>[] interfaces = class1.getInterfaces();
	            for(int i=0;i<interfaces.length;i++){
	                System.out.println(i+1+":"+interfaces[i].getName());
	            }
	            
	            //获取类的全部构造函数
	            System.out.println("---------------获取类的全部构造函数-------------");
	            Constructor<?>[] cons =  class1.getConstructors();
	            for(int i=0;i<cons.length;i++)
	            {
	                StringBuffer buffer = new StringBuffer("cons"+i+1+":");
	                Class<?>[] clazz = cons[i].getParameterTypes();
	                for(int j=0;j<clazz.length;j++)
	                {
	                    buffer.append(clazz[j].getName());
	                }
	                System.out.println(buffer.toString());
	            }
	            
	            //反射实例化对象
	            System.out.println("---------------反射实例化对象-------------");
	            UserInfo userInfo = (UserInfo) class1.newInstance();
	            userInfo.setRealName("张三");
	            System.out.println(userInfo.getRealName());
	            
	            //获取本类的全部属性
	            System.out.println("----------------获取本类的全部属性------------");
	            Field[] field = class1.getDeclaredFields();
	            for(int i=0; i<field.length;i++)
	            {
	                //获取权限修饰符
	                int mo = field[i].getModifiers();
	                String priv = Modifier.toString(mo);
	                //获取属性类型
	                Class<?> type = field[i].getType();
	                System.out.println(priv+"--"+type.getName()+"--"+field[i].getName());
	            }
	            
	            //获取本类和父类的全部属性
	            System.out.println("----------------获取本类和父类的全部属性------------");
	            Field[] attrs = class1.getFields();
	            for(int i=0; i<attrs.length;i++)
	            {
	                //获取权限修饰符
	                int mo = attrs[i].getModifiers();
	                String priv = Modifier.toString(mo);
	                //获取属性类型
	                Class<?> type = attrs[i].getType();
	                System.out.println(priv+"--"+type.getName()+"--"+attrs[i].getName());
	            }
	            
	            //获取某个类的全部方法
	            System.out.println("获取某个类的全部方法");
	            Method[] methods = class1.getDeclaredMethods();
	            for(Method method:methods){
	                //获取权限
	                int modifier = method.getModifiers();
	                String priv = Modifier.toString(modifier);
	                //获取返回值类型
	                Class<?> returnClass = method.getReturnType();
	                String returnStr = returnClass.getName();
	                //获取方法
	                String methodName = method.getName();
	                //获取入参
	                Class<?>[] pars = method.getParameterTypes();
	                StringBuffer buffer = new  StringBuffer("(");
	                for(Class<?> par:pars){
	                    buffer.append(par.getTypeName());
	                    buffer.append(" ");
	                    buffer.append(par.getName());
	                    buffer.append(",");
	                }
	                String params = buffer.append(")").toString();
	                System.out.println(priv+" "+returnStr+" "+methodName+params);
	            }
	            
	            //获取本类、父类的全部方法
	            System.out.println("---------------获取本类、父类的全部方法--------------");
	            Method[] localMethods = class1.getMethods();
	            for(Method method:localMethods){
	                //获取权限
	                int modifier = method.getModifiers();
	                String priv = Modifier.toString(modifier);
	                //获取返回值类型
	                Class<?> returnClass = method.getReturnType();
	                String returnStr = returnClass.getName();
	                //获取方法
	                String methodName = method.getName();
	                //获取入参
	                Class<?>[] pars = method.getParameterTypes();
	                StringBuffer buffer = new  StringBuffer("(");
	                for(Class<?> par:pars){
	                    buffer.append(par.getTypeName());
	                    buffer.append(" ");
	                    buffer.append(par.getName());
	                    buffer.append(",");
	                }
	                String params = buffer.append(")").toString();
	                System.out.println(priv+" "+returnStr+" "+methodName+params);
	            }
	            
	            //反射执行方法--getDeclaredMethod("方法名",入参类型.class,...,入参类型.class)
	            System.out.println("--------------反射执行方法------------");
	            Method setRealName = class1.getDeclaredMethod("setRealName", String.class);
	            UserInfo user = new UserInfo();
	            setRealName.invoke(user, "刘广平");
	            Method getRealName = class1.getDeclaredMethod("getRealName");
	            String realName = (String) getRealName.invoke(user);
	            System.out.println(realName);
	            
	            //反射操作属性
	            System.out.println("--------------反射操作属性------------");
	            UserInfo userPar = (UserInfo) class1.newInstance();
	            Field realNamePar = class1.getDeclaredField("realName");//获取属性对象
	            realNamePar.setAccessible(true);
	            realNamePar.set(userPar, "张三");
	            System.out.println(realNamePar.get(userPar));
	            System.out.println(userPar.getRealName());
	        } catch (ClassNotFoundException e) {
	            e.printStackTrace();
	        } catch (InstantiationException e) {
	            e.printStackTrace();
	        } catch (IllegalAccessException e) {
	            e.printStackTrace();
	        } catch (NoSuchMethodException e) {
	            e.printStackTrace();
	        } catch (SecurityException e) {
	            e.printStackTrace();
	        } catch (IllegalArgumentException e) {
	            e.printStackTrace();
	        } catch (InvocationTargetException e) {
	            e.printStackTrace();
	        } catch (NoSuchFieldException e) {
	            e.printStackTrace();
	        }
	    }
	}

> **注意：**

> 　　由于反射会额外消耗一定的系统资源，因此如果不需要动态地创建一个对象，那么就不需要用反射。  
> 　　另外，反射调用方法时可以忽略权限检查，因此可能会破坏封装性而导致安全问题。	
