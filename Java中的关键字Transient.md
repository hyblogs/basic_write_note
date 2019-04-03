# Transient关键字
>transient的作用及使用方法，官方解释为：<br>
Variables may be marked transient to indicate that they are not part of the persistent state of an object.  

## 先解释下Java中的对象序列化
>在讨论transient之前，有必要先搞清楚Java中序列化的含义；<br>
&emsp;&emsp;Java中对象的序列化指的是将对象转换成以字节序列的形式来表示，这些字节序列包含了对象的数据和信息，
一个序列化后的对象可以被写到数据库或文件中，也可用于网络传输，一般当我们使用缓存cache（内存空间不够有可能会本地存储到硬盘）
或远程调用rpc（网络传输）的时候，经常需要让我们的实体类实现Serializable接口，目的就是为了让其可序列化。
当然，序列化后的最终目的是为了反序列化，恢复成原先的Java对象，要不然序列化后干嘛呢，所以序列化后的字节序列都是可以恢复成Java对象的，
这个过程就是反序列化。

## 关于transient关键
>Java中transient关键字的作用，简单地说，就是让某些被修饰的成员属性变量不被序列化，这一看好像很好理解，就是不被序列化，
那么什么情况下，一个对象的某些字段不需要被序列化呢？如果有如下情况，可以考虑使用关键字transient修饰：<br>
1、类中的字段值可以根据其它字段推导出来，如一个长方形类有三个属性：长度、宽度、面积（示例而已，一般不会这样设计），那么在序列化的时候，面积这个属性就没必要被序列化了；</br>
2、其它，看具体业务需求吧，哪些字段不想被序列化；<br>
PS：记得之前看HashMap源码的时候，发现有个字段是用transient修饰的，我觉得还是有道理的，确实没必要对这个modCount字段进行序列化，
因为没有意义，modCount主要用于判断HashMap是否被修改（像put、remove操作的时候，modCount都会自增），对于这种变量，一开始可以为任何值，
0当然也是可以（new出来、反序列化出来、或者克隆clone出来的时候都是为0的），没必要持久化其值。

### HashMap源码：

    /**
     * The number of key-value mappings contained in this map.
     * 当前HashMap实际储存数据(Key-Value键值对)大小
     */
    transient int size;

    /**
     * The number of times this HashMap has been structurally modified
     * Structural modifications are those that change the number of mappings in
     * the HashMap or otherwise modify its internal structure (e.g.,
     * rehash).  This field is used to make iterators on Collection-views of
     * the HashMap fail-fast.  (See ConcurrentModificationException).
     */
    transient int modCount;

>实际开发过程中，我们常常会遇到这样的问题，这个类的有些属性需要序列化，而其他属性不需要被序列化，
打个比方，如果一个用户有一些敏感信息（如密码，银行卡号等），为了安全起见，
不希望在网络操作（主要涉及到序列化操作，本地序列化缓存也适用）中被传输，这些信息对应的变量就可以加上transient关键字。
换句话说，这个字段的生命周期仅存于调用者的内存中而不会写到磁盘里持久化。

>总之，java 的transient关键字为我们提供了便利，你只需要实现Serilizable接口，将不需要序列化的属性前添加关键字transient，
序列化对象的时候，这个属性就不会序列化到指定的目的地中。

## 使用方法
>序列化的时候，将不需要序列化的属性前添加关键字transient即可。 <br>
示例：

    package hy.example;
    
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.ObjectInputStream;
    import java.io.ObjectOutputStream;
    import java.io.Serializable;
    
    class UserInfo implements Serializable {  
        private static final long serialVersionUID = 996890129747019948L;  
        private String name;  
        private transient String psw;  
    
        public UserInfo(String name, String psw) {  
            this.name = name;  
            this.psw = psw;  
        }  
    
        public String toString() {  
            return "name=" + name + ", psw=" + psw;  
        }  
    }  
    public class TestTransient {
        public static void main(String[] args) {  
            UserInfo userInfo = new UserInfo("张三", "123456");  
            System.out.println(userInfo);  
            try {  
                // 序列化，被设置为transient的属性没有被序列化  
                ObjectOutputStream o = new ObjectOutputStream(new FileOutputStream("UserInfo.txt"));  
                o.writeObject(userInfo);  
                o.close();  
            } catch (Exception e) {  
                // TODO: handle exception  
                e.printStackTrace();  
            }  
            try {  
                // 重新读取内容  
                ObjectInputStream in = new ObjectInputStream(new FileInputStream("UserInfo.txt"));  
                UserInfo readUserInfo = (UserInfo) in.readObject();  
                //读取后psw的内容为null  
                System.out.println(readUserInfo.toString());  
            } catch (Exception e) {  
                // TODO: handle exception  
                e.printStackTrace();  
            }  
        }  
    }

>运行结果：<br>

>name=张三, psw=123456 <br>
name=张三, psw=null <br>
密码字段为null，说明被标记为transient的属性在对象被序列化的时候不会被保存。<br>

### 使用小结：
>&emsp;&emsp;1，一旦变量被transient修饰，变量将不再是对象持久化的一部分，该变量内容在序列化后无法获得访问。 <br>
&emsp;&emsp;2，transient关键字只能修饰变量，而不能修饰方法和类。注意，本地变量是不能被transient关键字修饰的。<br>
&emsp;&emsp;变量如果是用户自定义类变量，则该类需要实现Serializable接口。 <br>
&emsp;&emsp;3，被transient关键字修饰的变量不再能被序列化，一个静态变量不管是否被transient修饰，均不能被序列化。 <br>
对于第三点，加上static之后，依然能把姓名输出。这是因为：反序列化后类中static型变量name的值为当前JVM中对应static变量的值，这个值是JVM中的不是反序列化得出的。下例可说明，其值时JVM中得到的而不是反序列化得到的：

    package hy.example;

    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.ObjectInputStream;
    import java.io.ObjectOutputStream;
    import java.io.Serializable;

    class UserInfo implements Serializable {  
        private static final long serialVersionUID = 996890129747019948L;  
        private static String name;  
        private transient String psw;  
    
        public UserInfo(String name, String psw) {  
            this.name = name;  
            this.psw = psw;  
        }  
    
        public static String getName() {
            return name;
        }
    
        public static void setName(String name) {
            UserInfo.name = name;
        }
    
        public String getPsw() {
            return psw;
        }
    
        public void setPsw(String psw) {
            this.psw = psw;
        }
    
        public String toString() {  
            return "name=" + name + ", psw=" + psw;  
        }  
    }  
    public class TestTransient {
        public static void main(String[] args) {  
            UserInfo userInfo = new UserInfo("张三", "123456"); 
            System.out.println(userInfo);  
            try {  
                // 序列化，被设置为transient的属性没有被序列化  
                ObjectOutputStream o = new ObjectOutputStream(new FileOutputStream("UserInfo.txt"));  
                o.writeObject(userInfo);  
                o.close();  
            } catch (Exception e) {  
                // TODO: handle exception  
                e.printStackTrace();  
            }  
            try {  
                //在反序列化之前改变name的值
                userInfo.setName("hello");
                // 重新读取内容  
                ObjectInputStream in = new ObjectInputStream(new FileInputStream("UserInfo.txt"));  
                UserInfo readUserInfo = (UserInfo) in.readObject();  
                //读取后psw的内容为null  
                System.out.println(readUserInfo.toString());  
            } catch (Exception e) {  
                // TODO: handle exception  
                e.printStackTrace();  
            }  
        }  
    }

>运行结果：<br>

>name=张三, psw=123456<br>
>name=hello, psw=null<br>

>这说明反序列化后类中static型变量name的值为当前JVM中对应static变量的值，为修改后hello，而不是序列化时的值“张三”. <br>

>最后，为什么要不被序列化呢，主要是为了节省存储空间，其它的感觉没啥好处，可能还有坏处（有些字段可能需要重新计算，初始化什么的），总的来说，利大于弊。
