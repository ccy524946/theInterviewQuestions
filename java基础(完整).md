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

### 1.30Runtime

Runtime:运行时，时一个封装了JVM的类，每一个JAVA程序实际上都是启动了一个JVM进程，每一个JVM进程都对应一个Runtime实例，此实例时由JVM为其实例化的。所以我们不能实例化一个Runtime对象，应用程序也不能创建自己的Rntime类实例，但可以通过getRuntime方法获取当前Runtime运行时对象的引用。一旦得到了一个当前的Runtime对象的引用，就可以调用Runtime对象的方法去控制java虚拟机的状态和行为。

Runtime类中没有构造方法，本类的构造方法被私有化了，所以才会有getRuntime方法返回本来的实例对象，这与单例设计模式不谋而合；

public static Runtime getRuntime()直接使用此静态方法可以取得Runtime类的实例；

### 1.31接口和抽象类

#### 1.13.1接口和抽象类的区别？

1. 抽象类可以有构造方法，而接口内不能有构造方法。
2. 抽象类中可以有普通的成员变量，而接口不能有普通成员变量；
3. 抽象类冲可以包含非抽象的普通方法，而接口中所有的方法必须是抽象的，不能有非抽象的普通方法；
4. 抽象类中的抽象方法的访问类型可以是public，protected和private，但接口中的抽象方法只能是public类型的，并且默认即为public abstrat类型；
5. 抽象类中可以包含静态方法，接口不能包含静态方法；
6. 抽象类中和接口中都可以包含静态成员变量，抽象类中的静态变量的访问类型可以任意，但接口中定义的变量只能是public static类型，并且默认为public static final类型；
7. 一个类可以实现多个接口，但只能继承一个抽象类；

#### 1.13.2java抽象类可以有构造函数吗？

​	可以有，抽象类可以声明并且定义构造函数，因为你不可以创建抽象类的实例，所以构造函数只能通过构造函数链调用（java中构造函数链指的是从其他构造调用一个构造函数），例如，当你创建具体的实现类。现在一些面试官问，如果你不能对抽象类实例化那么构造函数的作用是什么？它可以用来初始化抽象类内部声明的通用变量，并被各种实现使用。另外，即使你没有提供任何构造函数，编译器将为抽象类添加默认的无参数的构造函数，没有的话你的子类将无法编译，因为在任何构造函数中的第一条语句隐式调用super()，java中默认超类的构造函数；

#### 1.13.2Java抽象类可以实现接口吗？它们需要实现所有的方法吗？

可以，抽象类可以通过使用关键字implements来实现接口，因为它们是抽象的，所以它们不需要实现所有的方法。好的做法是，提供一个抽象基类以及一个接口来声明类型，这样的例子是，java.util.List接口和相应的java.util.AbstractList抽象类。因为AbstractList实现了所有的通用方法，具体的实现像LinkedList和ArrayList不受实现所有方法的负担，它们可以直接实现List接口，这对两方面都很好，你可以利用接口声明类型的优点和抽象类的灵活性在一个地方实现共同的行为。

#### 1.13.3java抽象类可以是final的吗？

不可以，java抽象类不能是final的。将它们声明为final的将会阻止它们被继承，而这正是使用抽象类唯一的方法。它们也是彼此相反的，关键字abstract强制继承类，而关键字final阻止类被扩张，在现实世界中，抽象表示不完备性，而final是用来证明完整性，底线是，你不能让你的java类abstract又final，同时使用，是一个编译时错误；

#### 1.13.4java抽类可以有static方法吗？

可以，抽象类可以声明并定义static方法，没什么阻止这样做。但是，必须遵守java中将方法声明为static的准则

#### 1.13.5可以创建抽象类的实例吗？

不可以，你不能创建java抽象类的实例，它们是不完全的。即使你的抽象类不包含任何抽象方法，你不能对它实例化。将类声明为abstract的，就等你告诉编译器，它是不完全的不应该被实例化。当一段代码尝试实例化一个抽象类时java编译器会抛出错误；

#### 1.13.6抽象类必须有抽象方法吗？

不需要，抽象类有抽象方法不是强制性的。你只需要使用关键字abstract就可以将类声明为抽象类。编译器会强制所有结构的限制来使用抽象类，例如，现在允许创建一些实例。是否在抽象类中有抽象方法时引起争论的。我的观点时，抽象类应该有抽象方法，因为这是当程序员看到那个类类并做假设的第一件事。这也符合最小惊奇原则；

#### 1.13.7何时选用抽象类而不是接口？

这是对之前抽象类和接口对比问题的后续。如果你知道语法差异，你可以很容易回答这个问题。因为它们可以令你做出抉择。当关心升级时，因为不可能在一个发布的接口中添加一个新方法，用抽象类会更好。类似地，如果你的接口中有很多方法，你对它们的实现感到很头疼，考虑提供一个抽象类昨晚默认实现。这是java集合包中的模式，你可以使用提供默认实现List接口的AbstractList；

#### 1.13.8java中的抽象方法是什么？

抽象方法是一个没有方法体的方法，你仅需要声明一个方法，不需要定义它并使用关键字abstract声明，java接口中所有方法的声明默认是abstract的，这是抽象方法的例子public void abstract printVersion();

现在，为了实现这个方法，你需要继承该抽象类并重载这个方法；；

#### 1.13.9java抽象类中可以包含main方法吗？

可以，它是一个静态方法，可以使用main方法执行抽象类，但不可以创建任何实例；

### 1.32注解

**什么是注解？**

​	Annotation是java5开始引入的新特性，中文名称叫注解；

​	它是提供了一个安全的类似注释的机制，用来将任何的信息或元数据（metadata）与程序元素（类，方法，成员变量等）进行关联，为程序的元素（类，方法，成员变量）加上更直观更明了的说明，这些说明信息是与程序的业务逻辑无关，并且供指定的工具或框架使用，Annotation像一种修饰符一样，应用于包，类型，构造方法，方法，成员变量，参数及本地变量的声明语句中。

​	java注解是附加在代码中的一些元信息，用于一些工具在编译，运行时进行解析和使用，起到说明，配置的功能。注解不会影响代码的实际逻辑。仅仅起到辅助性的作用，包含在java.lang.annotation包中；

**注解的用处：**

1. 生成文档，这是最常见的，也就是java最早提供的注解，常用的有@param @return等
2. 跟踪代码依赖性，实现替代配置文件功能，比如Dagger2依赖注入，未来java开发，将大量注解配置，具有很大用处；
3. 在编译时进行格式检查，如@Override放在方法前，如果你这个方法并不是覆盖了超类方法，则编译时就能检查出

**注解的原理：**

​	注解本质是一个继承了Annotation的特殊接口，其具体实现类是java运行时生成的动态代理类，而我们通过反射获取注解时，返回的是java运行时生成的动态代理对象$Proxy1。通过代理对象调用自定义注解（接口）的方法，会最终调用AnnotationInvocationHandler 的invole方法。该方法会从memberValues 这个Map中索引出对应的值。而memberValues 的来源是java常量池。

**元注解：**

java.lang.annotation提供了四种元注解，专门注解其他的注解(在自定义注解的时候，需要使用到元注解):

- @Documented:	注解是否将包含在javaDoc中
- @Retention:     什么时候使用该注解
- @Target:   注解用于什么地方
- @Inherited：是否允许子类继承该注解

1. @Retention-定义该注解的生命周期
   - RetentionPolicy.SOURCE:在编译阶段丢弃。这些注解在编译结束之后就不再有任何意义，所以它们不会写入字节码。@Override，@SuppressWarnings都属于这类注解。
   - RetentionPolicy.Class:在类加载的时候丢弃。在字节码文件的处理中有用。注解默认使用这种方式；
   - RetentionPolicy.RUNTIME:始终不会丢弃，运行期也保留该注解，因此可以使用反射机制读取该注解的信息。我们自定义的注解通常使用这种方式；
2. @Target-表示该注解用于什么地方。默认值为任何元素，表示该注解用于什么地方。可用的ElementType参数包括；
   - ElementType.CONSTRUCTOR:用于描述构造器
   - ElementType.FIELD:成员变量，对象，属性（包括enum实例）
   - ElementType.LOCAL_VARLABLE:用于描述局部变量
   - ElementType.METHOD:用于描述方法
   - ElementType.PACKAGE:用于描述包
   - ElementType.PARAMETER:用于描述参数
   - ElementType.TYPE:用于描述类，接口（包括注解类型）或enum声明
3. @Documented-一个简单的Annotation标记注解，表示是否将注解信息添加在java文档中；
4. @Inherited-定义该注解和子类的关系
   - @Inherited元注解是一个标记注解，@Inherited阐述了某个被标注的类型是被继承的。如果一个使用了@Inherited修饰的annotation类型被用于一个class，则这个annotation被用于该class的子类；

**常见标准的Annotation**

1. @Override

   java.lang.Overrid是一个标记类型注解，它被用作标注方法。它说明了被标注的方法重写了父类的方法，起到了断言的作用。如果我们使用了这种注解在一个没有覆盖父类方法的方法时，java编译器将以一个编译错误来警示；

2. @Deprecated

   Deprecated也是一种标记类型注解，当一个类型或者类型成员使用@Deprecated修饰的话，编译器将不鼓励使用这个被标注的程序元素。所以使用这种修饰具有一定的“延续性”，如果我们在代码中通过继承或者覆盖的方式使用了这个过时的类型或者成员，虽然继承或者覆盖后的类型或者成员并不是被声明为@Deprecated，但编译器仍然要报警

   

3. @SuppressWarnings

   SuppressWarning  不是一个标记类型注解。它有一个类型为String[] 的成员，这个成员的值为被禁止的警告名。对于javac 编译器来讲，被-Xlint  选项有效的警告名也同样对@SuppressWarings 有效，同时编译器忽略掉无法识别的警@SuppressWarnings("unchecked") 

**自定义注解**

自定义注解类编写的一些规则:

1. Annotation 型定义为@interface, 所有的Annotation 会自动继承java.lang.Annotation这一接口,并且不能再去继承别的类或是接口.
2. 参数成员只能用public 或默认(default) 这两个访问权修饰
3. 参数成员只能用基本类型byte、short、char、int、long、float、double、boolean八种基本数据类型和String、Enum、Class、annotations等数据类型，以及这一些类型的数组.
4. 要获取类方法和字段的注解信息，必须通过Java的反射技术来获取 Annotation 对象，因为你除此之外没有别的获取注解对象的方法
5. 注解也可以没有定义成员,，不过这样注解就没啥用了

### 1.30泛型

1. java中的泛型是什么？使用泛型的好处是什么？

   在集合中存储对象并使用前进行类型转换是多么的不方便。泛型防止了那张情况的发生，它提供了编译期的类型安全，确保你只能把正确类型的对象放入集合中，避免了在运行时出现ClassCastException。

2. java的泛型是如何工作的？什么是类型擦除？

   这是一道更好的泛型面试题。泛型是通过类型擦除来实现的，编译器在编译时擦除了所有类型相关的信息，所以在运行时不存在任何类型相关的信息。例如List<String>在运行时仅用一个List来表示。这样做的目的，是确保能和Java 5之前的版本开发二进制类库进行兼容。你无法在运行时访问到类型参数，因为编译器已经把泛型类型转换成了原始类型。根据你对这个泛型问题的回答情况，你会得到一些后续提问，比如为什么泛型是由类型擦除来实现的或者给你展示一些会导致编译器出错的错误泛型代码。请阅读我的Java中泛型是如何工作的来了解更多信息。

3. 什么是泛型中限定通配符和非限定通配符？

   这是另一个非常流行的Java泛型面试题。限定通配符对类型进行了限制。有两种限定通配符，一种是<? extends T>它通过确保类型必须是T的子类来设定类型的上界，另一种是<? super T>它通过确保类型必须是T的父类来设定类型的下界。泛型类型必须用限定内的类型来进行初始化，否则会导致编译错误。另一方面<?>表示了非限定通配符，因为<?>可以用任意类型来替代。更多信息请参阅我的文章泛型中限定通配符和非限定通配符之间的区别。

4. List<?extends T> 和List<?super T>之间有什么区别?

   这和上一个面试题有联系，有时面试官会用这个问题来评估你对泛型的理解，而不是直接问你什么是限定通配符和非限定通配符。这两个List的声明都是限定通配符的例子，List<? extends T>可以接受任何继承自T的类型的List，而List<? super T>可以接受任何T的父类构成的List。例如List<? extends Number>可以接受List<Integer>或List<Float>。在本段出现的连接中可以找到更多信息。

5. 如何编写一个泛型方法，让它能接受泛型参数并返回泛型类型？

   编写泛型方法并不困难，你需要用泛型类型来替代原始类型，比如使用T, E or K,V等被广泛认可的类型占位符。泛型方法的例子请参阅Java集合类框架。最简单的情况下，一个泛型方法可能会像这样:

   ``` java
   public V put(K key, V value) {
       return cache.put(key, value);
   }
   ```

6. java中如何使用泛型编写写带有参数的类？

   这是上一道面试题的延伸。面试官可能会要求你用泛型编写一个类型安全的类，而不是编写一个泛型方法。关键仍然是使用泛型类型来代替原始类型，而且要使用JDK中采用的标准占位符。

7. 编写一段泛型程序来实现LRU缓存？

   对于喜欢Java编程的人来说这相当于是一次练习。给你个提示，LinkedHashMap可以用来实现固定大小的LRU缓存，当LRU缓存已经满了的时候，它会把最老的键值对移出缓存。LinkedHashMap提供了一个称为removeEldestEntry()的方法，该方法会被put()和putAll()调用来删除最老的键值对。当然，如果你已经编写了一个可运行的JUnit测试，你也可以随意编写你自己的实现代码。

8. 你可以把List<String>传递给一个接受List<Object>参数的方法吗？

   对任何一个不太熟悉泛型的人来说，这个Java泛型题目看起来令人疑惑，因为乍看起来String是一种Object，所以List<String>应当可以用在需要List<Object>的地方，但是事实并非如此。真这样做的话会导致编译错误。如果你再深一步考虑，你会发现Java这样做是有意义的，因为List<Object>可以存储任何类型的对象包括String, Integer等等，而List<String>却只能用来存储Strings。

9. Array中可以用泛型吗？

   这可能是Java泛型面试题中最简单的一个了，当然前提是你要知道Array事实上并不支持泛型，这也是为什么Joshua Bloch在Effective Java一书中建议使用List来代替Array，因为List可以提供编译期的类型安全保证，而Array却不能。

10. 如何阻止java中的类型未检查的警告？

    如何阻止Java中的类型未检查的警告?
    如果你把泛型和原始类型混合起来使用，例如下列代码，Java 5的javac编译器会产生类型未检查的警告;

    例如:

    ``` java
    List<String> rawList = new ArrayList()
    ```

    

### 1.34 泛型 ？与T的区别

``` java
public static <T> void show1(List<T> list){
 for (Object object : list) {
        System.out.println(object.toString());
    }
}
public static void show2(List<?> list) {
    for (Object object : list) {
        System.out.println(object);
    }
}
public static void test(){
   List<Student> list1 = new ArrayList<>();
   list1.add(new Student("zhangsan",18,0));
   list1.add(new Student("lisi",28,0));
   list1.add(new Student("wangwu",24,1));
   //这里如果add(new Teacher(...));就会报错，因为我们已经给List指定了数据类型为Student
   show1(list1);
   System.out.println("************分割线**************");
   //这里我们并没有给List指定具体的数据类型，可以存放多种类型数据
   List list2 = new ArrayList<>();
   list2.add(new Student("zhaoliu",22,1));
   list2.add(new Teacher("sunba",30,0));
   show2(list2);
}
```

从show2方法可以看出和show1的区别了，list2存放了Student和Teacher两种类型，同样可以输出数据，所以这就是T和?的区别啦

### 1.35字节流和字符流的区别

**字节流：**

![image-20200427225842338](C:\Users\10134\AppData\Roaming\Typora\typora-user-images\image-20200427225842338.png)

1. FileOutputStream(File name)创建一个文件输出流，向指定的File对象输出数据。
2. FileOutputStream(FileDescriptor)创建一个文件输出流，向指定的文件描述器输出数据。
3. FileOutputStream(String name)创建一个文件输出流，向指定名称的文件输出数据
4. FileOutputStream(String,boolean)用指定系统的文件名，创建一个输出文件

![image-20200427230158413](C:\Users\10134\AppData\Roaming\Typora\typora-user-images\image-20200427230158413.png)

**InputStreamReader 和 OutputStreamReader ：**

把一个以字节为导向的stream转换成为一个字符为导向的stream；

InputStreamReader 类是从字节流到字符流的桥梁：它读入字节， 并根据指定的编码方式，将之转换为字符流；

使用的编码方式可能由名称指定，或平台可接受的缺省编码方式；

InputStreamReader 的read()方法之一的每次调用，可能促使从基本字节输入流中读取一个或多个字节；

为了达到更好效率，考虑用BufferedReader封装InputStreamReader；

BufferedReader in = new BufferedReader(new InputStreamReader(System.in));

**相同点：**

InputStream，OutputStream,Reader,writer都是抽象类。所以不能直接new 

**字节流与字符流的区别:**

字节流和字符流使用是非常相似的，那么除了操作代码的不同之处，还有哪些不同：

区别：

1. 字节流在操作的时候本身是不会用到缓冲区（内存）的，是由文件本身直接操作从，而字符流在操作的时候是使用到缓冲区的；

2. 字节流在操作文件时，即使不关闭资源(close方法)，文件也能输出，但是如果字符流不适用close方法的话，则不会输出任何内容，说明字符流用的时缓冲区，并且可以使用flush方法强制进行刷新缓冲区，这时才能不在close的情况下输出内容；

3. Reader类的read()方法返回类型为int：作为整数读取的字符（占两个字节共16位），范围在0到65535之前（0x00-0xffff),如果已到达流的末尾，则返回-1；

   inputStream的read()虽然也返回int，但由于此类事面向字节流的，一个字节占8个位，所以返回0到255范围内的int字节值，如果因为已经到达末尾而没有可用的字节，则返回值-1。因此对于不能用0-255来表示的值就得用字符流来读取！比如说汉字

**字节流与字符流住哟啊的区别是它们的处理方式**

字节流：处理字节和字节数组或者二进制对象；

字符流：处理字符，字符数组或字符串；

**开发中究竟用字节流好还是字符流好？**

1. 字符（Reader和Writer）:中文，字符事是只有在内存中才会形成的操作字符，字符数组或字符串；
2. 字节（InputStream和OutputStream）:音频文件，图片，歌曲，所有的硬盘上保存文件或者进行传输的时候，操作字节个字节数组或二进制对象，
3. 如果要java程序实行一个拷贝功能，应该选用字节流进行操作（可能拷贝的是图片），并且采用边读边写的方式（节省内存）；

### 1.36父子类的加载顺序

类的加载顺序：

1. 父类静态代码块（包括静态初始化块，静态属性，但不包括静态方法）
2. 子类静态代码块（包括静态初始化块，静态属性，但不包括静态方法）
3. 父类非静态代码块（包括非静态初始化块，非静态属性）
4. 父类构造函数
5. 子类非静态代码块（包括非静态初始化块，非静态属性）
6. 子类构造函数

### 1.37什么是字符集和编码

在计算机底层，比如“字符集”在计算机中并不是文字的形式存在，而是一串二进制数字，如“01100111001...”

人类只认识文字，计算机只认识0和1，双方都不能妥协，那就必须要有一个从文字到0，1的映射了。

从我们可以看到的文字到0，1的映射称为编码，反过来从0，1到文字叫解码。

**字符集**

**ASCII,utf-8,utf-16,utf-32**这些都是字符集，字符的集合；

**ASCII**

因为计算机只能处理数字，如果要处理文本，就必须先把文本转换位数字才能处理，最早的计算机在设计时采用9个比特（bit）作为一个字节（byte）,所以，一个字节能表示的最大的整数就是255（二进制11111111=十进制255），0-255被用来表示大小写英文字符，数字和一些符号，这个编码表被称为ASCII编码，比如大写字母A的编码就是65，小写字母z的编码就是122；

**汉字表示**

因为计算机一开始是老美发明的，没考虑其他国家的字符，所以，中国指定了GB2312编码，用来把中文编进去；

类似的，日文和韩文等其他语言也有了这个问题，为了统一所有文字的编码，**Unicode**就诞生

了

**Unicode**

Unicode编码定义了这个世界上几乎所有字符（就是我们所看的字符，比如ABC，汉字等）的数字表示，而Unicode还兼容了很多老版本的编码规范，例如ASCII码

我们国家的每一个人都对应唯一的身份证号码，而Unicode也位每个字符发了一张身份证，这张“身份证”上有一串唯一的数字ID确定了这个字符；

这串数字在整个计算机的世界具有唯一性，Unicode给这串数字ID起了个名字叫【码点】

很多人说的编码其实是想表达Unicode转换格式（既：UTF，Unicode Transformation Formats）

UTF就是utf-8这些编码的前缀；

这个“Unicode转换格式”是为了解决“码点”在计算机存储方式而设计的；

【码点】经过映射后得到的二进制串的转换格式单位称之为【码元】（code unit）；【码点】就是一串二进制数，【码元】就是切分这个二进制数的方法

ex:如果有一个字符的码点二进制表示有n字节（n*8个二进制），其码元为8位（1个字节），那么其拥有码元n个。

Unicode 编码 发展到今天 扩展到了 21 位，为啥扩展到21位了呢？因为一开始老美只考虑自己那26个英文字母和数字，随着越来越多的国家的语言语言编码，Unicode不得的继续扩展，目前21位已经足够使用。

UTF-32是最好理解的一个了。UTF-32也就是说它的码元是32位，每32位去读一下码点，而码点是Unicode给字符的编码，前面也说了，最长才21位，因此每一个 UTF-32 值都可以直接表示对应的码点。

**为什么有UTF-8，UTF-16**

因为每个字符占用4字节太浪费空间了，所以有了UTF-8，UTF-16

什么是编码空间呢？前面说了Unicode ,它是 21 位的。这 21 位提供了 1,114,112 个码点,编码空间就是对应这1,114,112 个码点。

对了这里要说一下，这么多码点并不代表有这么多字符，目前大概只有10%的空间被使用了，人类社会还没创造出1,114,112 这么多的字符。

编码空间被分成 17 个平面（plane），每个平面有 65,536 个字符（正好填充2个字节，16位）。0 号平面叫做「基本多文种平面」（  BMP, Basic Multilingual Plane ），涵盖了几乎所有你能遇到的字符，除了 emoji（emoji位于1号平面 -  -）。其它平面叫做补充平面，大多是空的

UTF-16要常见得多，它的码元是16位的，也就是说每16位去读一下码点，获取码点的前16位数字，直到读取完成。

编码空间这里要用上了哈，BMP平面（也就是前面说的基本多文种平面）中的每一个码点都直接与一个UTF-16 的码元一一映射。

由于BMP 几乎包括了所有常见字符，UTF-16 一般需要 UTF-32大约 一半的空间。至于其它平面里很少使用的码点都是用两个 16 位的码元来编码的。

UTF-8 使用一到四个字节来编码一个码点。从 0 到 127 的这些码点直接映射成 1 个字节（对于只包含这个范围字符的文本来说，这一点使得  UTF-8 和 ASCII 完全相同）。接下来的 1,920 个码点映射成 2 个字节，在 BMP 里所有剩下的码点需要 3  个字节。Unicode 的其他平面里的码点则需要 4 个字节。UTF-8 是基于 8 位的码元的。UTF-8 是基于 8  位的码元的，因此它并不需要关心字节顺序（因为字节就是8位的呀，其它UTF-16和UTF-32在不同的机器编译环境下需要考虑字节的顺序问题）

https://mp.weixin.qq.com/s?__biz=MzI5MzYzMDAwNw==&mid=2247484848&idx=1&sn=ad7f134c40574ec1214df28b078c88e1&scene=19&token=557705008&lang=zh_CN#wechat_redirect

### 1.38 Math.round(11.5)等於多少? Math.round(-11.5)等於多少?

11.5+0.5后是12再向下取整是12;-11.5+0.5后是-11再向下取整-11

ex:

``` java
public class Ex(){
	public static void main(String[] args) {
		ceil();
		floor();
		round();
	}
  	//测试Math类的ceil方法，（天花板，向上取整）  
    public static void ceil(){
        int a = (int)Math.ceil(11.3);//12
        int b = (int)Math.ceil(-11.3);//11
        System.out.println("a="+a+",b="+b);
    }
    //floor：地板，向下取整
     public static void floor(){
        int a = (int)Math.floor(11.6);//11
        int b = (int)Math.floor(-11.6);//12
        System.out.println("a="+a+",b="+b);
    }
    //round：四舍五入
     public static void floor(){
        int a = (int)Math.floor(11.5);//12 11.3+0.5 11
        int b = (int)Math.floor(-11.6);//-11
        System.out.println("a="+a+",b="+b);
    }
    
}
```

Math类有三个取整的方法:ceil,floor,round,它们都是与英文名称的含义相对应，

**ceil ：天花板，表示向上取整；**

ex：

``` java
Math.ceil(11.3)的结果为12,Math.ceil(-11.3)的结果是-11;
```

**floor:地板，向下取整**

ex:

```
Math.floor(11.6)的结果为11,Math.floor(-11.6)的结果是-12;
```

**round：四舍五入**

ex：

```
Math.round(11.5)的结果为12，Math.round(-11.5)的结果为-11;
```

### 1.39 char 型变量中能不能存贮一个中文汉字?为什么?

char 型变量是用来存储 Unicode 编码的字符的，unicode 编码字符集中包含了汉字，所以，char 型变量中当然可以存储汉字啦。

不过，如果某个特殊的汉字没有被包含在unicode编码字符集中，那么，这个char变量就不能存储这个特殊汉字。补充说明：unicode编码占用两个字节，所以，char也占用两个字节

### 1.40面向对象和面向过程的区别

- **面向过程：面向过程性能比面向对象搞。**因为类调用时需要实例化，开销比较大，比较消耗资源，所以当性能是最重要的考量因素的时候，比如单片机，嵌入式开发，Linux/Unix等一般采用面向过程开发。但是，**面向过程没有面向对象易维护，易复用，易扩展**。
- **面向对象：面向对象易维护，易复用，易扩展 **，因为面向对象有封装，继承，多态性的特性，所以可以设计出低耦合的系统，使系统更加灵活，更加易于维护，但是**面向对象性能比面向过程低。**

### 1.41JVM,JDK,JRE

1. **JVM**

   java虚拟机（JVM）是运行java字节码的虚拟机。JVM有针对不同系统的特定实现，目的是使用相同的字节码。它们都会给出相同的结果。

   字节码和不同系统的 JVM 实现是 Java 语言“**一次编译，随处可以运行**”的关键所在。

   **字节码，使用它的好处：**

   在java中，JVM可以理解的代码就叫做字节码（扩展名为.class的文件），它不面向任何特定的处理器，只面向虚拟机，java语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言可移植的特点，所以java程序运行时比较高级，而且，由于字节码并不针对特定的机器，因此，java程序无须重新编译便可在多种不同操作系统的计算机上运行。

   **java程序从源代码到运行一般有下面3步：**

   .java文件(源代码)--->(jdk中的javac编译) .class文件(JVM可以理解的java字节码)——>(JVM)机器可执行的二进制机器码

2. **JDK和JRE**

   JDK是Java Development Kit，它是功能齐全的 Java SDK。它拥有 JRE 所拥有的一切，还有编译器（javac）和工具（如 javadoc 和 jdb）。它能够创建和编译程序。

   JRE 是 Java 运行时环境。它是运行已编译 Java 程序所需的所有内容的集合，包括 Java 虚拟机（JVM），Java 类库，java 命令和其他的一些基础构件。但是，它不能用于创建新程序。

   如果你只是为了运行一下 Java 程序的话，那么你只需要安装 JRE 就可以了。如果你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK  了。但是，这不是绝对的。有时，即使您不打算在计算机上进行任何 Java 开发，仍然需要安装 JDK。例如，如果要使用 JSP 部署 Web  应用程序，那么从技术上讲，您只是在应用程序服务器中运行 Java 程序。那你为什么需要 JDK 呢？因为应用程序服务器会将 JSP 转换为  Java servlet，并且需要使用 JDK 来编译 servlet。

### 1.42OracleJDK和OpenJDK的对比

对于java7，没什么关键的地方，OpenJDK项目主要基于SUN捐赠的HotSpot源代码，此外，OpenJDK被选为java7的参考实现，由Oracle工程师维护。关于JVM，JDK，JRE和OpenJDK之间的区别

OpenJDK 存储库中的源代码与用于构建 Oracle JDK 的代码之间有什么区别？

OracleJDK版本构建过程基于OpenJDK7构建，只添加了几个部分，例如部署代码，其中包括Oracle的java插件和java webStart的实现，以及一些封闭的源代码派对组件，如图形关栅化器，一些开源的第三方组件，如Rhino，以及一些零碎的东西，如附件文档或第三方字体。展望未来，我们的目的是开源OracleJDK的所有部分，除了我们考虑商业功能的部分。

**总结：**

1. Oracle JDK大概每6个月发一次主要版本，而OpenJDK版本大概每三个月发布一次。但这不是固定的。
2. OpenJDK是一个参考模型并且是完全开源的，而OracleJDK是OpenJDK的一个实现，并不是完全开源的。
3. OracleJDK比OpenJDK更稳定，OpenJDK和OracleJDK的代码几乎相同，但OracleJDK有更多的类和一些错误修复。因此如果想要开发企业/商业，建议是选择OracleJDK。因为它经过了彻底的测试和稳定。某些情况下，有些人提到使用OpenJDK可能会遇到了许多应用程序奔溃的问题。但是只要切换到OracleJDK就解决了问题。
4. 在响应性和JVM性能方面，OracleJDK和OpenJDK相比提供了更好的性能；
5. OracleJDK不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新版本获得支持来获取最新版本；
6. OracleJDK根据二进制代码许可证获得许可，而OpenJDK根据GPL v2许可证获得许可；

### 1.43 java和C++的区别

1. 都是面向对象的语言，都支持封装，继承和多态；
2. java不提供指针来直接访问内存，程序内存更加安全；
3. java的类是单继承的，C++支持多重继承，虽然java类不可以多继承，但是接口可以多继承；
4. java有自动内存管理机制，不需要程序员手动释放无用内存；
5. 在C语言中，字符串或字符数组最后都会有一个额外的字符'\0'来表示结束，但是，java语言中没有结束符这一概念；

### 1.44什么是java程序的主类应用程序和小程序的主类有何不同？

一个程序中可以有多个类，但是只能有一个类是主类，在java应用程序中，这个主类是指包含main()方法的类。而在java小程序中，这个主类是一个继承至系统类JApplet或Applet的子类，应用程序的主类不一定要求是public类，但小程序的主类要求必须是public，主类是java程序执行的入口点；

**java应用程序与小程序之间有哪些差别？**

应用程序是从主线程启动的（也就是main()方法）。applet小程序没有main()方法，主要是嵌在浏览器页面上运行的（调用了init()或者run()来启动）；嵌入浏览器这点跟flash的小游戏类似。

### 1.45在一个静态方法内调用一个非静态成员为什么是非法的？

由于静态方法可以不通过对象进行调用，因此在静态方法里，不能调用其他非静态变量，也不可以访问非静态变量成员。

### 1.46在java中定义一个不做事且没有参数的构造方法的作用？

java程序在执行子类的构造方法之前，如果没有用super()来调用父类特定的构造方法，则会调用父类中“没有参数的构造方法”。因此，如果父类中定义了有参数的构造方法，而在子类的构造方法有没有用super()来调用父类特定的构造方法，则编译时将发生错误，因为java程序在父类中找不到没有参数的构造方法可供执行，解决办法是在父类加上一个不做事且没有参数的构造方法；

### 1.47import java和javax有什么区别？

javaAPI所需要的包是java开头的包，javax当时只是扩展API包来使用。然而随着时间的推移，javax逐渐地扩展成为java API的组成部分。但是，将扩展从javax包移动到java包确实太麻烦了，最终会破坏一堆现有的代码，因此，最终决定javax包将成为API的一部分；

所以，实际上java和javax没有区别，这都是一个名字；

### 1.48接口和抽象类的区别

1. 接口的方法默认是public，所以方法在接口中不能有实现(java8开始接口方法可以有默认实现)而抽象类可以有非抽象的方法；
2. 接口中除了static，final变量，不能有其他变量，而抽象类中则不一定；
3. 一个类可以实现多个接口，但只能实现一个抽象类，接口本身可以通过extends关键字扩展多个接口；
4. 接口方法默认修饰符是public，抽象方法可以有public，protected和default这些修饰符（抽象方法就是为了被重写所以不能使用private关键字修饰）
5. 从设计层面来说，抽象是对类的抽象，是一种模板设计，而接口是行为的抽象，是一种行为的规范；

**备注：**

1. 在JDK8中，接口也可以定义静态方法，可以直接用接口名调用。实现类和实现是不可以调用的。如果同时实现两个接口，接口中定义了一样的默认方法，则必须重写，不然会报错；
2. JDK9的接口被允许定义私有方法；

**总结JDK7-JDK9 Java中接口概念的变化：**

1. 在JDK7或更早版本中，接口里面只能有常量变量和抽象方法，这些接口方法必须由选择实现接口的类实现；
2. JDK8的时候接口可以有默认方法和静态方法功能；
3. JDK9在接口中引入了私有方法和私有静态方法；

### 1.49成员变量与局部变量的区别？

1. 从语法形式上看：成员变量是属于类的，而局部变量是在方法中定义的变量或是方法的参数；成员变量可以呗public private static 等修饰符所修饰，而局部变量不能被访问控制修饰符及static所修饰；但是，成员变量和局部变量都能被final所修饰；
2. 从变量在内存中的存储方式来看：如果成员变量是使用static修饰的，那么这个成员变量是属于类的，如果没有使用static修饰，这个成员变量hi属于实例的，而对象存在于堆内存，局部变量则存在于栈内存；
3. 从变量在内存中的生存时间上看：成员变量是对象的一部分，它随着对象的创建而存在，而局部变量随着方法的调用而自动消失；
4. 成员变量如果没有被赋初始值则会自动以类型的默认而赋值(final修饰除外)，而局部变量不会自动赋值；

### 1.50 创建一个对象用什么运算符？对象实体与对象引用有何不同？

new 运算符，new创建对象实例(对象实例在堆内存中)，对象引用指向对象实例(对象引用存放在栈内存中)。一个对象引用可以指向0个或1个对象(一根绳子可以不系气球，也可以系一个气球)；一个对象可以有 n 个引用指向它（可以用 n 条绳子系住一个气球）。

### 1.51.1什么是方法的返回值？返回值在类的方法里的作用是什么？

方法的返回是指我们获取到的某个方法体中的代码执行后产生的结果；前提是该方法可能产生结果，返回值的作用：接收出结果，使得它可以用于其他的操作； 

#### 1.51.2一个类的构造方法的作用是什么? 若一个类没有声明构造方法，该程序能正确执行吗? 为什么?

主要作用是完成对象的初始化工作。可以执行，因为一个类即使没有声明构造方法也会有默认的不带参数的构造方法；

### 1.51.3构造方法有哪些特性?

1. 名字与类名相同；
2. 没有返回值，但不能用void声明构造函数；
3. 生成类的对象时自动执行，无需调用；

### 1.51.4静态方法和实例方法有何不同

1. 在外部调用静态方法时，可以使用“类名.方法名”的方式，也可以使用“对象名.方法名”的方式。而实例方法只有后面这种方式。也就是说，调用静态方法可以无需创建对象
2. 静态方法在访问本类的成员时，只允许访问静态成员(即静态成员和静态方法)，而不允许访问实例成员变量和实例方法。实例方法则无此限制；