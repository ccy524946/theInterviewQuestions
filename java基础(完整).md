[TOC]

[ARouter](./Android/framework/ARouter.md)

1.1[== 与 equals的区别](xxx.md)

# 1.java基础知识

###   1.1. ==  与 equals

== ：它的作用是判断两个对象的地址是不是相等。即，判断两个对象是不是同一个对象（基本数据类型==比较的是值，引用数据类型==比较的是内存地址）

equals() :它的作用也是判断两个对象是否相等，但它一般有两种使用情况：

情况1：类没有覆盖equals()方法，则通过equals()比较类的两个对象试，等于通过“==”比较这两个对象。

情况2：类覆盖了equals()方法。一般，我们都覆盖equals()方法来两个对象的内容相等；若它们的内容相等，则返回true（即，认为这两个对象相等）；

**举个例子**

``` java
public class Test{
    public static void main(String[] args){
        String a = new String("ab");//a 为一个引用
        String b = new String("ab");//b 为另一个引用，对象的内容一样
        String aa = "ab";
        String bb = "ab";
        if(aa == bb){ // true
            System.out.println("aa == bb ");
        }
        if (a == b){  // false，非同一对象
            System.out.println("a==b");
        }
        if (a.equals(b)){  // true
            System.out.println("aEQb");
        }
        if (42 == 42.0) { // true
            System.out.println("true");
        }
    }
}
```

**说明**

*  String中的equals方法是被重写过的，因为object的equals方法是比较的对象的内存地址，而String的equals方法比较的是对象的值。
* 当创建String类型的对象时，虚拟机会在常量池中查找有没有已经存在的值要创建的值相同的对象，如果有就把它赋值给当前引用。如果没有就在常量池中重新创建一个String对象。

### 1.2.java 8种基本数据类型有哪些？

byte short int long float double boolean char

| 四类 | 八种    | 字节数 | 数据表示范围                             |
| ---- | ------- | ------ | ---------------------------------------- |
| 整型 | byte    | 1      | -128~127                                 |
|      | short   | 2      | -32768~32767                             |
|      | int     | 4      | -2147483648~2147483647                   |
|      | long    | 8      | -9223372036854775808~9223372036854775807 |
| 浮点 | float   | 2      | -3.403E38~3.403E38                       |
|      | double  | 4      | -1.798E308~1.798E308                     |
| 字符 | char    | 2      | 表示一个字符，如（‘a’, 'A', '0', '男'）  |
| 布尔 | boolean |        | 只有两个取值：true 和 false；            |

### 1.3.什么是装箱和拆箱？

装箱：就是自动将基本数据类型转换为包装器类型；

拆箱：就是自动将包装类型转换为基本数据类型；

**比如：把int转换成Integer,double转换为Double，等等。反之就是自动拆箱**

| 原始类型     | boolean     | char          | byte     | short     | int         | long     | float     | double     |
| ------------ | ----------- | ------------- | -------- | --------- | ----------- | -------- | --------- | ---------- |
| **封装类型** | **Boolean** | **Character** | **Byte** | **Short** | **Integer** | **Long** | **Float** | **Double** |

**示例**

``` java
Integer i = 10;//装箱
// 这个过程种会自动根据数值创建对应的Integer对象，这就是装箱
int j = i;//拆箱
//跟装箱对应，就是自动将包装类型转换为基本数据类型
```

###   1.4 查看以下代码有什么错？

```java
//1.以下代码有哪些错？
short s1 = 1;
s1 = s1+1;
/**
	在s1+1 运算会自动提升表达式的类型为int,那么将int赋值给short类型的变量s1会出现类型	  转换错误。
*/
//2.以下代码有哪些错？
short s1 = 1;
s1 +=1;
/**
	+=是java语言规定的运算符，java编译器会对它进行特殊处理，因此可以正确编译。
*/

```

### 1.5 . int 跟 Integer有什么区别？

| Integer                                                      | int                    |
| ------------------------------------------------------------ | ---------------------- |
| int的包装类                                                  | java的一种基本数据类型 |
| 必须实例化后才能使用                                         | int不需要              |
| 实际是对象的引用，当new一个Integer时，实际上时生成一个指针指向此对象 | 直接存储数据值         |
| 默认值是null                                                 | 默认值是0              |

### **1.6 .关于int跟Integer的比较**

1. 由于Integer实际上是对一个Integer对象的引用，所以两个通过new生成的Integer永远不相等（因为new生成的两个对象，其内存地址不同）；

   ``` java
   Integer i  = new Integer(100);
   Integer j  = new Integer(100);
   System.out.println(i==j);//false
   ```

2. Integer变量和int变量比较是，只要两个变量的值是相等的，则结果为true（**因为包装类Integer和基本数据类型int比较时，java会自动拆包装为int，然后进行比较，实际上就是变为两个int变量的比较**）

   ````java
   Integer i  = new Integer(100);
   int j = 100;
   System.out.println(i==j);//true
   ````

3. 非new生成的Integer变量和new Integer()生成的变量比较时，结果为false(**因为非new生成的Integer变量指向的是java常量池中的对象，而new Integer()生成的变量指向堆中新建的对象，两者在内存中的地址不同**)

   ``` java
   Integer i  = new Integer(100);
   Integer j = 100;
   System.out.println(i==j);//false
   ```

4. 对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则结果为false

   ``` java
   Integer i1 = 100;
   Integer j1 = 100;
   System.out.println(i1 == j1);//true
   ```

   ``` java
   Integer i2 = 128;
   Integer j2 = 128;
   System.out.println(i2 == j2);//false
   ```

   原因：

   java在编译Integer i1 = 100 时；会翻译成为Integer i1 = Integer.valueOf(100);而javaAPI中对Integer类型的valueOf定义如下：

   ``` java
   	/**
        * Returns an {@code Integer} instance representing the specified
        * {@code int} value.  If a new {@code Integer} instance is not
        * required, this method should generally be used in preference to
        * the constructor {@link #Integer(int)}, as this method is likely
        * to yield significantly better space and time performance by
        * caching frequently requested values.
        *
        * This method will always cache values in the range -128 to 127,
        * inclusive, and may cache other values outside of this range.
        * 该方法将始终缓存范围为-128到127的值，包括，并可能缓存此范围之外的其他值。
        * @param  i an {@code int} value.
        * @return an {@code Integer} instance representing {@code i}.
        * @since  1.5
        */
       public static Integer valueOf(int i) {
           if (i >= IntegerCache.low && i <= IntegerCache.high)
               return IntegerCache.cache[i + (-IntegerCache.low)];
           return new Integer(i);
       }
   ```

   java 对于 -128 到127之间的数，会进行缓存，Integer i = 127 时，会将127进行缓存，下次再写Integer j = 127时，就会直接从缓存中取到，就不会在new了。

### 1.7.字节和字符的区别？

| 字节               | 字符                                   |
| ------------------ | -------------------------------------- |
| 存储容量的基本单位 | 数字，字母，汉字以及其他语言的各种符号 |

1个字节 等于8 个二进制单位：一个一个字符由一个字节或多个字节的二进制单位组成

### 1.8.基本数据类型和引用类型的区别？

基本数据类型保存原始值；

引用类型保存的时引用值（**引用值就是指对象在堆中所处的位置或地址**）

### 1.9.java的四个基本特性以及多态的理解？

- java的四个基本特性：

| **抽象** | **将一类对象的共同特性总结出来构造类的过程，包括数据抽象和行为抽象两个方面。抽象只关注对象有哪些属性和行为，并不关注这些行为的细节是什么** |
| -------- | ------------------------------------------------------------ |
| **继承** | **从已有的类得到继承信息创建新类的过程，提供基础信息的类称为父类（超类，基类）得到继承信息的类称为子类（派生类）。继承让变化中的软件系统有了一个延续性。同时继承也是封装程序中可变因素的重要手段** |
| 封装     | 通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只通过已定义的接口。面向对象的本质就是将现实世界汇成一系列完全自治，封闭的对象。我们在类中编写的方法就是对实现细节的一种封装，我们编写一个类就是对数据的数据操作的封装，可以说封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口 |
| 多态     | 允许不同子类型的对象对同一消息做出不同响应                   |

- ​	多态的理解：

  方法重载（Overload）实现的是编译时的多态性（也称为前绑定）

  方法重写（Override）实现的是运行时的多态性（也称为后绑定）

  要实现多态需要做两件事情

  ​	1：方法重写（子类继承父类并重写父类中已有的或抽象方法）

  ​	2：对象造型（用父类型引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）

- 项目中对多态的应用

  举一个简单的例子，在物流信息管理系统中，有两种用户；订购客户和卖方客户，两个客户都可以登录系统，他们有相同的方法Login，但登录之后他们会进入到不同的的页面，也就是在登录的时候会有不同的操作，两种客户都继承父类的Login方法，但对于不同的对象，拥有不同的操作。

### 1.10 重载和重写的区别

* #### 重载（Overload）

  java中的方法重载发生在同一个类里面两个或者多个方法的方法名相同但是参数不同的情况

  1. 可以在一个类中也可以在继承关系的类中；
  2. 名相同；
  3. 参数列表不同（个数，顺序，类型）和方法的返回值类型无关

* #### 重写（Override）

  又称覆盖，方法覆盖是说子类重新定义了父类的方法。方法覆盖必须有相同的方法名，参数列表和返回类型。覆盖者可能不会限制它所覆盖的方法的访问。

  	1.  不能存在同一个类中，在继承或实现关系的类中；

     	2.  名相同，参数列表相同，方法返回值相同；
        	3.  子类方法的访问修饰符要大于父类的；
           	4.  子类的检查异常类型要小于父类的检查异常；

### 1.11java中是否可以覆盖一个private或者是static的方法

​	java中static方法不能被覆盖，因为方法覆盖是基于运行时动态绑定的，而static方法时编译时静态绑定的。static方法跟类的任何实列都不相关，所以概念上不适用。

​	java中也不可以覆盖private的方法，因为private修饰的变量和方法只能在当前类中使用，如果是其他的类继承当前类是不能访问到private变量或方法的，当然也不能覆盖。

### 1.12面向对象的六个基本原则

面向对象开发的六个基本原则（单一职责，开放封闭，里氏替换，依赖倒置，合成聚合复用，接口隔离）迪米特法则。在项目中用过哪些原则

* #### **六个基本原则**

​	**单一职责：**

​		一个类只做它该做的事情（高内聚）在面向对象中，如果只让一个类完成它该做的事，		而不涉及与它无关的领域就是践行了高内聚原则，这个类就只有单一职责。

​	**开放封闭：**

​		软件实体应当对扩展开放，对修改关闭。要做到开闭有两个要点：

​			1、抽象是关键，一个系统中如果没有抽象类或者接口系统就没有扩展点；

​			2、封装可变性，将系统中的各种可变因素封装到一个继承结构中，如果多个可变因			素混杂在一起，系统将变得复杂而慌乱；

​	**里氏替换：**

​		任何时候都可以用子类型替换掉父类型。子类一定是增加父类的能力而不是减少父类的		能力，因为子类比父类的能力更多，把能力多的对象当成能力少的对象来用当然没有任		何问题。

​	**依赖倒置**

​		面向接口编程（该原则说的直白和具体一些就是声明方法的参数类型，方法的返回类		型，变量的引用类型时，尽可能使用抽象类型而不用具体类型，因为抽象类型可以被它		的任何一个子类所替代）

​	**合成聚和复用**

​		优先使用聚合或合成关系复用代码

​	**接口隔离**

​		接口要小而专，绝不能大而全。臃肿的接口时对接口的污染，既然接口表示能力，那么		一个接口只应该秒速一种能力，接口也应该时高度内聚的。

* #### 迪米特法则

  迪米特法则又叫最少知识原则，一个对象应当对其他对象有尽可能少的了解。

* #### 项目中用到的原则

  单一职责，开放封闭，合成聚合复用（最简单例子就是String类）、接口隔离

### 1.13 java创建对象的四种方式

#### 	**1.13.1 使用new创建对象**

​	使用new关键字创建对象应该时最常见的一种方式，但我们应该知道，使用new创建对象会增加耦合度。无论使用什么框架，都要减少new的使用以降低耦合度。

``` java
public class Hello {
    public void sayHello(){
        System.out.println("Hello world!");
    }
}
```

``` java
public class Test01 {
    public static void main(String[] args) {
      Hello hello = new Hello();
      hello.sayHello();
    }
}
```

Consloe - 输出：

``` consloe
Hello world!
```

#### 	**1.13.2 使用反射的机制创建对象**

​	**使用Class类的newInstance()方法**

``` java
public class Hello {
    public void sayHello(){
        System.out.println("Hello world!");
    }
}
```

``` java
public class Test01 {
    public static void main(String[] args) throws Exception {
     Class clazz  = Class.forName("com.wannabe.test.Hello");
     Hello hello = (Hello) clazz.newInstance();
     hello.sayHello();
    }
}
```

Consloe - 输出：

``` consloe
Hello world!
```

​	**使用Constructor类的newInstance方法**

​	Hello类的代码不变Test01代码如下：

``` java
import java.lang.reflect.Constructor;
public class Test01 {
    public static void main(String[] args) throws Exception {
    //获取类对象
     Class clazz  = Class.forName("com.wannabe.test.Hello");
     //获取构造器
     Constructor constructor = clazz.getConstructor();
     Hello hello = (Hello) constructor.newInstance();
     hello.sayHello();
    }
}
```

Consloe - 输出：

``` consloe
Hello world!
```

#### 	**1.13.3 采用clone**

​	clone时，需要已经有一个分配了内存的源对象，创建新对象时，首先应该分配一个和源对象一样大的内存空间。要嗲用clone方法需要实现Cloneable接口，由于clone方法是protracted的，所以要修改Hello类

``` java
public class Hello implements Cloneable{
    public void sayHello(){
        System.out.println("Hello world!");
    }
    public static void main(String[] args) throws Exception {
        Hello hello1  = new Hello();
        Hello hello2  = (Hello) hello1.clone();
        hello2.sayHello();
    }
}
```

Consloe - 输出：

``` consloe
Hello world!
```

#### 	**1.13.4 采用序列化机制**

​	使用序列化时，要实现Serializable接口，将一个对象序列化到磁盘上，而采用反序列化可以将磁盘上的对象信息转化导内存中。

``` java
import java.io.Serializable;
public class Hello implements Serializable {
    public void sayHello(){
        System.out.println("Hello world!");
    }
}
```

``` java
import java.io.*;
/**
 * @description 序列化与反序列化对象
 */
public class Serialize {
    public static void main(String[] args) throws Exception {
        Hello hello = new Hello();
        //准备一个文件用于存储该对象的信息；
        File file = new File("hello.obj");
        FileOutputStream fileOutputStream = new FileOutputStream(file);
        ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
        FileInputStream fileInputStream = new FileInputStream(file);
        ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
        //序列化对象，写入到磁盘中
        objectOutputStream.writeObject(hello);
        //反序列化对象
        Hello newHello = (Hello) objectInputStream.readObject();
        //测试方法
        newHello.sayHello();
    }
}
```

Consloe - 输出：

``` consloe 
Hello world!
```

> 转载：https://www.cnblogs.com/yunche/p/9530927.html

### 1.14 String、StringBuffer和StringBuilder的区别

* String、StringBuffer、StringBuilder

  * 都是filnal类，都不允许被继承；

  * String长度时不可变的，StringBuffer和StringBuilder长度时可变的；

  * StringBuffer时线程安全的，StringBuilder不是线程安全，但它们两个中的所有方法都是相同的，StringBuffer在StringBuilder的方法之上添加了synchronizad修饰，保证线程安全。

  * StringBuilder比StringBuffer拥有更好的性能。

  * 如果一个String类型的字符串，在编译时就可以确定是一个字符串常量，则编译完成之后，字符串会自动拼接成一个常量。此时String的速度比StringBuffer和StringBuilder的性能好的多。

    

### 1.15 String 不可变好处

* final
  * 首先因为String不可变，如果String不是final，那么就可以有子类继承Sting类，任何子类覆盖其方法，使得这些方法可以修改字符串，这样就违背了String的不可变性
* 不可变原因
  * 提高效率：比如一个字符串String s1 = "abc"，"abc"被放到常量池里面去了，我再String s2 = "abc"并不会复制字符串"abc"，只会多个引用指向原来那个常量，这样就提高了效率，而这一前提时String不可变，如果可变，那么多个引用指向同一个字符串常量，我就可以通过一个引用改变字符串，然后其他引用就被影响力了。
  * 安全：String常被用来表示url，文件路径，如果String可变，或存在安全隐患
  * String不可变，那么他的hashcode就一样，不用每次重新计算了
* String不变性的理解
  * String类时被final进行修饰的，不能被继承
  * 用“+”符号连接字符串的时候会创建新的字符串；
  * String s = new String("Hello world!");可能创建两个对象也可能创建一个对象，如果静态区中有"Hello world!"字符串常量对象的话，则仅仅再堆中创建一个对象，如果静态区中没有“Hello world!”对象，则堆上和静态区中都需要创建对象；
  * 在java中，通过使用“+”符号来串联字符串的时候，实际上底层会转成通过StringBuilder实例的append()方法来实现；

### 1.16String Pool

字符串常量池（String Pool）保存着所有字符串字面量（literal strings），这些字面量在编译就确定，不仅如此，还可以使用String的intern()方法在运行过程中将字符串添加到String Pool中。

当一个字符串调用intern()方法时，如果String Pool中已经存在一个字符串和该字符串值相等（使用equals()方法进行确定），那么就会返回StringPool中字符串的引用；否则，就会在StringPool中添加一个新的字符串，并返回这个新字符串的引用。

下面实例中，s1和s2采用new String()的方法新建了两个不用字符串，而s3和s4时通过s1.intern()方法取得一个字符串引用。intern()首先把s1引用的字符串放到StringPool中，然后返回这个字符串引用，因此s3和s4引用的是同一个字符串。

``` java
String s1 = new String("aaa");
String s2 = new String("aaa");
System.out.println(s1 == s2 );	//false
String s3 = s1.intern();
String s4 = s1.intern();
System.out.println(s3 == s4);	//true
```

如果是采用"bbb"这种字面量的形式创建字符串，会自动地将字符串放入StringPool中。

``` java
String s5 = "bbb";
String s6 = "bbb";
System.out.println(s5 == s6 );	//true
```

在java 7 之前，SpringPool被放在运行时常量池中，它属于永久代，而在java 7 ,String Pool被移到堆中。这是因为永久代的空间有限，在大量使用字符串的场景下会导致OutOfMemoryError错误。

### 1.17 new String("abc")

使用这种方式一共创建两个字符串对象（前提试String Pool中还没有"abc"字符串对象）

* "abc"属于字符串字面量，因此编译时期会在String Pool中创建一个字符串对象，指向这个"abc"字符串字面量；
* 而使用new的方式会在堆中创建一个字符串对象。 

创建一个测试了，其中Main方法中使用这种方式来创建字符串对象。

``` java
public class Test(){
    public static void main(String[] args){
        String s = new String("abc");
    }
}
```

使用javap - verbose Test 进行反编译，得到以下内容：

``` java
Classfile /C:/Users/10134/Desktop/新建文件夹/Test.class
  Last modified 2020-4-8; size 332 bytes
  MD5 checksum c8c1a1562f5f07e5849494dbb05ea92a
  Compiled from "Test.java"
public class Test
  minor version: 0
  major version: 52
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #6.#15         // java/lang/Object."<init>":()V
   #2 = Class              #16            // java/lang/String
   #3 = String             #17            // abc
   #4 = Methodref          #2.#18         // java/lang/String."<init>":(Ljava/lang/String;)V
   #5 = Class              #19            // Test
   #6 = Class              #20            // java/lang/Object
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               main
  #12 = Utf8               ([Ljava/lang/String;)V
  #13 = Utf8               SourceFile
  #14 = Utf8               Test.java
  #15 = NameAndType        #7:#8          // "<init>":()V
  #16 = Utf8               java/lang/String
  #17 = Utf8               abc
  #18 = NameAndType        #7:#21         // "<init>":(Ljava/lang/String;)V
  #19 = Utf8               Test
  #20 = Utf8               java/lang/Object
  #21 = Utf8               (Ljava/lang/String;)V
{
  public Test();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return
      LineNumberTable:
        line 1: 0

  public static void main(java.lang.String[]);
    descriptor: ([Ljava/lang/String;)V
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=3, locals=2, args_size=1
         0: new           #2                  // class java/lang/String
         3: dup
         4: ldc           #3                  // String abc
         6: invokespecial #4                  // Method java/lang/String."<init>":(Ljava/lang/String;)V
         9: astore_1
        10: return
      LineNumberTable:
        line 3: 0
        line 4: 10
}
SourceFile: "Test.java"

```

在Constant Pool中，#17存储这个字符串字面量"abc"，#3是String Pool的字符串对象，它指向#17这个字符串字面量。在main方法中，0：行new #2在堆中创建一个字符串对象，并且使用 ldc #3将String Pool中的字符串对象作为String构造函数的参数。

以下是String构造函数的源码。可以看到，在将一个字符串对象作为另外一个字符串对象的构造函数参数时，并不会完全复制value数组内容，而是都会指向同一个value数组。

```  java
public String(String original) {
        this.value = original.value;
        this.hash = original.hash;
    }
```

### 1.18 String有重写Object的hashcoide和toSting吗？如果重写equals不重写hashcoid会出现什么问题？

* **String有重写Object的hashcoide和toSting吗**
  * String重写了Object类的hashcode和String方法。
* **当equals方法呗重写时，通常有必要重写hashCode方法，以维护hashCode方法的常规协定，该协定声明相对等的两个对象必须有相同的hashCode**
  * objec1.euqal(object2)时为true，object1.hashCode()==object2.hashCode()为true
  * object1.hashCode()==object2.hashCode()为false时，objec1.euqal(object2)必定为false
  * object1.hashCode()==object2.hashCode()为true时，但objec1.euqal(object2)不一定为true
* 重写equals不重写hashCode会出现什么问题
  * 在存储散列时（如Set类），如果原对象equals(新对象)，但没有对hashCode重写，即两个对象拥有不同的hashCode，则在集合中将会存储两个值相同的对象，从而导致混看。因此在重写equals方法时，必须重写hashCode

### **1.19 开发与运行Java程序需经过哪些过程？**

1. 用工具编辑源程序，也就是写代码，保存；
2. 用java编辑器工具javac.exe编译源程序文件，生成字节码.class文件；
3. 用java解释器工具java.exe解释运行生成.class文件；

### 1.20 java如何进行文件读取？

FileReader类是将文件按字符流的方式读取char数组或者String.FilenputStream则按字符流的方式读取文件byte数组；

1. 首先获得一个文件句柄。File file = new File(); file 即为文件句柄。两人之间连通电话网络了，接下来就可以开始打电话了；
2. 通过这条线路读取甲方的信息：new FileInputStream(file) 目前这个信息已经读进来内存当中了。接下来需要解读成乙方可以理解的东西；
3. 既然你使用FileInputSteam()。那么对应的需要使用InpustStreamReader()这个方法进行解读刚才装进来内存当中的数据；
4. 解读完成后要输出，那当然要转换成IO可以识别的数据，那就需要调用字节码读取的方法Bufferedreader(),同时使用bufferedReader()的readline()方法读取txt文件中的每一行数据；

### 1.21反射

反射机制是**运行状态中**，对于任意一个类，都能够**知道这个类的所有属性和方法**；对于任意一个对象，**都能够调用它的任意一个方法和属性**；这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制；

获取Class对象方法：class.getClass(),Class.forName,ClassLoader.loadClass



**Class.forName(),ClassLoader.loadClass()的区别：**

- forName在类加载的时候会执行静态代码块
- loadclass只有在调用的newInstance方法的时候才会执行静态代码块

初始化不同：

1. Class.forName()会对类初始化，而ClassLoader.loadClass()只会装载或链接；可见的效果就是类中静态初始化段及字节码中对所有静态成员的初始工作的执行（这个过程在类的所有父类中递归地调用）；这点就与ClassLoader.loadClass()不同；ClassLoader.loadClass()加载的类对象是在第一次被调用时才进行初始化的；你可以利用上述的差异，比如，要加载一个静态初始化开销很大的类，你就可以选择提前加载该类（以确保它在classpath下），但不进行初始化，直到第一次使用该类的域或方法时才进行初始化

类加载器不同：

1. Class.forName()方法（只有一个参数），使用调用者的类加载器来加载，也就是用加载了调用forName()方法的代码的那个类加载器，ClassLoader.loadClass()方法是一个实例化（非静态方法）调用时需要自己指定类加载器；

### 1.22JDK和JRE的区别

- java运行时环境（JRE）。它包括java虚拟机，java核心类库和支持文件。它不包含开发工具（JDK）--编译器，调试器和其他工具；
- java开发工具包（JDK）。是完整的java软件开发包，包含了JRE，编译器和其他的工具（比如：javaDoc，java调试器）可以让开发者开发，编译，执行java应用程序；

###### jdk1.8的新特性

- 接口可用default关键字添加非抽象方法
- lambda表达式：以前java集合是不能够进行内部迭代的，只能用循环外部迭代，有了lambda就能内部迭代

###### jdk1.7新特性

- 可以通过[],{}的形式向集合内添加元素
- switch支持String类型数据
- 数值可以加下划线

###### jdk1.5新特性

- for each循环
- 自动装拆箱：基本数据类型和它的包装类自动转换，Integer.valueOf ;Integer.invalue
- 泛型：其实是类型擦除，编译完类型就没了，执行方法又回到了原来的类型强转
- 可变参数

### 1.23 static和final

1. **static和final区别**

   - static
     - 修饰变量：静态变量随着类加载时被完成初始化，内存中只有一个，且JVM也只会为它分配一次内存，所有类共享静态变量
     - 修饰方法：在类加载的时候就存在，不依赖任何实例；static方法必须实现，不能用abstract修饰；
     - 修饰代码块：在类加载完之后就会执行代码块中的内容；
     - 父类静态代码块--->子类静态代码块--->父类非静态代码块--->父类构造方法--->子类非静态代码块--->子类构造方法；
   - final
     - 修饰变量：
       - 编译期常量：类加载的过程完成初始化，编译后带入到任何计算式中，只能是基本类型；
       - 运行时常量：基本数据类型或引用数据类型，引用不可变，但引用的对象内容可变；
     - 修饰方法：不能被继承，不能被子类修改；
     - 修饰类：不能被继承；
     - 修饰形参：final形参不可变；

2. **Final的好处**

   - final关键字提高了性能，JVM和java应用都会缓存final变量；
   - final变量可以安全的在多线程环境下进行共享，而不需要额外的同步开销；
   - 使用final关键字，JVM会对方法，变量及类进行优化；

3. **static方法是否可以覆盖**

   static方法不能被覆盖，因为方法覆盖是基于运行时动态绑定的，而static方法是编译时静态绑定的。static方法跟类的任何实例都不相关，所以概念上不适用；

### 1.24session和cookie区别

- session在服务器端，cookie在客户端（浏览器）
- session的运行依赖session id，而session id是存在cookie中的，也就是说，浏览器禁用cookie，同时session也会失效（但是可以通过其它方式实现，比如在url中传递session_id）
- session可以放在文件，数据库，或内存中都可以
- 用户验证这种场合一般用session
- cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗考虑到当前安全应当使用session
- session会在一定时间内保存在服务器上，当访问增多，会比较占用你服务器的性能考虑到减轻服务器性能方面，应当使用cookie
- 单个cookie保存的数据不能超过4k，很多浏览器都限制一个站点最多保存20个cookie
- cookie是web服务器发送给浏览器的一块信息，浏览器会在本地文件中给每一个web服务器存储cookie。以后浏览器在给特定的web服务器发请求的时候，同时会发送所有为该服务器存储的cookie
- 无论客户端浏览器做怎么样的设置，session都应该能正常工作。客户端可以选择禁用cookie，但是，session仍然是能够工作的，因为客户端无法禁用服务端的session。在存储的数量方面session和cookie也是不一样的的。session能存储任意的java对象，cookie只能存储String类型的对象

### 1.25 finalize finalization finally

1. **finalize 用途**

   垃圾回收器（garbage colector）决定回收某个对象时，就会运行该对象的finalize()方法，但是在java中很不辛，如果内存总是充足的，那么垃圾回收可能永远不会进行，也就是说filalize()了能永远不被执行，显然指望它做收尾工作是靠不住的。而finalize()最重要的用途是回收特殊渠道申请的内存。java程序有垃圾回收器，所以一般情况下内存问题不用程序员操心。但有一种JNI(Java Native Interface)调用non-java程序(C或C++),finalize()的工作就是回收这部分的内存。

2. **finally**

   finally一定会被执行，如果finally里有return语句，则覆盖try/catch里的return，比较爱考的是finally里面没有return语句，这时虽然finally里对return的值进行了修改，但return的值并不改变这种情况

3. **finally代码块和finalize()方法有什么区别?**

   无论是否抛出异常，finally代码块都会执行，它主要是用来释放应用占用的资源。finalize()方法是Object类的一个protected方法，它是在对象被垃圾回收之前由java虚拟机调用的。

4. **finally到底是在return之前执行还是return之后执行？**

   - finally是在return语句执行之后，return语句返回之前，finally是必须行的（当然是建立在try执行的基础上）；

   - finally中修饰的基本类型没有return是不影响返回结果的，有了return才会影响返回结果；

   - finally中修改set，list，map引用类型时，就算没有return也会影响返回结果；

     ``` java
     import java.util.ArrayList;
     import java.util.List;
     public class finallytest {
         public static void main(String[] args) {
             int j = test1();
             System.out.println("j=" +j);
             List<String> cats = new ArrayList<>();
             cats = addCats(cats);
             assert cats != null;
             cats.forEach(System.out::println);
         }
      
         private static int test1() {
             int i = 0;
             try {
                 System.out.println("try");
                 return i+=10;
             } catch (Exception e) {
                 e.printStackTrace();
                 return i;
             } finally {
                 System.out.println("finally i =" + i);
                 i+=10;
                 System.out.println("finally ii="+i);
                 return i;
             }
         }
      
         private static List<String> addCats(List<String> cats) {
             try {
                 cats.add("a");
                 return cats;
             } catch (Exception e) {
                 e.printStackTrace();
             } finally {
                 cats.add("b");
             }
      
             System.out.println("out");
             return null;
      
         }
     }
     ```

     在JVM虚拟机中，有虚拟机栈，上面的代码中每一个方法都对应一个栈帧，方法的执行对应着栈帧入栈，方法的执行完毕对着栈帧出栈；

     栈帧可以理解为一个方法的运行空间。它主要由两部分构成，一部分时局部变量表，方法中定义的局部变量以及方法的参数就存放在这张表中；另一部分时操作数栈，用来存放操作数；

     刚才的两段代码中的finally块中，i变量是要放在局部变量表的，每次有关于i的运算，都是要把i从局部变量表取出来（可以理解为copy一个副本），比如i+=10；那么需要把i和10都放在操作数栈中进行计算，然后得到一个结果，而这个记过是需要通过return语句写回到局部变量表；

     第一段代码中的finally块中，虽然执行了i+=10，但是由于没有return，所以局部变量表中的内容没有变化，所以i还是10；

     第二段代码中的finally块中，由于最后return i语句的执行，更新了局部变量中的i的值，所以最后返回结果就是20了；

     return返回后，就代表着方法执行结束，相应的该方法的栈帧就出栈了，而这个时候也就意味着，return返回是最后执行的，所以finally语句是在返回之前执行的！

5. **final关键字详解**

   final在java中是一个保留的关键字，可以声明变量，方法和类；

   ****

   **什么是final变量/方法/类？**

   任何变量前被final修饰就是final变量，定义类前被final修饰就是final类，任何方法前被final修饰就是final方法；

   ****

   **变量/方法/类三的区别**

   1. **final类**

      ![image-20200417172951587](C:\Users\10134\AppData\Roaming\Typora\typora-user-images\image-20200417172951587.png)

      当前final修饰一个类时，表明这个类不能被继承。上图13行，那句英文翻译过来就是不能继承Cat类；

      把final关键字去掉就可以了； 

   2. **final方法**

      使用final方法的两个原因：

      1. 将方法锁定，以防任何继承类修改它的涵义；
      2. 效率：早期的java实现中，会将final方法转为内嵌调用。但是如果方法过于庞大，可以能看不到内嵌调用带来的任何性能提升。在最近的java版本中华，不需要使用final方法进行这些优化了；

      **而且final方法时静态绑定的，在编译时就确定好哪个类的方法，所以final方法没有final方法的快一些；**

   3. **final变量**

      变量被final修饰就是final变量，

      ****

      **final变量跟普通变量的区别：**

      ``` java
      public class Main {
         public static void main(String[] args) {
             String a = "wananbe2";
             final String b = "wananbe";
             String d = "wananbe";
             String c = b + 2;
             String e = d + 2;
             System.out.println((a == c)); //true
             System.out.println((a == e)); //false
         }
      }
      ```

      - 变量a指的时字符串常量池中的wannabe2；
      - 变量b是final修饰的，变量b的值在编译时就已经确定了它的确定值，换句话说就是提前知道了变量b的内容是个啥，相当于一个编译期常量
      - 变量c是b+2得到的，由于b是一个常量，所以使用b的时候相当于使用b的原始值（wannabe）来进行计算，所以c生成的也是一个常量，a是常量，c也是常量，都是wannabe2而java中常量池中只能生唯一的一个wannabe2字符串，所以a和c相等
      - d是指向常量池中wannabe，但由于d不是final修饰，也就是说使用d的时候不会提前知道d的值是什么，所以在计算e的时候就不一样了，e的话由于使用的是d的引用计算，变量d的访问却需要在运行时通过链接来进行，所以这种计算会在堆上生成wannabe2，所以最后e指向的时堆上锁定wannabe2；所以a和e不相等

      ****

      **final修饰变量和修饰引用变量的区别**

      就是final修饰的常量普通变量不可改变，修饰的引用变量不可变，引用对象的内容可以改变；

   ![image-20200417175033137](C:\Users\10134\AppData\Roaming\Typora\typora-user-images\image-20200417175033137.png)

   ​		这个就是普通int变量，想修改但是报错了；

   ​		**修饰的引用变量不可变：**

   ![image-20200417175406841](C:\Users\10134\AppData\Roaming\Typora\typora-user-images\image-20200417175406841.png)	xiaoBai是引用变量，被final修饰，如果再把xiaoBai这个引用指向别的地方，就报错了；

   ​	**引用对象的内容可以改变**

   ​	![image-20200417175822259](C:\Users\10134\AppData\Roaming\Typora\typora-user-images\image-20200417175822259.png)

​			运行结果2没有报错，说明xiaoBai这个对象里面的i值增加了1，引用对象的内容改变了；

****

​	**4.	final关键字的好处**

- final方法比没有final快一些；
- final关键字提高了性能，JVM和java应用都会缓存final变量
- final变量可以安全的在多线程环境下运行共享，而不需要额外的同步开学
- 使用fianl关键字，JVM会对方法，变量及类进行优化；

### 1.26访问控制修饰符

| 访问级别 | 访问控制修饰符     | 同类 | 同包 | 子类 | 不同包 |
| -------- | ------------------ | ---- | ---- | ---- | ------ |
| 公开     | public             | √    | √    | √    | √      |
| 受保护   | protracted         | √    | √    | √    | --     |
| 默认     | 没有访问控制修饰符 | √    | √    | --   | --     |
| 私有     | private            | √    | --   | --   | --     |

不写时默认default。默认对于同一个包中的其他类相当于公开（public），对于不是同一个包中的其他类相当于私有（private），受保护（protected）对子类相当于公开，对不是同一个包中的没有父子关心的类相当于私有

不可以覆盖private方法，因为private修饰的变量和方法只有当前类中使用，如果是其他的类继承当前类是不能访问到private变量或方法的，当然依然不能覆盖；

### 1.24Object有哪些方法？

- hashcode()
  - 该方法用于哈希查找，重写equals方法一般都要hashCode方法，这个方法在一些具有哈希功能的Collection中用到
  - 一般必须满足obj1.equals(obj2)==true。可以推出obj1.hash- Code()==obj2.hashCode()，但是hashcode相等不一定满足equals。不过为了提高效率，应该尽量使上面两个条件接近等价。

****

- clone()
  - 保护方法，实现对象的浅复制，只有实现了Cloneable接口才可以调用该方法，否则抛出ClonNotSupportedException异常

****

- equals()
  - 该方法时非常重要的一个方法，一般equals和==是不一样的，但是Object中两者是一样的，子类一般都有这个方法

****

- toString()
  - 该方法用的比较多，一般子类都有覆盖

****

- getClass()
  - final方法，获取运行时类型

****

- wait()
  - wati方法就是使当前线程等待该对象的锁，当前线程必须是该对象的拥有者，也就是具有该对象的锁。wait()方法一直等待，直到获得锁或者被中断，wait(long timeout)设定一个超时间隔，如果在规定时间内没有获得锁就返回；
  - 调用该方法后当前线程进入睡眠状态，直到一下事件发生
    1. 其他线程调用了该对象的notify方法
    2. 其他线程嗲用了该对象的notifyAll方法
    3. 其他线程调用了interrupt中断该线程
    4. 时间间隔到了
  - 此时该线程就可以调度了，如果被中断的话就抛出一个InterruptedException异常

****

- notify()
  - 该方法唤醒在该对象上等待的某个线程；
- notifyAll()
  - 该方法唤醒在该对象上等待的所有线程；
- finalize()
  - 该方法用于释放资源，因为无法确定该方法什么时候被调用，很少使用

### 1.28Java语言有哪些特点？

1. 简单易学；
2. 面向对象（封装，继承，多态）；
3. 平台无关性（java虚拟机实现平台无关性）；
4. 可靠性
5. 安全性
6. 支持多线程（C++ 语言没有内置的多线程机制，因此必须调用操作系统的多线程功能来进行多线程程序设计，而 Java 语言却提供了多线程支持）
7. 支持网络编程并且很方便（java语言诞生本身就是为简化网络编程设计的，因此java语言不仅支持网络编程而且很方便）
8. 编译与解释并存

### 1.29异常

Java 异常类层次结构图

![Java异常类层次结构图](https://my-blog-to-use.oss-cn-beijing.aliyuncs.com/2019-2/Exception.png)

java中，所有的异常都有一个共同的祖先，java.lang包中的**Throwable类**；

Throwable：有两个重要的子类：**Error（错误）**和 **Exception（异常）**，二者都是java异常处理的重要子类，各自都包含大量子类；

****

**Error(错误)：是程序无法处理的错误**，表示运行应用程序中比较严重问题。大多数错误与代码编写者执行的操作无关，而表示代码运行时JVM（java虚拟机）出现的问题。

例如：java虚拟机运行错误（Virtual MachineError）,当JVM不再有继续执行操作所需的内存资源时，将出现OutOfMemoryError。这些异常发生时，java虚拟机（JVM）一般会选择线程终止。

这些错误表示故障发生于虚拟机自身，或者发生在虚拟机试图执行应用时，如java虚拟机运行错误（Virtual MachineError），类定义错误（NoClassDefFoundError）等。这些错误是不可查的，因为它们在应用程序的控制和处理能力之外，而且绝大多数是程序运行时不允许出现的状况。对于设计合理的应用程序来说，即使确定发生了错误，本质上也不应该试图去处理它所引起的异常状况，在java中，错误通过Error的子类描述；

****

**Exception(异常):是程序本身可以处理的异常**。Exception类有一个重要的子类**RuntimeExcpetion**它是由java虚拟机抛出。

**NullPointerException**(要访问的变量没有引用任何对象，抛出该异常)；

**ArithmeticException**(算术运算异常，一个整数除以0时，抛出该异常)；

**ArrayIndexOutOfBoundsException** (下标越界异常)；

注意：**异常和错误的区别：异常能被程序本身处理，错误时无法处理的；**

****

**Throwable类常用方法**

- public String getMessage():返回异常发生时的简要描述；
- public String toString():返回异常发生时的详细信息；
- public String getLocalizedMessage():返回异常对象的本地化信息，使用Throwable的子类覆盖这个方法，可以生成本地化信息，如果子类没有覆盖该方法，则该方法返回的信息与getMessage()返回的结果相同；
- public void printStrackTrace():在控制台上打印Throwable对象封装的异常信息；

****

**异常处理总结**

- try块：用于捕获异常，其后可接零个或多个catch块，如果没有catch块，则必须跟一个finally块；
- catch块：用于处理try捕获到的异常；
- finally块：无论是否捕获或处理异常，finally块里的语句都会被执行。当在try块或catch块中遇到return语句时，finally语句将在方法返回之前被执行；

**在以下4种特殊情况下，finally块不会被执行**

1. 在finally语句第一行发生异常，因为在其他行，finally块还是会得到执行；
2. 在前面的代码中用了System.exit(int)已退出程序，exit时带参函数；若该语句在异常语句之后，finally会执行；
3. 程序所在的线程死亡；
4. 关闭CPU