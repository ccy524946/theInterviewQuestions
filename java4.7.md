[TOC]

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

###   1.4 . 查看以下代码有什么错？

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