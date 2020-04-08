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