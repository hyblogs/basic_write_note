#Java自动装箱与拆箱
##1.前言
>最近在看关于优化的知识，看到关于装箱与拆箱的效率问题，故整理了一下关于此的知识点

##2.概念
>什么是自动装箱和拆箱：

>自动装箱就是Java自动将原始类型值转换成对应的对象，比如将int的变量转换成Integer对象，这个过程叫做装箱，反之将Integer对象转换成int类型值，这个过程叫做拆箱。因为这里的装箱和拆箱是自动进行的非人为转换，所以就称作为自动装箱和拆箱。原始类型byte,short,char,int,long,float,double和boolean对应的封装类为Byte,Short,Character,Integer,Long,Float,Double,Boolean。

>何时发生自动装箱和拆箱：

>自动装箱和拆箱在Java中很常见，比如我们有一个方法，接受一个对象类型的参数，如果我们传递一个原始类型值，那么Java会自动将这个原始类型值转换成与之对应的对象。最经典的一个场景就是当我们向ArrayList这样的容器中增加原始类型数据时或者是创建一个参数化的类，比如下面的ThreadLocal。

	ArrayList<Integer> intList = new ArrayList<Integer>();
	intList.add(1); //autoboxing - primitive to object
	intList.add(2); //autoboxing
	ThreadLocal<Integer> intLocal = new ThreadLocal<Integer>();
	intLocal.set(4); //autoboxing
	int number = intList.get(0); // unboxing
	int local = intLocal.get(); // unboxing in Java

>由上可知，装箱是java内部自动完成，众所周知对于java的重载是以入参格式来判断，而不依赖于返回值；当发生重载时，到底会不会发生自动装箱，下面将举例说明

	public class Test {
	
	    public void test(int num){
	        System.out.println("int");
	
	    }
	
	    public void test(Integer num){
	        System.out.println("Integer");
	
	    }
	    public static void main(String[] args) {
	        Test test = new Test();
	        Integer c = 12;
	        int d = 34;
	        test.test(c);
	        test.test(d);
	    }
	}

>结果：

	Integer
	int

>由上可知，当出现这种情况时，不会发生自动装箱操作。

##3.注意事项
###3.1.null问题
>有拆箱操作时一定要特别注意封装类对象是否为null。

>代码：

	Integer a = null;
	int b = a;

结果：

	Exception in thread "main" java.lang.NullPointerException
	    at com.molly.test.Test.main(Test.java:30)
	    at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	    at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	    at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	    at java.lang.reflect.Method.invoke(Method.java:498)
	    at com.intellij.rt.execution.application.AppMain.main(AppMain.java:147)

>这两行代码是完全合法的，完全能够通过编译的，但是在运行时，就会抛出空指针异常。其中，a为Integer类型的对象，它当然可以指向null。但在第二行时，就会对a进行拆箱，也就是对一个null对象执行intValue()方法，当然会抛出空指针异常。

###3.2.等于问题
>”==“可以用于原始值进行比较，也可以用于对象进行比较，当用于对象与对象之间比较时，比较的不是对象代表的值，而是检查两个对象是否是同一对象，这个比较过程中没有自动装箱发生。进行对象值比较不应该使用”==“，而应该使用对象对应的equals方法 
实例：

	Integer a = 1233;
	int b = 1233;
	System.out.println(a == b);

>上面例子中a是对象类型，而b是基本类型，大家都知道对象类型是地址，而基本类型是值，是不相等的，但是由于引用了intValue()方法发生了自动拆箱操作,所以输出结果是true；

	Integer a = 1233;
	Integer b = 1233;
	System.out.println(a == b);

>可能大家都会认为上面的代码输出应该是true，实际却是false ,这是因为 a和b的初始化都发生了自动拆箱操作。但是处于节省内存的考虑，JVM会缓存-128到127的Integer对象。但是这个时候a、b已经超出范围，a和b实际上不是同一个对象。所以使用”==“比较返回false。那么如何a、b比较相等呢，在int的取值范围（-2的31次方到2的31次方-1）可以用： System.out.println(a.intValue() == b.intValue());来进行Integer之间比较。

>由于JVM缓存	了-128到127的Integer对象，所以下面的代码输出结果是：true。

	Integer d = 12;
	Integer e = 12;
	System.out.println(d == e);

###3.3.Integer.parseInt与Integer.valueOf比较
>在对字符串转化为整型比较时，也要注意自动拆箱问题。   
例如：

	String a = "23";
	String b = "23";
	System.out.println(Integer.valueOf(a) == Integer.valueOf(b));

>结合3.2.中的描述不能看出上面输出true 
但是当不再-128到127范围内，则输出为false这是因为 
valueOf(String s )也是Integer类的静态方法，它的作用是将形参 s 转化为Integer对象，那么如何比较转化的输出为true，可用parseInt(String s )，它是类Integer的静态方法，它的作用就是将形参 s 转化为int.也可以这样输出：

    System.out.println(Integer.parseInt(a) == Integer.parseInt(b));

>或者

    System.out.println(Integer.valueOf(a).intValue() == Integer.valueOf(b).intValue());

>或者

    System.out.println(Integer.parseInt(a) == Integer.valueOf(b));

>或者

	System.out.println(a.equals(b));

##4.备注
>因为自动装箱会隐式地创建对象，像前面提到的那样，如果在一个循环体中，会创建无用的中间对象，这样会增加GC压力，拉低程序的性能。所以在写循环时一定要注意代码，避免引入不必要的自动装箱操作。

##5.String 的比较问题
>看一下下面的两个实例

	public class Test {
	
	    public static void main(String[] args) {
	
	        String a = "ab";
	        String b = "a";
	        b +="b";
	        System.out.println(a == b);
	
	        String c = "ab";
	        String d = "a" +"b";
	        System.out.println(c == d);
	
	        String e = new String("ab");
	        System.out.println(c == e);
	
	    }
	}

>可能大家认为String是对象类型，那么三个输出都是false，实际上却不是，这里不得不说一下，字符串常量池的概念。

>当代码中出现字面量形式创建字符串对象时，JVM首先会对这个字面量进行检查，如果字符串常量池中存在相同内容的字符串对象的引用，则将这个引用返回，否则新的字符串对象被创建，然后将这个引用放入字符串常量池，并返回该引用。

>由于b是一个String变量，编译期无法确定b的值，故不会优化为一个字符串。即使我们知道b的值，但JVM认为它是个变量，变量的值只能在运行期才能确定，故不会优化。运行期字符串的+连接符相当于new，故该行代码在Heap中创建了一个内容为“计算机软件”的String对象，并返回该对象的引用，所以第一个打印是false，而第二个中d直接指向c的地址，所以打印是true，当我们使用了new来构造字符串对象的时候，不管字符串常量池中有没有相同内容的对象的引用，新的字符串对象都会创建，所以第三个打印是false。
