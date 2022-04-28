# java基础知识汇总

## 目录

* [多线程](# 19、多线程)
* [常用类](# 20、常用类)
* [集合](# 23、集合)
* [泛型](# 泛型)
* [IO流](# IO流)
* [反射](# 反射)
* [java8新特性](# java8新特性)
* [end](# end)



### 19、多线程

> 1、线程的生命周期、以及切换到各个状态所用到的方法
>
> [![HB9YnJ.png](https://s4.ax1x.com/2022/02/12/HB9YnJ.png)](https://imgtu.com/i/HB9YnJ)



> 2、同步代码块中的同步监视器和共享数据的理解
>
> * 共享数据和同步监视器都必须唯一
> * 同步监视器是对象并且多个线程都公用一个同步监视器
> * 共享数据就是多个线程一起共享的数据
>
> 同步方法和静态同步方法
>
> * 同步方法中的同步监视器是：this（当前类的对象）
> * 静态同步方法中的的同步监视器是：当前类本身（类.class）



> 3、sleep()和wait()的区别
>
> * （同）二者都会进入阻塞状态
> * （异）是否释放同步监视器：sleep()方法不会释放当前线程占用的同步监视器；wait()方法会释放当前线程的同步监视器
> * 声明的位置不同：sleep()方法是声明在Thread类中的；wait()方法是声明在Object类中。
> * 使用的要求不同：sleep()可以在任何地方使用；wait()只能在同步代码块或者同步方法中使用。



> 4、写一个线程安全的懒汉式



> 5、创建多线程有哪几种方式？
>
> * 继承Thread类
> * 实现Runnable接口
> * 实现Callable接口
> * 使用线程池 （提高了线程响应速度、提高了资源的重用率、方便线程管理）



#### 线程的同步机制

> 1、背景
>
> * 为了解决线程不安全问题
>
> 2、java中的解决方法
>
> * 同步机制
> * 同步代码块（synchronized(){}）
> * （静态）同步方法
> * JDK5.0新增的方法：Lock锁
>
> 3、synchronized和Lock的异同？
>
> * 同： 都可以解决线程安全问题
> * 异： synchronized机制在执行完同步代码后会自动释放同步监视器
> * ​         Lock需要手动启动(lock.lock)、结束同步需要手动 停止(lock.unlock)
>
> 3、利弊
>
> 4、面试题：java是如何解决线程安全问题的，有哪几种解决方法，并对比异同。





## 20、常用类



> 1、String概述
>
> * 使用双引号括起来
> * String的底层数组value[]是被final修饰
> * String类也被final修饰以此不可以被继承
> * String类实现了Comparable接口可以比较大小
> * String类实现了Serializable接口可以序列化
> * String类型通过字面量声明时，此时字符串值声明在字符串常量池中
> * 字符串常量池中是不会存在两个相同内容的字符串（equals方法比较内容，返回true则相同）



> 2、String的不可变性
>
> * 对原有的字符串进行修改操作必须保持原来的数组不变，要重新指定一个新的内存区域赋值（比如：原字符串 + 一个字符串 、 replace方法）
> * 底层char数组被final修饰不可变
>
> 代码举例：
>
> ~~~java
> String s1 = "hello";
> String s2 = "hello";
> s1 = "abc";
> sout(s1); //abc
> sout(s2); //hello
> sout(s1 == s2) //地址值不同f
> ~~~
>
> 



> 1、String与char[]数组相互转换
>
> 2、getBytes()编码和解码



> StringBuffer
>
> * StringBuffer的方法通常会返回一个StringBuffer对象，源码中return this也就是调用方法的StringBuffer自己



> 1、String 、StringBuffer、StringBuilder区别
>
> * String：来自jdk1.0，不可变的字符串序列，底层是一个char[]数组
> * StringBuffer：来自jdk1.0，可变的字符串序列，底层是一个char[]数组，方法都由synchronized修饰是线程安全的，效率比StringBuilder低
> * StringBuilder：来自jdk5.0，可变的字符串序列，底层是一个char[]数组，非线程安全的，效率高
>
> 源码分析：
>
> ~~~ java
> String s = new String(); //new char[0];
> String s1 = new String("abc"); //new char[]{'a','b','c'}
> 
> StringBuffer sb = new StringBuffer(); //new char[16];
> StringBuffer sb1 = new StringBuffer("abc");//new char[16 + "abc".length()]
> 
> //问题1：
>         StringBuffer sb = new StringBuffer();
>         System.out.println(sb.length());
> 
> //问题2：扩容问题：如果要添加的数据底层数组存不下了
> 
> /*如果minimumCapacity - value.length > 0会将(value.length << 1) + 2生成一个新的数组，并将原来的数组复制到新的数组中
> value = Arrays.copyOf(value, newCapacity(minimumCapacity));*/
> ~~~
>
> 总结：
>
> * StringBuffer扩容会降低效率，为了避免扩容可以使用new StringBuffer(int capacity)
>
> 



> Date
>
> ~~~java
> //两个构造器
> Date date = new Date();
> Date date1 = new Date(long time);
> //方法
> date.getTime();
> date.toString();
> // java.util.Date  -->  java.sql.Date
> java.sql.Date date2 = new java.sql.Date(long time);
> Date date3 = new Date(date2.getTime());
> ~~~
>
> 



> 有关日期API说明
>
> jdk8之前的日期时间API有：
>
> ~~~java
> System.currentTimeMillis();
> Date date = new Date();
> Calendar instance = Calendar.getInstance();
> ~~~
>
> jdk8新增日期和时间API：
>
> ~~~java
> LocalDate ld = LocalDate.now();
> LocalDateTime ldt = LocalDateTime.now();
> LocalTime lt = LocalTime.now();
> 
> LocalDateTime of = LocalDateTime.of(2022, 2, 18, 0, 0);	
> ~~~
>
> 总结：
>
> * 新的日期/时间API中，所有的类都是不可变的，这对于多线程是有好处的（ldt.withMouths()方法会返回一个新的LocalDateTime对象不会改变原对象的属性。而JDK8之前的calender会直接改变自身的属性值具有可变性。）
> * 新的日期/时间API中，年月日都不存在偏移量（Date中年是从1900年开始，月是从0开始，周日代表1周六代表7处理起来不太方便）
>
> ~~~java
> LocalDateTime of = LocalDateTime.of(2022, 2, 18, 0, 0);//2022-02-18T00:00
> Date date = new Date(2022,2,18);//Sat Mar 18 00:00:00 CST 3922
> Date date1 = new Date(2022 - 1900,1,18);//Fri Feb 18 00:00:00 CST 2022
> ~~~
>
> * 格式化：只能将Date类格式化，不能格式化calendar
>
> ~~~java
> SimpleDateFormat sdf = new SimpleDateFormat("YYYY-MM-dd hh-mm-ss");
> String res1 = sdf.format(date);
> System.out.println(res1);
> ~~~



> comparable和comparator区别
>
> * comparable一旦确定了，不管在哪里都可以比较大小。
> * comparator临时定制比较方式。



> 结论： 
>
> * 字符串中，常量与常量拼接后的字符串仍然在存放在方法区的字符串常量池中
> * 字符串拼接时只要出现了变量，那么拼接后的字符串就会被存放到堆中



## 23、集合



> 1. list接口框架
>
> |	------	Collection接口：单列集合，用来存储一个个的对象
>
> ​	|	------	List接口：有序，可重复性数据
>
> ​		|	------	ArrayList：作为list接口的主要实现类，线程不安全，效率高，底层使用Object[] elementData数组存储数据。
>
> ​		|	------	LinkedList：插入和删除数据时，效率高于ArrayList，底层链表实现。
>
> ​		|	------	Vector：作为List接口的古老实现类，线程安全，效率低，底层Object[] elementData数组存储。
>
> ​	|	------	Set接口：存储无序的、不可重复的数据
>
> ​		|	------	HashSet：作为Set接口的主要实现类；线程不安全的；可以存储null值。
>
> ​			|	------	LinkedHashSet：作为HashSet的子类，遍历内部数据时可按照添加顺序遍历。对于频繁遍历操作效率高于HashSet
>
> ​		|	------	TreeSet：可以添加对象的指定属性，进行排序。



> 2. ArrayList源码分析
>
> > 2.1 jdk 7.0 情况下：
> >
> > ~~~java
> > ArrayList list = new ArrayLIst();
> > //底层是创建了长度为10的Object[]数组elementData
> > 
> > list.add(123);	//elementData[0] = new Integer(123);
> >     
> > list.add(11);
> > //如果容量不够，则扩容原来的1.5倍,同时将原数组中的数据复制到新数组中
> > 
> > //结论： 建议
> > ArrayList list = new ArrayList(int capacity);
> > ~~~
>
> > 2.2 jdk 8.0情况下：
> >
> > ~~~java
> > ArrayList list = new ArrayLIst();
> > //底层Object[] elementData初始化为{}，并没有创建长度为10的数组
> > 
> > list.add(123);
> > /* 第一次调用add()方法时，底层才会创建长度10的数组，并将123添加到elementData[0] */
> > // 后续添加和jdk 7.0中相同。
> > ~~~
>
> * **总结：** jdk7中的ArrayLIst的对象的创建类似于单例的饿汉模式，而jdk8中的ArrayList对象的创建类似于单例的懒汉模式，延迟了数组的创建，节省内存。



> 3. linkedList源码分析
>
> ~~~java
> LinkedList list = new LinkedList();
> //内部声明了Node类型的first和last,默认值为NULL
> list.add(123) //将123封装到Node中，创建了Node对象。
> ~~~
>
> 



> 4. Vector源码分析
>
> * jdk7和jdk8中通过 Vector() 构造器创建对象时，底层都创建了长度为10的Object[]数组。扩容时，默认扩容为原来的两倍。



> ArrayList、LinkedList、Vector三者的异同？
>
> 同： 都是List的实现类、都具有相同的存储性质（有序，可重复）
>
> 异： 



> 区分remove(int index) 和 remove(Object obj)



> Set的 无序性 和 不可重复性
>
> 1. 无序性：数据存放在底层数组中不是按照数组的索引顺序存储的，但也不是随机存储的。数据存放是按照每个数据计算出来的哈希值来确定存放位置（索引位置）。
>
> 2. 不可重复性：内容不可相同，最后将会通过equals()方法来比较内容是否相同，若为true则不可插入。相同元素只能添加一个。



> Set集合元素添加过程（HashSet为例）
>
> 向HashSet中添加元素a，首先调用HashCode方法计算a的哈希值，此哈希值通过某种映射关系可以找到元素将要存放的位置（索引位置），判断此位置上是否有元素存在：
>
> * 若无，则直接插入
> * 若有其他元素b（或者以链表的形式存在的多个元素），则依次比较a和b的hash值是否相同：
>   * 若hash值不同，则元素添加成功
>   * 若hash值相同则，比较equals()方法：返回ture则添加失败，false则添加成功。
>
> 总结：
>
> jdk7 ：元素a存放到数组中，指向原来的元素（新即将插入的元素的中的next等于原来的元素）
>
> jdk8： 元素a存放到数组中，原来的元素指向a（）
>
> （七上八下）
>
> HashSet底层：数组 + 链表  （前提：jdk7）



> Map : 双列数据，存储key-value键值对数据
>
> * HashMap：map的主要实现类，是线程不安全的，效率高，可以存储null的key和value。
>   * LinkedHashMap：可以按照添加的顺序，顺序输出元素，在hashmap的基础上增加了一对指针，分别指向上一个和下一个元素。对于频繁的遍历操作效率要比HashMap高。
> * TreeMap：保证按照添加的key - value进行排序，实现排序遍历。
> * Hashtable：作为古老实现类，是线程安全的，效率较低，不可以存储null的key和value。
>   * Properties：常用来处理配置文件，key和value都是String类型。





> Map结构理解
>
> * Map中的key：是无序的、不可重复的、使用Set存储所有的key   -->  key所在的类要重写equals()方法和hashCode()方法（HashMap中）
> * Map中的value：无序的、可重复的，使用Collection存储所有的value  -->  value所在的类要重写equals()方法
> * 一个键值对构成了一个Entry对象
> * Map中的entry：无序的、不可重复的，使用Set存储所有的entry





> HashMap() 的底层实现原理？ jdk7中
>
> * HashMap  map  =  HashMap()调用构造器后，会创建一个长度为16的 Entry [] table
>
> * map.put(key1 , value1)方法
>
> 首先调用key1所在类的hashCode()计算key1的哈希值，此哈希值通过某种映射后得到在Entry数组中的存放位置。如果此时存放位置上的数据为空，则添加成功。
>
> 否则比较key1和已经存在的一个或多个数据的哈希值：
>
> * 若不相同则添加
> * 若相同则，继续比较，调用key1所在类的equals方法。如果为false则添加成功。如果为true则使用value1 = value2（替换值）
>
> 扩容问题：
>
> * 当数组长度大于等于临界值时（size >= threshold）并且存放位置非空时，默认扩容原来的两倍，并将原有数据复制过来。
>
>    HashMap() 的底层实现原理？ jdk8中
>
> *  相比较7而言调用空构造器是没有创建一个长度为16的数组
> * 8 的底层数组是 Node[ ] ，而非Entry[ ]
> * 当调用map.put(key,value)时会创建一个长度为16的数组
> * 7的底层是  数组 + 链表   8 的底层是  数组  +  链表  +  红黑树
> * 当数组中某一索引位置上元素的个数  >  8 ，并且当前数组长度  >  64时（若 <  64则先去扩容），此时索引位置上的所有数据改为使用红黑树存储结构



> DEFAULT_INITIAL_CAPACITY : hashmap默认容量，16
>
> DEFAULT_LOAD_FACTOR：HashMap默认加载因子：0.75
>
> thredshold : 扩容临界值，=容量* 填充因子：16 * 0.75 = > 12
>
> jdk8中新增：
>
> TREEIFY_THRESHOLD：Bucket中链表长度大于该默认值，转化为红黑树（默认值8）
>
> MIN_TREEIFY_CAPACITY：桶中的Node被树化时的最小hash表容量为64



### 泛型



> * 静态方法中不能使用类的泛型，从面向对象角度考虑，静态方法在类创建之前就加载了，而泛型要在创建对象时才确定。
> * 异常类不能是泛型（因为要继承的Exception类不是泛型的）
> * 泛型类的数组不能new T[10];编译不通过（这个时候T还是一个变量所以编译出错），可以(T[]) new Object[10];（但此时后面存入的数据需要是T类型的不然类型转换异常）
> * 泛型方法所属的类是不是泛型类都没有关系（public <E> List<E> copyFromArrayToList(E[] list)）。泛型方法在调用时才指明泛型参数的类型，而不是实例化时。因此可以使用static修饰泛型函数，
> * 泛型的类型必须是类，不能是基本数据类型，当涉及到基本数据类型时可以使用包装类；默认状态下泛型是java.lang.Object类型的。
> * 泛型类在实例化时最好指定类型，不然默认为java.lang.Object



> 通配符 ？
>
> ~~~java
> List<?> list = null;
> List<String> list1 = new ArrayList<String> ();
> List<Integer> list2 = new ArrayList<Integer> ();
> list1 = list2; // 编译不通过，不知子父类关系，不能赋值，可使用通配符
> list = list1;
> list = list2;
> //对于list<?>来讲，不可以添加任何数据，除了null
> list.add("aaa");  //编译不通过，通配符不能赋值
> list.add(null);
> //通配符可作为方法的形式参数来操作
> print(list1);
> print(list2);
> ~~~
>
> * 通配符允许读取数据，读取的数据为Object。
> * 通配符写入数据只能add( null )。



> 限制通配符 
>
> ~~~ java
>         //Person是Student的父类
>         //限制通配符
>         List<? extends Person> list1 = null; //? <= Person
>         List<? super Person> list2 = null;  //? >= Person
> 
>         List<Student> list3 = null;
>         List<Person> list4 = null;
>         List<Object> list5 = null;
> 
>         //测试限制通配符的范围
>         list1 = list3;
>         list1 = list4;
>         list1 = list5;  //编译不通过
> 
>         list2 = list3;  //编译不通过
>         list2 = list4;
>         list2 = list5;
> ~~~
>
> 



[![q9NnZ4.png](https://s1.ax1x.com/2022/03/17/q9NnZ4.png)](https://imgtu.com/i/q9NnZ4)



[![q9NKo9.png](https://s1.ax1x.com/2022/03/17/q9NKo9.png)](https://imgtu.com/i/q9NKo9)





### IO流



> 流的分类
>
> * 按数据单位可分为字符流（2byte = 16bit）和字节流（1byte = 8bit）
>   * 字符流：文本数据的io操作，一个char两个byte，一个汉字两个byte
>   * 字节流 ：非文本数据
> * 按方向有：输入流和输出流
> * 按角色不同可分为：节点流（直接操作文件，文件流）和处理流（）
>   * 节点流：FileInputeStream、FileOutputStream、FileReader、FileWriter
>   * 处理流（主要）：缓冲流（BufferedInputStream、BufferedOutputStream、BufferedReader、BufferedWriter）
> * 字节流和字符流的两个输入输出流都是抽象类都不可以实例化
>   * InputStream 和 OutputStream
>   * Reader 和 Writer
>
> 



> 节点流中的输入字符流FileReader
>
> * read()方法：读取单个字符，返回为int类型，代表该字符的ASCII码值
> * 异常处理：为了保证流资源可以正常关闭，通过try-catch-finally来进行流的关闭工作



[![q9JAxO.png](https://s1.ax1x.com/2022/03/17/q9JAxO.png)](https://imgtu.com/i/q9JAxO)



[![q9NpZQ.png](https://s1.ax1x.com/2022/03/17/q9NpZQ.png)](https://imgtu.com/i/q9NpZQ)



> RandomAccessFile使用
>
> * 直接继承java.lang.Object类，实现了DataInput 和 DataOutput接口
> * 既可以作为一个输入流，又可以作为一个输出流
> * 作为输出流：当写出的文件不存在则会自动创建，如果写出到的文件存在，则会对原有内容进行覆盖（从文件开头开始进行覆盖）



> 对象序列化的理解
>
> * 序列化是将对象转化成二进制流，并且可以永久保存到磁盘上或者通过网络发送到另一个网络节点
> * 反序列化是指当其它程序获取到了这种二进制流，就可以恢复成原来的java对象



> 对象想要序列化，需要满足的条件
>
> * 实现接口Serializable 接口
> * 对象所在的类提供常量：序列化版本号
> * 要求对象的属性都可以序列化（基本数据类型、String：本身就可序列化）



> NIO -- new IO or No-Blocking IO
>
> * 目的与IO相同，但是使用方式完全不相同，NIO支持面向缓冲区的，而IO是面向流的、NIO是基于通道的IO操作。
> * NIO是以更加高效的方式进行读写操作
> * java1.4发布NIO1.0，jdk7时发布2.0（增强了文件处理和文件特性的支持）



> Path的使用
>
> * jdk7提出的
> * Path替换原有的File类（File类中有些方法出问题只返回False不报异常很难排查问题，Path则直接抛异常）



> FIles工具类
>
> * jdk7提出的
> * 工具包



### 网络通信



> 1. 端口号和IP地址的组合得到一个网络套接字：socket
>
> * 网络通信也被称为：socket通信
>
> 2. 端口号
>
> * 不同的进程有不同的端口号
> * 范围：别规定为一个16位的整数：0 ~ 65535



> 一、实现网路通信要解决的两个主要问题
>
> * 如何找到网络上一台或者多台主机后定位主机中的某一个进程
> * 如何保证可靠数据传输
>
> 二、网络通信的两个要素
>
> * 问题一：IP和对应的端口号
> * 问题二：TCP/IP
>
> 三、IP和端口号
>
> * java中使用InetAddress类代表IP





### 反射



> 反射机制与面向对象中的封装性是不是矛盾？如何看待两个技术？
>
> 不矛盾，封装性主要体现在将需要的功能暴露出来不需要的给隐藏。反射体现的是动态性，可以处理在特定情况下需要用到被隐藏的功能时使用，不然只需要使用暴露出来的功能就足以。



> java.lang.Class类的理解
>
> 1. 类的加载过程
>
>    程序经过javac.exe命令后，会生成一个或多个字节码文件（.class结尾）；
>
>    接着使用java.exe命令，将某个字节码文件解释运行，相当于将某个字节码文件加载到内存中，此过程就称为类的加载。加载到内存中的类，被称为运行时类，此时运行时类就作为Class的一个实例。
>
> 2. 换句话说，Class的实例就是一个运行时类。
>
> 3. 万事万物皆对象



> 获取Class类的四种方法
>
> 1. .class
> 2. 运行时类的对象.getClass()
> 3. 调用Class的静态方法Class.forName("study.test.Person")
> 4. 使用类的加载器：ClassLoader
>
> * 上面三种创建方式所获取的运行时类都是相同的
> * 加载到运行时的类，会缓存一段时间，在此期间通过不同方式获取运行时类



> 类的加载过程
>
> 1. 将类加载到内存中
> 2. 链接：链接时属性的默认值为0
> 3. 初始化后，由<clinit>()方法执行决定此时属性的值为多少





> 常用获取class类的三种实例
>
> ~~~java
> Class clazz = String.class;
> Class clazz = 对象.getClass();
> Class clazz = Class.forName(String classpath);
> ~~~
>
> 



> 对于Class类的理解
>
> Class类对应着一个加载到内存中的运行时类



> 动态代理类
>
> ~~~java
> package study.test;
> 
> import java.lang.reflect.InvocationHandler;
> import java.lang.reflect.Method;
> import java.lang.reflect.Proxy;
> 
> /**
>  * @author Xavier
>  * @create 2022-03-24-20:16
>  */
> public class ActiveProxy {
>     public static void main(String[] args) {
>         SuperMan superMan = new SuperMan();
>         //代理类的对象proxyInstance
>         Human proxyInstance = (Human) ProxyFactory.getProxyInstance(superMan);
>         //通过代理类对象调用方法时，会自动调用被代理类中的同名方法
>         String belief = proxyInstance.getBelief();
>         System.out.println(belief);
>         proxyInstance.eat("鸡腿");
>     }
> }
> 
> interface Human{
>     void eat(String food);
>     String getBelief();
> }
> //被代理类
> class SuperMan implements Human{
> 
>     @Override
>     public void eat(String food) {
>         System.out.println("吃饭吃" + food);
>     }
> 
>     @Override
>     public String getBelief() {
>         return "I am SuperIronMan";
>     }
> }
> //代理类
> class ProxyFactory{
>     //根据被代理类obj,动态返回一个代理类。
>     public static Object getProxyInstance(Object obj){
> 
>         MyInvocationHandler handler = new MyInvocationHandler();
>         handler.bind(obj);
>         //通过代理类调用方法时，如何动态的去调用被代理类中的同名方法
>         //创建动态代理类的对象
>         //回调handler中的invoke方法
>         return Proxy.newProxyInstance(obj.getClass().getClassLoader(), obj.getClass().getInterfaces(),handler);
>     }
> 
> }
> 
> class MyInvocationHandler implements InvocationHandler{
> 
>     private Object obj;
> 
>     public void bind(Object obj){
>         this.obj = obj;
>     }
> 
>     //当通过代理类的对象调用方法a时，就会自动的调用如下的方法
>     //将被代理类要执行的方法a的功能声明在invoke中
>     @Override
>     public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
>         //method:代理类对象调用的方法，也就是被代理类要调用的方法
>         //obj：被代理类的对象
>         //args:方法的参数
>         Object res = method.invoke(obj, args);
>         //代理类对象调用invoke方法的返回值
>         return res;
>     }
> }
> ~~~





### java8新特性



> lambda表达式 和  方法引用
>
> 1.方法引用使用情景：当要传递给lambda体的操作，已经有实现的方法了，就可以使用方法引用
>
> 2.方法引用，本质是Lambda表达式，Lambda表达式作为函数式接口的实例。所以方法引用也是函数式接口的实例。
>
> 3.使用格式：  类（对象） ::  方法名
>
> 4.具体有以下三种
>
> 对象 :: 非静态方法
>
> 类 :: 静态方法
>
> 类 ::  非静态方法
>
>  5.使用要求：要求接口函数中的抽象方法的形参列表和返回值类型与方法引用的方法的形参列表和返回值类型相同！
>
> ~~~ java
> package study.test;
> 
> import java.io.PrintStream;
> import java.util.Comparator;
> import java.util.function.Consumer;
> 
> /**
>  * @author Xavier
>  * @create 2022-03-27-16:52
>  */
> public class LambdaTest {
> 
>     public static void main(String[] args) {
>         LambdaTest lt = new LambdaTest();
> //        lt.test1();
> //        lt.test2();
>         lt.test3();
>     }
> 
>     /**
>      * 情况一：对象 :: 实例方法
>      * Consumer中的void accept(T t);
>      * PrintStream中的void println(T t);
>      */
>     public void test1(){
>         Consumer<String> con1 = str -> System.out.println(str);
>         con1.accept("我是Lambda函数");
>         System.out.println("******************************");
>         PrintStream out = System.out;
>         Consumer<String> con2 = out :: println;
>         con2.accept("我是方法引用");
>     }
> 
>     /**
>      * 情况二：类 :: 静态方法
>      * Comparator中的int compare(T t1, T t2);
>      * Integer中的int compare(T t1, T t2);
>      */
>     public void test2(){
>         Comparator<Integer> com1 = (a,b) -> Integer.compare(a,b);
>         System.out.println(com1.compare(12, 13));
>         System.out.println("**********************************");
> 
>         Comparator<Integer> com2 = Integer::compare;
>         System.out.println(com2.compare(13,12));
>     }
> 
>     /**
>      * 情况三：类 :: 非静态方法
>      * Comparator中的int compare(T t1, T t2);
>      * String中的int t1.compareTo(t2);
>      */
>     public void test3(){
>         Comparator<String> com1 = (t1,t2) -> t1.compareTo(t2);
>         System.out.println(com1.compare("abc","abd"));
>         System.out.println("**************");
>         Comparator<String> com2 = String :: compareTo;
>         System.out.println(com2.compare("abc","abe"));
>     }
> }
> 
> 
> 
> ~~~
>
> 



> Stream API
>
> 1.Stream 的操作三步骤
>
> * 创建Stream：一个数据源（集合、数组），获取一个流
> * 中间操作：对数据源的数据进行处理
> * 终止操作：一旦执行终止操作就执行中间操作，并产生结果。之后，不会再被使用



> Stream的创建方法
>
> * 使用集合创建：list.stream() /  list.parallelStream()
> * 使用数组创建:  Arrays.stream(arr)
> * 使用Stream.of()方法：Stream<Integer>   stream  =   stream.of(1,2,3,4,5)  
> * 创建无限流：Stream.iterate()  /   Stream.generate()



> Stream 的中间操作
>
> 1.筛选与切片
>
> filter()、limit()、skip()、distinct()；distinct筛选,通过流所产生元素的hashCode()和equals()去除重复元素
>
> 2.映射
>
> map()
>
> 3.排序
>
> sort() 、sort(Comparator)



> Stream的终止操作
>
> 1.匹配与查找
>
> allMatch() 、 anyMatch() 、noneMatch、findFirst、findAny、count、max、min、forEach
>
> 2.归约
>
> reduce
>
> 3.收集
>
> collect



> java8中的optional可以避免空指针的出现
>
> 1.创建一个空指针异常情况：两个类在其中一个类的构造器中实例化另一个类，函数调用时使用空构造器后调用另一个类的方法就会产生空指针（因为此时另一个类为null）。
>
> 2.optional相当于包装类，通过of()或者ofNullable()方法可以获得一个Optional类型的实例，其中的orElse()方法可以防止空指针

# end

[目录](# 目录)
