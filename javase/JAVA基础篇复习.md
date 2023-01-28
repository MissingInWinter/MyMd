# JAVA基础篇复习

## 一.前期背景及环境

### 1.一些介绍

| Java SE(Java Standard Edition):标准版  （J2SE）     | Java技术的核心和基础         |
| --------------------------------------------------- | ---------------------------- |
| Java EE(Java Enterprise  Edition):企业版   （J2EE） | 企业级应用开发的一套解决方案 |
| Java ME(Java Micro Edition):小型版                  | 针对移动设备应用的解决方案   |

java具有面向对象、与平台无关、安全、稳定和多线程等优良特性

动态：

Java程序的基本组成单元就是类，有些类是自己编写的、而有些类是从类库中引入的，而类又是运行时动态装载的，这就使得java可以在分布式环境中动态的维护程序及类库。

c\c++则是编译阶段就将函数库或类库中被使用的相关生成机器码、后续升级需重新编译。

#### 1.1.jre、jvm、api等

java语言不像c\c++那样只能针对特定的处理器（Central Processing Units--------CPU）芯片进行编译。

Java可以在计算机操作系统上再提供一个java运行环境（Java Runtime Environment--------JRE）。该运行环境由Java虚拟机（Java Virtual Machine--------JVM）、类库、以及一些核心文件组成。

（Java Development Kit----------JDK）Java 语言的软件开发工具包.

(Intergrated Development Environment-------IDE)Java集成开发环境

(Application Programming Interface------API)应用程序编程接口

![7af40ad162d9f2d36880ccf1a3ec8a136327cc1f](images\7af40ad162d9f2d36880ccf1a3ec8a136327cc1f.png)

![j](images\j.png)

Java源程序编译生成字节码、Java虚拟机负责将字节码翻译成虚拟机所在平台的机器码、并让当前平台运行该机器码。

### 2.java环境配置

总结、网上下载安装包解压、在环境变量中加上

JAVA_HOME=你的解压路径

在PATH变量中添加

$JAVA_HOME/bin

这样就可以在任意目录下使用bin目录下的那些命令

![java环境变量](images\java环境变量.png)

PATH中很多值之间是由";"号连接、在Linux系统中配置时你会看到是以“:”连接。

## 二.命令行java的使用

### 1.新建Hello.txt

注意Java区分大小写、类名需与文件名相同、写完后改为Hello.java

如果源文件中有很多类（当你在一个Hello.txt中写不止一个类时、并列关系非内部类）、我们只能有一个类是public类。

`public class Hello{`
`public static void main(Sting[] args){`
`System.out.println("HELLO!");`
`}`
`}`

### 2.使用   javac  Hello.txt 会·生成hello.class

![Helloclass](images\Helloclass.png)

jdk1.6后编译器不再向早期版本兼容、像你用JDK8编译的字节码只能在安装了JRE8或更高版本的环境中运行。若未使用到JDK8中的一些新功能可以使用

`javac -source 1.6 Hello.java`

来在jre6中运行

### 3.使用java Hello来运行程序

使用Java解释器（java.exe）来解释字节码文件。

Java应用程序总是从主类的main方法开始执行。

`java Hello`

/注意不要写成java Hello.class/

另外jdk11后可以直接使用java Hello.java

### 4.使用javap 反编译

`javap Hello`

实测文件名加不加.class都可以

## 三.基础知识

### 1.注释

// 单行注释      

/* 多行注释    */

/**

文档注释、可以提取到文档说明中去

*/

在句中出现、只注释//或/*开始后的那部分

### 2.项目结构

project - module - package – class
project中可以创建多个module
module中可以创建多个package
package中可以创建多个class

### 3.快捷键

| **快捷键**                        | **功能效果**                     |
| --------------------------------- | -------------------------------- |
| main/psvm、sout、…                | 快速键入相关代码                 |
| Ctrl + D                          | 复制当前行数据到下一行           |
| Ctrl + Y                          | 删除所在行，建议用Ctrl + X       |
| Ctrl + ALT + L                    | 格式化代码                       |
| ALT + SHIFT + ↑ , ALT + SHIFT + ↓ | 上下移动当前代码                 |
| Ctrl + / , Ctrl + Shift  + /      | 对代码进行注释(讲注释的时候再说) |

### 4.字面量

计算机是用来处理数据的，字面量就是告诉程序员：数据在程序中的书写格式。

字符必须单引号围起来，有且仅能一个字符。

字符串必须用双引号围起来。

### 5.变量

内存中的一块区域。

用来存储一个数据的，且存储的数据可以被替换

变量要先声明再使用

变量声明后，不能存储其他类型的数据。

变量的有效范围是从定义开始到“}”截止,且在同一个范围内部不能定义2个同名的变量。

变量定义的时候可以没有初始值，但是使用的时候必须给初始值。

### 5.标志符

标志符就是名字。

我们写程序时会起一些名字，如类名、方法名、变量名，取名时要遵守一定的规则。

基本要求：由数字、字母、下划线(_)和美元符($)等组成

强制要求：不能以数字开头、不能是关键字、区分大小写

### 6.进制

Java程序中支持书写二进制、八进制、十六进制的数据，分别需要以0B或者0b、0、0X或者0x开头。

每3位二进制作为一个单元，最小数是0，最大数是7，共8个数字，这就是八进制。

每4位二进制作为一个单元，最小数是0，最大数是15，共16个数字，依次用： 0~9 A B C D E F  代表就是十六进制

十进制转二进制：除2取余

二进制至八、十六进制：拆成三个、四个一单位、分别转为八、十六进制即可

### 7.基本数据类型

### ![基本数据类型](images\基本数据类型.png)

![元素默认值](images\元素默认值.png)

#### 7.1添加尾缀说明

我们知道Java在变量赋值的时候，其中float、double、long数据类型变量，需要在赋值直接量后面分别添加f或F、d或D、l或L尾缀来说明。
其中，long类型最好以大写L来添加尾缀，因为小写l容易和数字1混淆。
例如：

long lNum  = 1234L;
float fNum = 1.23f;
double dNum = 1.23d;

这是Java语法规定，不添加尾缀很容易引起编译器报错，并且程序可读性也会变差。

不添加尾缀也不会报错的情况
Java语言中，整数直接量（例如：1、2、10等），JVM虚拟机是默认为int类型数据的。所以，当整数直接量赋给long、float或者double，而不添加尾缀，虚拟机也会直接将int类型数据自动转换为对应类型然后赋值。因为数据长度短的转换为长的并不会造成数据丢失，所以默认可以自动转换。　
例如：

long  lNum  = 5;   //不报错，因为int自动转换为long类型，不会报错
float fNum  = 7;   //不报错，因为int自动转换为float类型，不会报错
double dNum = 10;  //同上

但是，**当浮点直接量（例如：1.2等），JVM虚拟机默认为double类型，**如果直接赋值给float就会引起编译器报错。

float fNum  = 1.2; //报错，因为1.2虚拟机是默认为double类型，不能直接赋值给float类型变量
float fNew  = 1.3f;//正确，因为尾缀添加了f，即告诉了虚拟机1.3属于float类型变量

总结
所以，当Java中遇到这三种类型变量需要赋直接量时候，最好都添加上相应的尾缀。这样不仅会防止编译器报错，也会增加程序的可读性。
　　但是下面这种情况就算添加尾缀也是错的，因为尾缀仅是为了告诉虚拟机该直接数属于什么数据类型，而不能实现数据类型强制转换。

long lNum = 1.2L;      //错误，double类型数据不能直接赋值给long类型
long lNew = (long)1.2; //正确，double类型数据强制转换为long类型

#### 7.5包装类、8基本数据类型的包装类

| 基本数据类型 | 引用数据类型 |
| ------------ | ------------ |
| byte         | Byte         |
| short        | Short        |
| int          | Integer      |
| long         | Long         |
| char         | Character    |
| float        | Float        |
| double       | Double       |
| boolean      | Boolean      |



集合和泛型支持包装类不支持基本数据类型

**变成类了！（重要理解！）**



```java
public static void main(String[] args) {
   // Integer integer1 = new Integer(1);  //注意new Integer方法提示过时
    Integer integer2 = 1;
    Integer integer = Integer.valueOf(1);
    System.out.println(integer==integer2);  //true
        integer=integer2;
        integer=2;
        System.out.println(integer2);  //依旧是1

    Integer integer3 = 200;
    Integer integer4 = Integer.valueOf(200);
    System.out.println(integer3==integer4);  //false
    
    Integer integer5 = Integer.parseInt("1");
    System.out.println(integer2==integer5);  //true
    System.out.println(integer5.toString());
}
```

1． 尽量使用values方法。最大可能使用缓存，提高程序的效率。

2． 类变量使用包装类。想象有一个和数据库表对应的实体类，如果你使用的基本数据类型，在插入时，可能会插入一些让你意想不到的初始值。

3． 方法的参数要使用包装类。使用包装类意味着你在调用时，可以令若干个参数为null。null是无意义的。但是如果你使用了基本数据类型，那么，你将不得不传入一个值，即使这个值对你来说，没有什么意义。

4． 方法的返回值要根据是否可为null来确定使用包装类还是基本类。当一个方法的返回值，一定不会出现null的情况时，推荐使用基本类来作为返回值。这样，调用者在拿到这个方法的返回值时，就不必担心它是为null了。

5． 方法内部(局部变量)使用基本类型。基本类型的时间效率和效率上来说，都是要优于包装类的。所以，在方法内部，能使用基本类型尽量不要使用包装类。

6． 小数的计算。严格来说，这条不属于基本类型和包装类的内容，但是，这里顺便提交，当涉及到小数的计算时，要考虑到计算的精度问题，可以使用BigDecimal，也可以通过缩小计量单位，达到化零为整的目的，这个，根据具体场景来确定。

### 8.自动类型转换

类型范围小的变量，可以直接赋值给类型范围大的变量。

表达式的最终结果类型由表达式中的最高类型决定。（**有些时候/2  除2  还是用/2.0 吧**）

在表达式中，byte、short、char 是直接转换成int类型参与运算的。 

a+=b 等价于 a = (a的数据类型)(a+b); 将a + b的值给a

### 9.三目运算符

条件表达式 ?  值1 : 值2;

### 10.运算符优先级

需要注意的是&>^>|

^  异或、相同为false不同为true



9^2=11,11^2=9
^符号是位逻辑运算符里的按位异或，只有在两个比较的位不同时结果是1，否则为0.
分析：
9 二进制：1 0 0 1
2 二进制：0 0 1 0
9^2 结果： 1 0 1 1 转换为十进制：8+2+1=11



System.out.println(10 > 3 || 10 > 3 && 10 < 3);  // true

System.out.println( (10 > 3 || 10 > 3 ) && 10 < 3);  // false

### 11.流程控制

#### 11.1 if&else

if(){}else{}

#### 11.2 switch(注意穿透)

switch(表达式){
   case 值1:
     执行代码...;
     break;
   case 值2:
     执行代码...;
     break;

​      … 
   case 值n-1:
​     执行代码...;
​     break;
   default:
​     执行代码n;
 }

①表达式类型只能是byte、short、int、char，JDK5开始支持枚举，JDK7开始支持String、不支持double、float、long。

②case给出的值不允许重复，且只能是字面量，不能是变量。

③不要忘记写break，否则会出现穿透现象。

如果代码执行到没有写break的case块，执行完后将直接进入下一个case块执行代码（而且不会进行任何匹配），直到遇到break才跳出分支，这就是switch的穿透性。(常见面试题)

```java
public class Switch_Study {
    public static void main(String[] args) {
        int n = 2;
        switch (n){
            case 1:
                System.out.println("1");
            case 2:
                System.out.println("2");
            default:
                System.out.println("default");
        }
    }
}
```

没有break语句、穿透了、输出2和default

#### 11.3 for 循环

数组或集合使用  其变量.for  即可

#### 11.4 while、do-while

注意while语句内需要有能使判断条件变为false的语句（自增什么的）。

break  : 跳出并结束当前所在循环的执行、或case分支。

continue: 用于跳出当前循环的当次执行，进入下一次循环。

## 四.常用进阶

### 1.随机Random类

nextInt(n)功能只能生成：0 – (n-1)之间的随机整数

```java
import java.util.Random;

public class Random_Study {
    public static void main(String[] args) {
        Random random = new Random();
        System.out.println(random.nextInt(2));
    }
}
```

只能随机生成0或1

### 2.Scanner输入

```java
import java.util.Scanner;

public class Scanner_study {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println(scanner.next());
    }
}
```

System、String在JDK中的Java.lang包下
 lang包不需要我们导包，是默认的包。

### 3.数组

#### 3.1数组的初始化

静态初始化：定义数组的时候直接给数组赋值。

完整格式
数据类型[] 数组名 = new 数据类型[]{元素1，元素2 ，元素3… };

double[] scores = new double[]{89.9, 99.5, 59.5, 88.0};
 int[] ages = new int[]{12, 24, 36}

简化格式

数据类型[] 数组名 = { 元素1，元素2 ，元素3，… };
 int[] ages = {12, 24, 36};

动态初始化：定义数组的时候只确定元素的类型和数组的长度，之后再存入具体数据。

数据类型[] 数组名 = new 数据类型[长度];
 int[] arr = new int[3];

#### 3.2数组的长度.length

#### 3.3数组操作工具类Arrays；Comparator比较器（重要）

| 方法名                                                       | 说明                                             |
| ------------------------------------------------------------ | ------------------------------------------------ |
| public static [String](mk:@MSITStore:C:\course\API文档\jdk-9_google.CHM::/java/lang/String.html) toString(类型[] a) | 返回数组的内容（字符串形式）                     |
| public  static void sort(类型[] a)                           | 对数组进行默认升序排序                           |
| public  static <T> void sort(类型[] a, [Comparator](mk:@MSITStore:C:\course\API文档\jdk-9_google.CHM::/java/util/Comparator.html)<?  super T> c) | 使用比较器对象自定义排序                         |
| public  static int binarySearch(int[] a,  int key)           | 二分搜索数组中的数据，存在返回索引，不存在返回-1 |

```java
public static void main(String[] args) {
    int[] arr = {1,3,2,5,4};
    System.out.println(Arrays.binarySearch(arr, 2));//返回索引
    System.out.println(Arrays.toString(arr));
    Arrays.sort(arr); //默认升序排序
    System.out.println(Arrays.toString(arr));
}
```

```java
    public static void main(String[] args) {
        Student student1 = new Student("乔治", 5);
        Student student2 = new Student("佩奇", 6);
        Student student3 = new Student("佩奇", 4);
        Student[] students = {student1,student2,student3};
        System.out.println(Arrays.toString(students));
//[Student{name='乔治', age=5}, Student{name='佩奇', age=6}, Student{name='佩奇', age=4}]
        Arrays.sort(students, new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
               return o2.getAge()-o1.getAge();  //降序
            }
        });

        System.out.println(Arrays.toString(students));
//[Student{name='佩奇', age=6}, Student{name='乔治', age=5}, Student{name='佩奇', age=4}]
    }
```

return o2.getAge()-o1.getAge();  //降序

o1.getAge()-o2.getAge(); //升序

**记得**

**return o1-o2  升序**

**return o2-o1  降序**

以下为一些网上找到的理解

对于o1、o2、返回正数则交换位置、负数则不交换位置

- 对于o1-o2若大于零为正数、则o1>o2、交换位置、还是为升序
- 对于o1-o2若小于零为负数、则o1<o2、不交换位置、还是升序
- 对于o2-o1若大于零为正数、则o1<o2、交换位置、还是为降序
- 对于o2-o1若小于零为负数、则o1>o2、不交换位置、还是降序



### 4.java内存分配介绍

![jn](images\jn.png)

![jn2](images\jn2.png)

方法是放在方法区中的，被调用的时候，需要进入到栈内存中运行

栈内存中保存的变量保存的是堆内存中new出来的对象的首地址

引用类型数组、栈中保存了其变量名指向该引用型数组的首地址、然后堆内存中该引用数组内部也保存的是new出来相关对象的地址、具体的对象依旧散在堆内存中。

此时打印数组（arr）打印地址

若相关类重写了toString方法、则打印其栈内变量时打印内容（默认调用其tostring方法）

### 5.常见异常

![Snipaste_2022-12-13_23-38-57](images\Snipaste_2022-12-13_23-38-57.png)



常见运行时异常：

- 数组越界异常ArrayIndexOutOfBoundsException
- 空指针异常（就是使用了   null.方法  ）对象还没有初始化给值、或为空就调用了其方法NullPointerException
- 类转换异常 如果转型后的类型和对象真实对象的类型不是同一种类型，那么在运行代码时，就会出现ClassCastException
- 元素越界异常、例如迭代器iterator遍历集合取元素时没有提取判断hasnext()的时候NoSuchElementException异常
- 数字操作异常ArithmeticException
- 数字转换异常NumberFormatException

编译时异常：目的在于提醒不要出错!

如：ParseException

**默认异常处理机制**

![Snipaste_2022-12-13_23-48-43](images\Snipaste_2022-12-13_23-48-43.png)

**自己处理方式**

try、catch、finally



方法 throws 异常1 ，异常2 ，异常3 ..{
 }



方法 throws Exception{
 }



try{
    // 监视可能出现异常的代码！
  }catch(异常类型1 变量){
    // 处理异常
 }catch(异常类型2 变量){
    // 处理异常
 }...



try{
   // 可能出现异常的代码！
 }catch (Exception e){
   e.printStackTrace(); // 直接打印异常栈信息
 }


 Exception可以捕获处理一切异常类型！

try、catch、finally

### 6.Debug

打断点、点击调试

![图片1](images\图片1.png)

step over  不进入方法内向下走

step into   进入方法内向下走

force step into 进入源码方法内部向下走

step out    跳出方法

### 7.方法（调用）

不带static的实例方法通过new其对象.方法调用

带static的静态方法直接使用类名.方法（其使用变量也需是静态的）

```java
import java.util.Arrays;

public  class People {
    static int a = 1;
    public static void speak(String ...abc){
        System.out.println(Arrays.toString(abc));
    }
}
```

方法中不能嵌套定义另一个方法、但可以使用其它方法包括自己

String ...abc定义接收未知个数参数（若有其它参数、只能放在最后）

都是值传递。

基本类型的参数传输存储的数据值。

引用类型的参数传输存储的地址值。

方法重载：同一个类中，多个方法的名称相同，形参列表不同。形参的个数、类型、顺序不同，不关心形参的名称。

方法重写：子类重写父类方法。



```java
public class MyTest {
    public static void main(String[] args) {
        Student student1 = new Student("佩奇", 6);

        abc(student1); //14

        System.out.println(student1); //14

    }
    static void abc(Student student){
        student.setAge(14);
        System.out.println(student);
    }
}
```

就是值传递、传入地址值、不过相当于人家方法内部进入你家地址做了一些改变

### 8.对象

当堆内存中的对象，没有被任何变量引用（指向）时，就会被判定为内存中的“垃圾”。Java存在自动垃圾回收器，会定期进行清理。

### 9.this关键字

可以出现在构造器、方法中代表当前对象的地址。

可以用于指定访问当前对象的成员变量、成员方法。

### 10.面向对象的三大特征：封装，继承，多态。

### 11.成员变量与局部变量

| 区别         | 成员变量                                   | 局部变量                                       |
| ------------ | ------------------------------------------ | ---------------------------------------------- |
| 类中位置不同 | 类中，方法外                               | 常见于方法中                                   |
| 初始化值不同 | 有默认值,无需初始化                        | 没有默认值，使用之前需要完成赋值               |
| 内存位置不同 | 堆内存                                     | 栈内存                                         |
| 生命周期不同 | 随着对象的创建而存在，随着对象的消失而消失 | 随着方法的调用而存在，随着方法的运行结束而消失 |
| 作用域       |                                            | 在所归属的大括号中                             |

## 五.高级进阶

### 1.String类

| 构造器                         | 说明                                   |
| ------------------------------ | -------------------------------------- |
| public String()                | 创建一个空白字符串对象，不含有任何内容 |
| public String(String original) | 根据传入的字符串内容，来创建字符串对象 |
| public String(char[] chs)      | 根据字符数组的内容，来创建字符串对象   |
| public String(byte[] chs)      | 根据字节数组的内容，来创建字符串对象   |

java.lang.String 类代表字符串，String类定义的变量可以用于指向字符串对象，然后操作该字符串。

Java 程序中的所有字符串文字（例如“abc”）都为此类的对象。

#### 1.-1字符和编码

| 方法名称                            | 说明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| byte[] getBytes()                   | 使用平台的默认字符集将该  String编码为一系列字节，将结果存储到新的字节数组中 |
| byte[] getBytes(String charsetName) | 使用指定的字符集将该 String编码为一系列字节，将结果存储到新的字节数组中 |

| 构造器                                   | 说明                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| String(byte[] bytes)                     | 通过使用平台的默认字符集解码指定的字节数组来构造新的  String |
| String(byte[] bytes, String charsetName) | 通过指定的字符集解码指定的字节数组来构造新的 String          |

```java
public static void main(String[] args) {
    byte[] bytes = "八十天环游地球".getBytes(StandardCharsets.US_ASCII);
    System.out.println(new String(bytes, StandardCharsets.UTF_8)); //???????
}
```

#### 1.0**关于String类为什么不用new（）**

1. jvm为了提升性能和减少内存开销，避免字符的重复创建，其维护了一块特殊的内存空间，即字符串常量池，用来存储字符串常量。
2. 使用String直接赋值: String str=“abc”:可能创建一个或者不创建对象，如果”abc”在字符串池中不存在，会在java字符串池中创建一个String对象(”abc”)，然后str指向这个内存地址，无论以后用这种方式创建多少个值为”abc”的字符串对象，始终只有一个内存地址被分配。 
2. 使用new String()赋值: String str=newString(“abc”);至少会创建一个对象，也有可能创建两个。因为用到new关键字，肯定会在堆中创建一个String对象，如果字符池中已经存在”abc”，则不会在字符串池中创建一个String对象，如果不存在，则会在字符串常量池中也创建一个对象。

因此，直接赋值产生1或0个对象，使用newString()赋值时产生2或1对象，赋值时先看字符串常量池，如果字符串常量池中没有，就在常量池中创建一个，如果有，前者直接引用，后者在堆内存中还需创建一个“abc”实例对象(此时引用变量指向的是堆内存中创建的实例对象，而不是常量池中的实例对象)。

知识点：关于String字符串拼接

1. 字符串拼接分为变量拼接和已知字符串拼接

String str="abc"; //在常量池中创建abc
String str1="abcd"://在常量池中创建abcd
String str2=str+"d";//拼接字符串，此时会在堆中新建一个abcd的对象，因为str2编译之前是未知的
String str3="abc"+"d";//拼接之后str3还是abcd，所以还是会指向字符串常量池的内存地址
System.out.println(str1==str2); //false 
System.out.println(str1==str3);//true
为什么给str3赋值时不会在堆中创建一个对象，而给str2赋值时却会在堆中创建一个对象?

编译期: 是指把源码交给编译器编译成计算机可以执行的文件的过程。在Java中也就是把Java代码编成class文件的过程。编译期只是做了一些翻译功能，并没有把代码放在内存中运行起来，而只是把代码当成文本进行操作，比如检查错误。

运行期: 是把编译后的文件交给计算机执行，直到程序运行结束。所谓运行期就把在磁盘中的代码放到内存中执行起来。在Java中把磁盘中的代码放到内存中就是类加载过程。

str3="abc"+"d"其实就等同于字面量赋值(即等同于str3="abcd")。 String str2=str+"d":在编译时将str看作一个引用类型变量，此时就会把str2认为是以newString0方式来创建的，堆内存中就会开辟空间，然后创建对象，接着再把空间的地址值返回给str2。


String其实常被称为不可变字符串类型，它的对象在创建后不能被更改。

#### 1.1intern()方法

理解、返回字符串在字符串常量池中的引用、（因为有时你的指向为堆内存中的那个new出来的引用！）

尽管在输出中调用intern方法并没有什么效果，但是实际上后台这个方法会做一系列的动作和操作。在调用”ab”.intern()方法的时候会返回”ab”，但是这个方法会首先检查字符串池中是否有”ab”这个字符串，如果存在则返回这个字符串的引用，否则就将这个字符串添加到字符串池中，然会返回这个字符串的引用。

#### 1.2查看equeals方法

以下是String类内的equals方法、看出是比较值是否相同；如果地址相同为同一对象直接返回true了、我们知道直接赋值将指向字符串常量池中、而使用new字符串时是指向堆内存中的、所以有时即使值相等但比较地址并不相等。

所以比较值即使地址不同依旧需要接着操作



coder为1时为UTF-16一个字符占两个字节

coder为0时为LATIN1一个字符占一个字节（虽节省了空间但字符表示并不完全）

![Snipaste_2022-11-26_14-54-41](images\Snipaste_2022-11-26_14-54-41.png)

![Snipaste_2022-11-26_14-55-38](images\Snipaste_2022-11-26_14-55-38.png)

可以看到在调试过程中印证了

比较“我”时coder为1

比较“a”时coder为0

此外COMPACT_STRINGS默认为true表示开启了不同编码

第一步：确认是相同字符串类

第二步：!COMPACT_STRINGS如果开启了不同编码则为false、此时必须要求后面的coder相等第二步才为true

​              !COMPACT_STRINGS如果关闭了不同编码则为true、此时后面条件直接就不再比较了。

第三步：就是比较值是否相等了

```java
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    return (anObject instanceof String aString)
            && (!COMPACT_STRINGS || this.coder == aString.coder)
            && StringLatin1.equals(value, aString.value);
}
```



#### 1.3关于自定义类的equals方法

```java
public class Student {
    private String name;
    private Integer age;
    
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return Objects.equals(name, student.name) && Objects.equals(age, student.age);
    }
}
```

如果不重写类中的equals方法、比较地址、重写后比较值相等，

```java
public class Equals_ss {
    public static void main(String[] args) {
        Student student1 = new Student("佩奇", 6);
        Student student2 = new Student("佩奇", 6);
        System.out.println(student1.equals(student2));
    }
}
```

未重写时走的时Object类中的equals方法

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

输出false



重写equals方法后

```java
public class Student {
    private String name;
    private Integer age;
    
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Student student = (Student) o;
        return Objects.equals(name, student.name) && Objects.equals(age, student.age);
    }
}
```

输出true

#### 1.5String类常用方法

| 方法名                                                       | 说明                                                     |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| public int length()                                          | 返回此字符串的长度                                       |
| public char charAt(int index)                                | 获取某个索引位置处的字符                                 |
| public char[] toCharArray()：                                | 将当前字符串转换成字符数组返回                           |
| public String substring(int beginIndex, int endIndex)        | 根据开始和结束索引进行截取，得到新的字符串（包前不包后） |
| public String substring(int beginIndex)                      | 从传入的索引处截取，截取到末尾，得到新的字符串           |
| public String replace(CharSequence target, CharSequence replacement) | 使用新值，将字符串中的旧值替换，得到新的字符串           |
| public String[] split(String regex)                          | 根据传入的规则切割字符串，得到字符串数组返回             |

### 1.5 toString方法

默认是返回当前对象在堆内存中的地址信息:类的全限名@内存地址

toString方法与equals方法一样、在父类Object内、就是用来让子类重写的

子类对象重写toString方法后就可以直接打印了（自动生成）

### 1.55 Objects工具类

Objects.equals(Object a,Object b)

```java
public static boolean equals(Object a, Object b) {
    return (a == b) || (a != null && a.equals(b));
}
```

Objects.equals(Object a,Object b)依旧是依赖您类中重写的equals方法、没有重写则依旧比较地址



Objects.isNull(Object obj)

```java
public static boolean isNull(Object obj) {
    return obj == null;
}
```



Objects.toString(Object obj,String nullDefault)

```java
Objects.toString(student2, "为空")
```

```java
public static String toString(Object o, String nullDefault) {
    return (o != null) ? o.toString() : nullDefault;
}
```

Objects.toString(Object obj)依旧是依赖您类中重写的toSting方法、没有重写则输出地址、为null则输出“为空”。

### 1.555 StringBuilder概述

StringBuilder是一个可变的字符串的操作类，我们可以把它看成是一个对象容器。

使用StringBuilder的核心作用：操作字符串的性能比String要更高（如拼接、修改等）。

| 构造器                            | 说明                                           |
| --------------------------------- | ---------------------------------------------- |
| public  StringBuilder()           | 创建一个空白的可变的字符串对象，不包含任何内容 |
| public  StringBuilder(String str) | 创建一个指定字符串内容的可变字符串对象         |

| 方法名称                              | 说明                                                |
| ------------------------------------- | --------------------------------------------------- |
| public StringBuilder append(任意类型) | 添加数据并返回StringBuilder对象本身                 |
| public StringBuilder reverse()        | 将对象的内容反转                                    |
| public int length()                   | 返回对象内容长度                                    |
| public String toString()              | 通过toString()就可以实现把StringBuilder转换为String |

StringBuilder：内容是可变的、拼接字符串性能好、代码优雅。
String ：内容是不可变的、拼接字符串性能差。

定义字符串使用String
拼接、修改等操作字符串使用StringBuilder

```java
public class StringBuilder_s {
    public static void main(String[] args) {
        StringBuilder stringBuilder = new StringBuilder("a");
        StringBuilder stringBuilder1 = stringBuilder.append("b").append("c").append(1);
        System.out.println(stringBuilder1);       //abc1
        System.out.println(stringBuilder1.reverse());   //1cba
        String str = stringBuilder1.toString();
        System.out.println(str);                  //1cba
    }
}
```

### 2.ArrayList

| 方法名                               | 说明                               |
| ------------------------------------ | ---------------------------------- |
| public boolean add(E e)              | 将指定的元素追加到此集合的末尾     |
| public void add(int index,E element) | 在此集合中的指定位置插入指定的元素 |

| 方法名称                          | 说明                                   |
| --------------------------------- | -------------------------------------- |
| public E get(int  index)          | 返回指定索引处的元素                   |
| public int  size()                | 返回集合中的元素的个数                 |
| public E remove(int  index)       | 删除指定索引处的元素，返回被删除的元素 |
| public boolean remove(Object o)   | 删除指定的元素，返回删除是否成功       |
| public E set(int index,E element) | 修改指定索引处的元素，返回被修改的元素 |

### 3.static关键字

- static修饰成员变量之后称为静态成员变量（类变量）、修饰方法之后称为静态方法（类方法）、在方法区。

- 静态成员变量（有static修饰，属于类、加载一次，内存中只有一份），访问格式

  ​      类名.静态成员变量(推荐)

  ​      对象.静态成员变量(不推荐)。

- 静态成员方法（有static修饰，归属于类），建议用类名访问，也可以用对象访问。

- 实例成员方法（无static修饰，归属于对象），只能用对象触发访问。

- 表示对象自己的行为的，且方法中需要访问实例成员的，则该方法必须申明成实例方法。

- 如果该方法是以执行一个共用功能为目的，则可以申明成静态方法。

- 静态方法只能访问静态的成员，不可以直接访问实例成员。

- 实例方法可以访问静态的成员，也可以访问实例成员。

- 静态方法中是不可以出现this关键字的。

### 4.代码块（静态非静态）

**代码块分为**

**静态代码块**:

**格式**：static{}

**特点**：需要通过static关键字修饰，随着类的加载而加载，并且自动触发、只执行一次

**使用场景**：在类加载的时候做一些静态数据初始化的操作，以便后续使用。



 **构造代码块**（**了解，见的少**）：

**格式**：{}

**特点**：每次创建对象，调用构造器执行时，都会执行该代码块中的代码，并且在构造器执行前执行

**使用场景**：初始化实例资源。

### 5.继承extends

不支持多继承、但支持多层继承

可以通过super关键字，指定访问父类的成员。

继承后便可进行方法重写了@Override、不能重写私有及静态方法。子类重写父类方法时，访问权限必须大于或者等于父类被重写的方法的权限。缺省 < protected < public

子类中所有的构造器默认都会先访问父类中无参的构造器，再执行自己。

子类构造器的第一行语句默认都是：**super()**，不写也存在。

子类初始化之前，一定要调用父类构造器先完成父类数据空间的初始化。

子类构造器中可以通过书写 super(…)，手动调用父类的有参数构造器

| **关键字** | **访问成员变量**                 | **访问成员方法**                    | **访问构造方法**              |
| ---------- | -------------------------------- | ----------------------------------- | ----------------------------- |
| **this**   | this.成员变量  访问本类成员变量  | this.成员方法(…)  访问本类成员方法  | **this(…)**  **访问本类构器** |
| **super**  | super.成员变量  访问父类成员变量 | super.成员方法(…)  访问父类成员方法 | super(…)  访问父类构造器      |

### 6.package包

一个类中需要导入多个同名其它类使用包名.类名

```java
import org.my.dao.Student;
//import org.my.pojo.Student;    //同时出现报错

public class MyTest {
    public static void main(String[] args) {
        Student student1 = new Student("佩奇", 6);
        org.my.pojo.Student student2 = new org.my.pojo.Student("乔治", 5);
        org.my.dao.Student student3 = new org.my.dao.Student("苏西", 6);

  //      System.out.println(student1);
        System.out.println(student2);
        System.out.println(student3);
    }
}
```

### 7.权限修饰符

| **修饰符** | **同一 个类中** | **同一个包中**  **其他类** | **不同包下的**  **子类** | **不同包下的**  **无关类** |
| ---------- | --------------- | -------------------------- | ------------------------ | -------------------------- |
| private    | √               |                            |                          |                            |
| 缺省       | √               | √                          |                          |                            |
| protected  | √               | √                          | √                        |                            |
| public     | √               | √                          | √                        | √                          |

### 8.final关键字

- final 关键字是最终的意思，可以修饰（类、方法、变量）
- 修饰类：表明该类是最终类，不能被继承。
- 修饰方法：表明该方法是最终方法，不能被重写。
- 修饰变量：表示该变量第一次赋值后，不能再次被赋值(有且仅能被赋值一次)。
- **修饰成员变量要先赋值、或在构造器中加参、修饰静态成员变量则必须先赋值了、此时使用public修饰就是所谓“常量”、new一个空对象也是赋值了、地址值。**

1. final修饰的变量是基本类型：那么变量存储的数据值不能发生改变。
2. final修饰的变量是引用类型：那么变量存储的地址值不能发生改变，但是地址指向的对象内容是可以发生变化的。

```java
public static void main(String[] args) {
   final Student student1 = new Student("佩奇", 6);
   Student student2 = new Student("佩奇2", 6);
   
    student1.setAge(11);    //不报错、地址不能变、值可以变
    student2.setAge(12);
    System.out.println(student1);
    System.out.println(student2);

 //   student1=student2;  //报错、地址不能变、值可以变
    student2=student1;  //不报错
    student1.setAge(21);
    student2.setAge(22);
    System.out.println(student1);
    System.out.println(student2);
}
```

### 9.常量

常量是使用了public static final修饰的成员变量，必须有初始化值，

在编译阶段会进行“宏替换”：把使用常量的地方全部替换成真实的字面量。

### 10.枚举enum关键字

```java
enum Enum_s {
    Spring("pq",20),Summer,Autumn,Winter;
    private String name;
    private Integer age;

    Enum_s() {
    }

    Enum_s(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Enum_s{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

```java
public static void main(String[] args) {
    System.out.println(Enum_s.Spring);
    System.out.println(Enum_s.Summer);
    Enum_s autumn = Enum_s.Autumn;
    Enum_s winter = Enum_s.Winter;
    autumn.setAge(1);
    winter=autumn;
 //   Enum_s.Winter=Enum_s.Autumn;    //报错
    System.out.println(winter.getAge());
}
```



![Snipaste_2022-11-27_16-42-25](images\Snipaste_2022-11-27_16-42-25.png)

不过多例模式并不需要final关键字

**（Season枚举类就是创建了几个类型为Season的常量）**

枚举类默认修饰符为public、构造器默认私有private、没写也是。

### 11.抽象类abstract关键字

- 在Java中abstract是抽象的意思，可以修饰类、成员方法。
- abstract修饰类，这个类就是抽象类；修饰方法，这个方法就是抽象方法。
- 抽象方法：只有方法签名、不能声明方法体
- 一个类中如果定义了抽象方法，这个类必须声明成抽象类，否则报错。
- 抽象类中不一定有抽象方法，有抽象方法的类一定是抽象类
- 一个类如果继承了抽象类，那么这个类必须重写完抽象类的全部抽象方法，否则这个类也必须定义成抽象类。

### 12.接口interface

public **interface** 接口名 {

​    // 常量

​    // 抽象方法

} 

JDK8之前接口中只能是抽象方法和常量，没有其他成分了。

**接口中写变量要赋值初始化、即使不写也默认有public、static、final修饰 //常量**

**接口中写方法即使不写也默认有public、abstract修饰**

**（为方便理解、以上两行一定要记牢）**

一个类实现多个接口，多个接口中有同样的静态方法不冲突。
一个类继承了父类，同时又实现了接口，父类中和接口中有同名方法，默认用父类的。
一个类实现了多个接口，多个接口中存在同名的默认方法，可以不冲突，这个类重写该方法即可。

但相同名称返回值不同依旧报错

### 13.接口和抽象类

均不能实例化、创建对象

抽象类用extends关键字单继承但可以传递继承，接口implements可以多实现。

个人理解{

抽象类就是有几个抽象方法于是就加上了abstract关键字、于是类也变成了抽象类、其他类继承后先重写所有抽象方法或接着定义为抽象类

接口就是可被多实现的内部只有常量与抽象方法（jdk8之前）的抽象类、变为interface关键字（更具模板规范专业性一点了）

}

jdk8后接口又可以添加默认方法了、有方法体但需default关键字修饰、默认被public修饰、通过接口实现类的对象调用。

jdk8后接口又可以添加静态方法了、有方法体但需static关键字修饰、默认被public修饰、通过本身接口名调用。

jdk9后接口又可以添加私有方法了、有方法体必须使用private修饰、只能在本类中被其他的默认方法或者私有方法访问。

原因：多个实现类实现了接口、后需丰富接口功能、但又不想所有实现类均重写抽象方法。



接口----->抽象类----->实现类

直接实现接口时需全部实现其中的抽象方法、当我们不想实现接口中的全部方法时、可以做个抽象类实现接口（因为抽象类不必实现另一个抽象类的全部抽象方法）中我们不想实现的方法（为空或按需求写方法体）然后我们只需继承这个抽象类就只要求实现接口中未在抽象类中重写过的方法。

例：当我们新建实体类只想实现接口interface里的a方法时、

接口interface内有a、b两抽象方法、我们做个抽象类abstract去仅重写其b方法、当我们新建实体类实现类继承抽象类abstract时、只会强制要求你重写a方法。

### 14.内部类

#### 14.1静态内部类

有static修饰，属于外部类本身。
它的特点和使用与普通类是完全一样的，类有的成分它都有，只是位置在别人里面而已。

public class Outer{

​    // 静态成员内部类
​     public static class Inner{
​     }
 }

格式：外部类名.内部类名 对象名 = new 外部类名.内部类构造器;
 范例：Outer.Inner in =  new Outer.Inner();

```java
public class StaticInner {
    private int a = 10;
    private static int b = 20;
    static class InnerClass{
        public static void main(String[] args) {
         //   System.out.println(a);    //报错
            System.out.println(b);
        }
        
    }
}
```

```java
public class MyTest {
    public static void main(String[] args) {
        StaticInner.InnerClass innerClass = new StaticInner.InnerClass();
        System.out.println(innerClass);
    }
}
```

#### 14.2成员内部类

无static修饰，属于外部类的对象。
JDK16之前，成员内部类中不能定义静态成员，JDK 16开始也可以定义静态成员了。

**怎么访问成员内部类里的静态变量（JDK16后）------Outer.Inner.变量**

public class Outer {

​    // 成员内部类

​    public class Inner {

​        }

}

格式：外部类名.内部类名 对象名 = new  外部类构造器.new 内部类构造器();

范例：Outer.Inner in =  new Outer().new  Inner();

**注意两个new！**

#### 14.3关于访问变量

**静态变量方法是随着类加载在内存中便存在一份被共享访问、访问时使用 类名.变量**

**正常的成员变量方法是只有当你new出相应类对象时才被加载、访问时使用 对象.变量**

**所以看能不能访问到相应变量，一般静态都能访问到、普通成员变量在有相应对象后才能访问到**

**所以静态内部类可以直接访问外部静态变量、需使用外部类对象访问普通变量**

**而成员内部类可以直接访问到静态、普通成员变量、因为你成员内部类是需要你new出来当使用new Outer().new  Inner()后就已经有相应对象了、自然可以访问到。**

**在成员内部类中访问所在外部类对象格式：外部类名.this。**

```java
public class StaticInner {
    private int a = 10;
    private static int b = 20;
     static class InnerClass{
        public static void main(String[] args) {
            StaticInner staticInner = new StaticInner();
            System.out.println(staticInner.a);
            //   System.out.println(a);    //报错
            System.out.println(b);
        }

    }
}
```

```java
public class PtInner {
    private int a = 10;
    private static int b = 20;

    public  class InnerClass1{
        public  void meth() {
            System.out.println(a);    //不报错
            System.out.println(b);
        }
    }
    
}
```

对于普通成员内部类、里面写Main方法也没用、不能运行、所以另找类使用来测试

```java
PtInner.InnerClass1 innerClass1 = new PtInner().new InnerClass1();
innerClass1.meth();
```

```java
public class PtInner {
    private int a = 10;
    private static int b = 20;

    public  class InnerClass1{
        private int a = 20;
        public  void meth() {
            int a = 30;
            System.out.println(PtInner.this.a); //10
            System.out.println(this.a);  //20
            System.out.println(a);  //30
            PtInner ptInner = new PtInner();
            System.out.println(ptInner.a);  //10
            System.out.println(b);  //20
        }
    }

}
```

#### 14.4匿名内部类

本质上是一个没有名字的局部内部类。
作用：方便创建子类对象，最终目的是为了简化代码编写。

匿名内部类是一个没有名字的内部类，同时也代表一个对象。
匿名内部类产生的对象类型，相当于是当前new的那个的类型的子类类型。

```java
public class NoNameClass {
    public static void main(String[] args) {
        People p = new People() {         //接口不能创建对象、此处是相当于匿名实现类、子类
            @Override
            public void eat() {
                System.out.println("吃了");
            }

            @Override
            public void sleep() {
                System.out.println("睡了");

            }
        };
        p.eat();
        p.sleep();
    }
}

interface People{
    void eat();
    void sleep();
}
```

```java
public class NoNameClass {
    public static void main(String[] args) {
        People p = new People() {         //创建的是People子类对象、这是多态写法
            @Override
            public void eat() {
                System.out.println("吃了");
            }

            @Override
            public void sleep() {
                System.out.println("睡了");

            }
        };
        p.eat();
        p.sleep();
    }
}

class People{
    void eat(){};
    void sleep(){};
}
```

```java
public class NoNameClass {
    public static void main(String[] args) {
        People p = new People() {         //相当于new了一个匿名实现类、子类
            @Override
            public void eat() {
                System.out.println("吃了");
            }

            @Override
            public void sleep() {
                System.out.println("睡了");

            }
        };
        p.eat();
        p.sleep();
       
    }
}

abstract class People{
    abstract void eat();
    abstract void sleep();
}
```

匿名内部类主要还是作为参数使用

最主要用法还是以下：14.5

#### 14.5Lambda表达式

```java
public class NoNameClass {
    public static void meth(People people){
        people.sleep();
    }
    public static void main(String[] args) {
        meth(new People() {        //接口不能创建对象、此处依旧是其实现类
            @Override
            public String sleep() {
                return "你好！";
            }
        });
    }
}

interface People{
    String sleep();
}
```

简化为

```java
public class NoNameClass {
    public static void meth(People people){
        people.sleep();
    }
    public static void main(String[] args) {
        meth(() -> "你好！");
    }
}

interface People{
    String sleep();
}
```

#### 

函数式接口：首先必须是接口、其次接口中有且仅有一个抽象方法的形式

**Lambda**表达式只能简化函数式接口的匿名内部类的写法形式

- 参数类型可以省略不写。
- 如果只有一个参数，参数类型可以省略，同时()也可以省略。
- 如果Lambda表达式的方法体代码只有一行代码。可以省略大括号不写,同时要省略分号！
- 如果Lambda表达式的方法体代码只有一行代码。可以省略大括号不写。此时，如果这行代码是return语句，必须省略return不写，同时也必须省略";"不写

```java
public class NoNameClass {

    public static void main(String[] args) {

        MyMath myAdd = (i,j)-> i+j;
        System.out.println(myAdd.num(1, 2));
        MyMath myDel = (i,j)->i-j;
        System.out.println(myDel.num(2, 1));
        
    }
}

interface MyMath{
    int num(int i,int j);
}
```

**一些Lambda表达式常用**

**Consumer、Predicate、Function、Comparator**

**挨个消费处理、做判断、做映射、做比较**，去看六、10stream流内容

**stream流中的、**

**1、peek、foreach**

**2、filter**

**3、map**

**4、max、sorted**

#### 14.6进一步了解::

##### 1.System.out::println

一个函数式接口：打印System.out::println

```java
@FunctionalInterface
public interface MyStudent<T> {
    void print(T t);
}
```

@FunctionalInterface标志一个函数式接口、如果写错了会报错

```java
public static void main(String[] args) {
    MyStudent<Student> myStudent = student -> System.out.println(student);
    MyStudent<Student> myStudent1 = System.out::println;

    Student student = new Student("佩奇", 6);
    myStudent.print(student); //Student{嘿嘿！name='佩奇', age=6}
    myStudent1.print(student); //Student{嘿嘿！name='佩奇', age=6}
}
```

##### 2.类名::方法

一个函数式接口：类名::方法

```java
@FunctionalInterface
public interface MyStudent<T> {
    Integer getAge(T t);
}
```

```java
public static void main(String[] args) {
    MyStudent<Student> myStudent = student -> student.getAge();
    MyStudent<Student> myStudent1 = Student::getAge;

    Student student = new Student("佩奇", 6);
    System.out.println(myStudent.getAge(student)); //6
    System.out.println(myStudent1.getAge(student)); //6
}
```

##### 3.类名::静态方法

一个函数式接口：类名::静态方法

```java
public static void main(String[] args) {
    MyStudent<String> student = s -> Integer.parseInt(s);
    MyStudent<String> student1 = Integer::parseInt;

    System.out.println(student.getAge("2")); //2
    System.out.println(student1.getAge("3")); //3
}
```

##### 4.类名::new

```java
@FunctionalInterface
public interface MyStudent3 {
    Student getStudent(String name,Integer age);
}
```

```java
public static void main(String[] args) {
    MyStudent3 student = (name,age)->{return new Student(name,age);};
    MyStudent3 student1 = (name,age)->new Student(name,age);
    MyStudent3 student2 = Student::new;


    System.out.println(student1.getStudent("佩奇",8));  //Student{嘿嘿！name='佩奇', age=8}

    System.out.println(student2.getStudent("乔治",6)); //Student{嘿嘿！name='乔治', age=6}
}
```

##### 5.外部实例::方法

```java
@FunctionalInterface
public interface MyStudent4 {
    Boolean isEquals(String str);
}
```

```java
public static void main(String[] args) {
    String name = "hei";
    MyStudent4 myStudent = str -> name.equals(str);
    MyStudent4 myStudent2 = name::equals;

    System.out.println(myStudent.isEquals("hei")); //true
    System.out.println(myStudent2.isEquals("hei2")); //false
}
```

### 15.时间API

**LocalDate**：不包含具体时间的日期。

**LocalTime**：不含日期的时间。

**LocalDateTime**：包含了日期及时间。

**Instant**：代表的是时间戳。

**DateTimeFormatter** 用于做时间的格式化和解析的

**Duration**:用于计算两个“时间”间隔

**Period**:用于计算两个“日期”间隔

**总结：就用LocalDateTime+DateTimeFormatter+ChronoUnit**

**另数据库中使用Timestamp类型、java中也使用Timestamp去接**

新建TimeStamp类

Timestamp timestamp = new Timestamp(时间毫秒值);  例如填入 date.getTime()



```java
import java.sql.Timestamp;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.time.*;
import java.time.format.DateTimeFormatter;
import java.time.temporal.TemporalAccessor;
import java.util.Date;

public class LocalDateTime_S {
    public static void main(String[] args) throws ParseException {
//////////////////LocalDateTime学习
        LocalDateTime now = LocalDateTime.now();
        System.out.println("今天为一年中的第"+now.getDayOfYear()+"天");
        System.out.println("今天星期"+now.getDayOfWeek());
        LocalDateTime plus10Days = now.plusDays(10L);
        System.out.println("10天后为："+plus10Days);

/////////////////LocalDateTime 转时间毫秒值
        long epochMilli1 = now.toInstant(ZoneOffset.of("+0")).toEpochMilli();
        long epochMilli3 = now.toInstant(ZoneOffset.UTC).toEpochMilli();
        System.out.println(epochMilli1);
        System.out.println(epochMilli3); //UTC与+0相等

        long epochMilli = now.toInstant(ZoneOffset.of("+8")).toEpochMilli();
        System.out.println(epochMilli);
        System.out.println(System.currentTimeMillis());  //+8是与当前系统时刻相等（亚洲/上海）


//////////////////TimeStamp转LocalDateTime
        Timestamp timestamp = Timestamp.from(Instant.now());
        LocalDateTime localDateTime = timestamp.toLocalDateTime();



//////////////////LocalDateTime转TimeStamp
        Timestamp timestamp1 = Timestamp.valueOf(localDateTime);
        Timestamp timestamp2 = Timestamp.valueOf("2022-12-01 23:46:00");

/////////////////////DateTimeFormatter学习
        DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
        String formatplus10Days = dateTimeFormatter.format(plus10Days);
        System.out.println("格式化好后10天后为："+formatplus10Days);
        LocalDateTime parse = LocalDateTime.parse("1999-01-11 00:00:00", dateTimeFormatter);
        System.out.println(parse);
        LocalDateTime birthDate = LocalDateTime.of(2002, 2, 14, 0, 0, 0);
        System.out.println(birthDate.isBefore(now));

        //   LocalDateTime parse = (LocalDateTime) dateTimeFormatter.parse("1999-01-11 00:00:00");   //类型转化失败
        //  SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        //   Date parse1 = (LocalDateTime) simpleDateFormat.parse("1999-01-11 00:00:00");         //类型转化失败






/////////////////////以下为Duration/Period学习
        Duration between = Duration.between(birthDate, now);
        System.out.println("咱已经活了"+between.toDays()+"天！");   //Duration最大只能比较到天

        Period betweenPeriod = Period.between(birthDate.toLocalDate(), now.toLocalDate());
        System.out.println("咱已经活了"+betweenPeriod.getYears()+"年！"+betweenPeriod.getMonths()+"月"+betweenPeriod.getDays()+"天！");
        // 注意此处getMonths()、getDays()、数值都很小、不是跨年计算

        System.out.println("咱已经活了"+ChronoUnit.YEARS.between(birthDate, now)+"年！");
        System.out.println("咱已经活了"+ChronoUnit.DAYS.between(birthDate, now)+"天！");
        System.out.println("咱已经活了"+ChronoUnit.MONTHS.between(birthDate, now)+"月！");  // ChronoUnit类可以用来更好的比较间隔


///////////////////////////以下为时间戳学习
        Instant instant = Instant.now();
        System.out.println("打印当前时间戳："+instant);

        LocalDateTime parse1 = LocalDateTime.ofInstant(instant, ZoneId.systemDefault());
        System.out.println("打印当前时间戳转为LocalDateTime、ZoneId.systemDefault："+parse1);

        System.out.println("打印LocalDateTime、ZoneId.systemDefault转为时间戳："+parse1.toInstant(ZoneOffset.UTC));

        Date parse2 = Date.from(instant);
        System.out.println("打印当前时间戳转为的Date："+parse2);
        Instant instant1 = parse2.toInstant();
        System.out.println("打印Date转为当前时间戳的："+instant1);   //发现这次时间慢了8小时。


    }
}


今天为一年中的第337天
今天星期SATURDAY
10天后为：2022-12-13T23:23:07.258249900
1670109787258
1670109787258
1670080987258
1670080987263
格式化好后10天后为：2022-12-13 23:23:07
1999-01-11T00:00
true
咱已经活了7597天！
咱已经活了20年！9月19天！
咱已经活了20年！
咱已经活了7597天！
咱已经活了249月！
打印当前时间戳：2022-12-03T15:23:07.275294500Z
打印当前时间戳转为LocalDateTime、ZoneId.systemDefault：2022-12-03T23:23:07.275294500
打印LocalDateTime、ZoneId.systemDefault转为时间戳：2022-12-03T23:23:07.275294500Z
打印当前时间戳转为的Date：Sat Dec 03 23:23:07 CST 2022
打印Date转为当前时间戳的：2022-12-03T15:23:07.275Z

Process finished with exit code 0


```

**看完理解后、建议直接跳过下面、直接去 五.16**



#### 15.1Date

1、日期对象如何创建，如何获取时间毫秒值？
public  Date();
public long getTime();   //返回从1970年1月1日   00:00:00走到此刻的总的毫秒数
2、时间毫秒值怎么恢复成日期对象
public Date(long time);
public void setTime(long time);

```java
import java.util.Date;

public class Date_S {
    public static void main(String[] args) {
        Date date = new Date();
        System.out.println(date);      //Sat Dec 03 15:41:58 CST 2022
        System.out.println(date.getTime());  //1670053318137
        System.out.println(new Date(date.getTime() + 1415926535));  //Tue Dec 20 01:00:44 CST 2022
    }
}
```

#### 15.2SimpleDateFormat

1、SimpleDateFormat代表什么，有什么作用？
简单日期格式化对象
可以把日期对象及时间毫秒值格式化成我们想要的字符串形式。
可以把字符串的时间形式解析成Date日期对象。

2、SimpleDateFormat的对象如何创建？
public SimpleDateFormat(String pattern)

3、SimpleDateFormat格式化，以及解析时间的方法是怎么样的？
public final String format(Date d):格式化日期对象
public final String format(Object time):格式化时间毫秒值
public Date parse(String source)：解析字符串时间

```java
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class SimTime {
    public static void main(String[] args) throws ParseException {
        String mytime = "2022-12-01T23:46:00.000Z";
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss.SSS'Z'");
        Date date = simpleDateFormat.parse(mytime);
        System.out.println(date);  //Thu Dec 01 23:46:00 CST 2022

        Date date1 = new Date();
        String mytime2 = simpleDateFormat.format(date1);
        System.out.println(mytime2);  //2022-12-03T15:48:48.130Z

    }
}
```

#### 15.3LocalDateTime

| public static Xxxx now(); | 静态方法，根据当前时间创建对象  | LocaDate localDate = LocalDate.now();     LocalTime llocalTime = LocalTime.*now*();     LocalDateTime localDateTime = LocalDateTime.*now*(); |
| ------------------------- | ------------------------------- | ------------------------------------------------------------ |
| public static Xxxx of(…); | 静态方法，指定日期/时间创建对象 | LocalDate  localDate1 =  LocalDate.*of*(2099  ,  11,11);     LocalTime  localTime1 =  LocalTime.*of*(11, 11, 11);     LocalDateTime  localDateTime1 =  LocalDateTime.*of*(2020, 10, 6, 13, 23, 43); |

| 方法名                          | 说明               |
| ------------------------------- | ------------------ |
| public int geYear()             | 获取年             |
| public int getMonthValue()      | 获取月份（1-12）   |
| Public int getDayOfMonth()      | 获取月中第几天乘法 |
| Public int getDayOfYear()       | 获取年中第几天     |
| Public DayOfWeek getDayOfWeek() | 获取星期           |

| 方法名                         | 说明                    |
| ------------------------------ | ----------------------- |
| public LocalDate toLocalDate() | 转换成一个LocalDate对象 |
| public LocalTime toLocalTime() | 转换成一个LocalTime对象 |

| 方法名                                             | 说明                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| plusDays, plusWeeks, plusMonths, plusYears         | 向当前 LocalDate 对象添加几天、 几周、几个月、几年           |
| minusDays, minusWeeks, minusMonths, minusYears     | 从当前 LocalDate 对象减去几天、 几周、几个月、几年           |
| withDayOfMonth, withDayOfYear, withMonth, withYear | 将月份天数、年份天数、月份、年 份 修 改 为 指 定 的 值 并 返 回 新  的 LocalDate 对象 |
| isBefore, isAfter                                  | 比较两个 LocalDate                                           |

#### 15.4Duration/Period

```java
import java.time.Duration;
import java.time.LocalDateTime;
import java.time.Period;

public class LocalDateTime_S {
    public static void main(String[] args) {
        
        LocalDateTime now = LocalDateTime.now();
        LocalDateTime birthDate = LocalDateTime.of(2002, 2, 14, 0, 0, 0);
        System.out.println("今天为一年中的第"+now.getDayOfYear()+"天");
        System.out.println("今天星期"+now.getDayOfWeek());
        
        LocalDateTime plus10Days = now.plusDays(10L);
        System.out.println("10天后为："+plus10Days);
        
        System.out.println(birthDate.isBefore(now));
        
        Duration between = Duration.between(birthDate, now);
        System.out.println("咱已经活了"+between.toDays()+"天！");
        
        Period betweenPeriod = Period.between(birthDate.toLocalDate(), now.toLocalDate());
        System.out.println("咱已经活了"+betweenPeriod.getYears()+"年！"+betweenPeriod.getMonths()+"月"+betweenPeriod.getDays()+"天！");

    }
}
```

今天为一年中的第337天
今天星期SATURDAY
10天后为：2022-12-13T16:26:26.390312600
true
咱已经活了7597天！
咱已经活了20年！9月19天！

### 16.正则表达式

![Snipaste_2022-12-08_21-07-01](images\Snipaste_2022-12-08_21-07-01.png)

```java
public static void main(String[] args) {
    String str = "aaabcde";
    String str2 = "aaa";
    String str3 = "cde";
    String str4 = "17365971111";
    String str5 = "我爱你、爱死你、就像老鼠爱大米";
   
    //   *  匹配0次或多次
    //   ？ 表示0次或一次即：表示是可选的、可有可无
    System.out.println(str.matches("a*"));   //false
    System.out.println(str2.matches("a*"));  //true
    System.out.println(str3.matches("a*cde")); //true
    System.out.println(str3.matches("(ab)?cde")); //true

    System.out.println(str4.matches("1\\d{10}")); //true

    System.out.println(str5.replaceAll("爱+", "喜欢")); //我喜欢你、喜欢死你、就像老鼠喜欢大米
    String[] splits = str5.split("爱");
    System.out.println(Arrays.toString(splits)); //[我, 你、, 死你、就像老鼠, 大米]
}
```



| 方法名                                               | 说明                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| public String replaceAll(String regex,String newStr) | 按照正则表达式匹配的内容进行替换                             |
| public String[] split(String regex)：                | 按照正则表达式匹配的内容进行分割字符串，反回一个字符串数组。 |

### 17.可变参数

可变参数用在形参中可以接收多个数据。
可变参数的格式：数据类型...参数名称

接收参数非常灵活，方便。可以不接收参数，可以接收1个或者多个参数，也可以接收一个数组

**可变参数在方法内部本质上就是一个数组。**

1.一个形参列表中可变参数只能有一个

2.可变参数必须放在形参列表的最后面

```java
 public static void main(String[] args) {
         System.out.println(addAll(1, 2, 3));
     
         Integer[] integers = {1,2,3};
         System.out.println(addAll(integers));
 }
static Integer addAll(Integer ...a){
     int sum = 0;
     for (Integer i : a) {
         sum=sum+i;
     }
    System.out.println(a[0]);
    System.out.println(a[1]);
    System.out.println(a[2]);
   
    return sum;
 }
```



## 六.集合

![Collection](images\Collection.png)

| 方法名称                             | 说明                             |
| ------------------------------------ | -------------------------------- |
| public  boolean add(E e)             | 把给定的对象添加到当前集合中     |
| public  void clear()                 | 清空集合中所有的元素             |
| public  boolean remove(E e)          | 把给定的对象在当前集合中删除     |
| public  boolean contains(Object obj) | 判断当前集合中是否包含给定的对象 |
| public  boolean isEmpty()            | 判断当前集合是否为空             |
| public  int size()                   | 返回集合中元素的个数。           |
| public  Object[] toArray()           | 把集合中的元素，存储到数组中     |

Collection是单列集合的祖宗接口，它的功能是全部单列集合都可以继承使用的。

```java
    public static void main(String[] args) {
        Collection<Student> students = new ArrayList<>();
        Student student1 = new Student("佩奇", 6);
        Student student2 = new Student("佩奇2", 6);
        students.add(student1);
        System.out.println(students.contains(student2)); //false

        students.add(student2);
        System.out.println(students.contains(student1));//true

        System.out.println(students.size());//2

        Object[] objects = students.toArray();
        System.out.println(Arrays.toString(objects));
//[Student{嘿嘿！name='佩奇', age=6}, Student{嘿嘿！name='佩奇2', age=6}]
        students.remove(student1);
        System.out.println(students.size()); //1
    }
```

### 1.迭代器

| 方法名称                        | 说明                                                        |
| ------------------------------- | ----------------------------------------------------------- |
| **Iterator<E>**  **iterator()** | 返回集合中的迭代器对象，该迭代器对象默认指向当前集合的0索引 |

| 方法名称          | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| boolean hasNext() | 询问当前位置是否有元素存在，存在返回true ,不存在返回false    |
| E  next()         | 获取当前位置的元素，并同时将迭代器对象移向下一个位置，注意防止取出越界。 |

```java
    public static void main(String[] args) {
        Collection<Student> students = new ArrayList<>();
        Student student1 = new Student("佩奇", 6);
        Student student2 = new Student("佩奇2", 6);
        students.add(student1);
        System.out.println(students.contains(student2)); //false
        students.add(student2);
        System.out.println(students.contains(student1));//true

        System.out.println(students.size());//2

        Object[] objects = students.toArray();
        System.out.println(Arrays.toString(objects));
//[Student{嘿嘿！name='佩奇', age=6}, Student{嘿嘿！name='佩奇2', age=6}]
        
        Iterator<Student> iterator = students.iterator(); //返回集合中的迭代器对象，该迭代器对象默认指向当前集合的0索引
        //遍历使用增强for、迭代器用于一些其他情况、是所有单列集合都可以使用的hasNext()\next()
        while (iterator.hasNext()){
            Student next = iterator.next();  //此功能为返回当前位置元素、并同时将迭代器对象移向下一个位置，注意防止取出越界
            System.out.println(next);

        }
        //增强for
        for (Student next : students) {
            System.out.println(next);

        }

//[Student{嘿嘿！name='佩奇', age=6}, Student{嘿嘿！name='佩奇2', age=6}]
        students.remove(student1);
        System.out.println(students.size()); //1
    }
```

### 2.增强for

for(元素数据类型 变量名 : 数组或者Collection集合) {

​     //在此处使用变量即可，该变量就是元素

}

一般对于要遍历的集合数组.for就能快捷组构

### 3.forEach结合Lambda表达式（重要）

再看五14.6

```java
public static void main(String[] args) {
    Collection<Student> students = new ArrayList<>();
    Student student1 = new Student("佩奇", 6);
    Student student2 = new Student("佩奇2", 8);
    students.add(student1);
    students.add(student2);


    students.forEach(new Consumer<Student>() {
        @Override
        public void accept(Student student) {
            System.out.println(student);
        }
    });

    students.forEach(student -> System.out.println(student));

    students.forEach(System.out::println);
    
}
```

输出是一样的

### 4.数据结构和特点

- 队列：先进先出，后进后出。
- 栈：后进先出，先进后出。
- 数组：内存连续区域，查询快，增删慢。
- 链表：元素是游离的，查询慢，首尾操作极快。
- 二叉树：永远只有一个根节点, 每个结点不超过2个子节点的树。
- 查找二叉树：小的左边，大的右边，但是可能树很高，查询性能变差。
- 平衡查找二叉树：让树的高度差不大于1，增删改查都提高了。
- 红黑树（就是基于红黑规则实现了自平衡的排序二叉树）

![Snipaste_2022-12-11_22-57-35](images\Snipaste_2022-12-11_22-57-35.png)

二叉树：

![Snipaste_2022-12-11_23-01-12](images\Snipaste_2022-12-11_23-01-12.png)

### 5.List集合

有序、可重复、有索引

List集合因为支持索引，所以多了很多索引操作的独特api，其他Collection的功能List也都继承了。

**一般也就有索引的List集合才有关于索引的api、只有key-value形式的map集合才有键值的api**

| 方法名称                       | 说明                                   |
| ------------------------------ | -------------------------------------- |
| void add(int  index,E element) | 在此集合中的指定位置插入指定的元素     |
| E remove(int  index)           | 删除指定索引处的元素，返回被删除的元素 |
| E set(int index,E  element)    | 修改指定索引处的元素，返回被修改的元素 |
| E get(int  index)              | 返回指定索引处的元素                   |

ArrayList底层是基于数组实现的，根据查询元素快，增删相对慢。第一次创建集合并添加第一个元素的时候，在底层创建一个默认长度为10的数组。

**List的sort方法也很实用**

**包括Collections工具类中.sort()方法也只支持List集合、排序就用List集合**

LinkedList底层基于双链表实现的，查询元素慢，增删首尾元素是非常快的。以下为特有api、首尾操作较多

LinkedList也是有索引的、以上方法也是适用的

| 方法名称                   | 说明                             |
| -------------------------- | -------------------------------- |
| public  void addFirst(E e) | 在该列表开头插入指定的元素       |
| public  void addLast(E e)  | 将指定的元素追加到此列表的末尾   |
| public  E getFirst()       | 返回此列表中的第一个元素         |
| public  E getLast()        | 返回此列表中的最后一个元素       |
| public  E removeFirst()    | 从此列表中删除并返回第一个元素   |
| public  E removeLast()     | 从此列表中删除并返回最后一个元素 |

```java
public static void main(String[] args) {
    List<Student> students = new LinkedList<>();

    Student student1 = new Student("佩奇", 6);
    Student student2 = new Student("佩奇2", 5);
    students.add(student1);

    students.add(student2);
    students.sort((o1, o2) -> o1.getAge()- o2.getAge());
    System.out.println(students);

    students.sort(Comparator.comparingInt(Student::getAge).reversed());
    System.out.println(students);


    System.out.println(students.get(1));
}
```

### 6.Set集合

HashSet : 无序、不重复、无索引。
LinkedHashSet：有序、不重复、无索引。
TreeSet：排序、不重复、无索引。

Set集合的功能上基本上与Collection的API一致。

Set集合的底层原理是什么样的
JDK8之前的，哈希表：底层使用数组+链表组成
JDK8开始后，哈希表：底层采用数组+链表+红黑树组成。

![Snipaste_2022-12-12_11-37-30](images\Snipaste_2022-12-12_11-37-30.png)

![Snipaste_2022-12-12_11-37-47](images\Snipaste_2022-12-12_11-37-47.png)

![Snipaste_2022-12-12_11-38-04](images\Snipaste_2022-12-12_11-38-04.png)

![Snipaste_2022-12-12_11-40-13](images\Snipaste_2022-12-12_11-40-13.png)

![Snipaste_2022-12-12_11-41-46](images\Snipaste_2022-12-12_11-41-46.png)



**如果希望Set集合认为2个内容一样的对象是重复的，**
**必须重写对象的hashCode()和equals()方法**

```java
public static void main(String[] args) {
    HashSet<Student> students = new HashSet<>();
    Student student = new Student("佩奇", 6);
    Student student1 = new Student("佩奇", 6);
    Student student2 = new Student("佩奇2", 5);
    Collections.addAll(students,student,student1,student2);
    System.out.println(students.size()); //3
    System.out.println(students);
}
```

重写自定义Student对象的hashCode()和equals()方法后再看students.size()变为了2

仅重写任意其中之一方法无效、毕竟先调用hashcode方法比较返回的数值相同再调用equals方法来比较值是否相同

仅重写hashCode可能确实返回了相同的值、但再调用equals方法时、未重写则比较地址时不相同了

仅重写equals方法时、那么hashCode并没有返回相同的值、自然依旧不能去重复



相同的值hash值相同嘛、但不同的两个值未必保证hash值一定不同、所有才会再调用equals方法来比较吧。

LinkedHashSet集合的特点和原理是怎么样的？
有序、不重复、无索引
底层基于哈希表，使用双链表记录添加顺序。

TreeSet集合的特点是怎么样的？
可排序、不重复、无索引
底层基于红黑树实现排序，增删改查性能较好

TreeSet集合自定义排序规则有几种方式
2种。
类实现Comparable接口，重写比较规则。
集合自定义Comparator比较器对象，重写比较规则。



![Snipaste_2022-12-12_11-45-54](images\Snipaste_2022-12-12_11-45-54.png)

### 7.Collections工具类

包括Collections工具类中.sort()方法也只支持List集合、排序就用List集合

.shuffle()打乱List集合元素顺序

```
Collections.   //查看
```

### 8.Map集合

key=value(键值对元素)

双列集合、以上Collectioon接口下实现类均为单列

![Snipaste_2022-12-12_16-30-39](images\Snipaste_2022-12-12_16-30-39.png)

Map集合的特点都是由键决定的。
Map集合的键是无序,不重复的，无索引的，值不做要求（可以重复）。
Map集合后面重复的键对应的值会覆盖前面重复键的值。

HashMap:元素按照键是无序，不重复，无索引，值不做要求。（与Map体系一致）
LinkedHashMap:元素按照键是有序，不重复，无索引，值不做要求。
TreeMap：元素按照建是排序，不重复，无索引的，值不做要求。

Map祖宗接口、其实现类均可继承使用其api

| 方法名称                            | 说明                                 |
| ----------------------------------- | ------------------------------------ |
| V  put(K key,V value)               | 添加元素                             |
| V  remove(Object key)               | 根据键删除键值对元素                 |
| void  clear()                       | 移除所有的键值对元素                 |
| boolean containsKey(Object key)     | 判断集合是否包含指定的键             |
| boolean containsValue(Object value) | 判断集合是否包含指定的值             |
| boolean isEmpty()                   | 判断集合是否为空                     |
| int  size()                         | 集合的长度，也就是集合中键值对的个数 |

#### 8.1获取全部键的set集合

| 方法名称         | 说明             |
| ---------------- | ---------------- |
| Set<K>  keySet() | 获取所有键的集合 |

| V  get(Object key) | 根据键获取值 |
| ------------------ | ------------ |

#### 8.2获取全部键值对

| 方法名称                       | 说明                     |
| ------------------------------ | ------------------------ |
| Set<Map.Entry<K,V>> entrySet() | 获取所有键值对对象的集合 |

| K getKey()   | 获得键 |
| ------------ | ------ |
| V getValue() | 获取值 |

#### 8.3Lambda遍历map

```java
maps.forEach((k , v) -> {
    System.out.println(k +"----->" + v);
});
```

#### 8.4HashMap

HashMap是Map里面的一个实现类。特点都是由键决定的：无序、不重复、无索引
没有额外需要学习的特有方法，直接使用Map里面的方法就可以了。
HashMap跟HashSet底层原理是一模一样的，都是哈希表结构，只是HashMap的每个元素包含两个值而已。

依赖hashCode方法和equals方法保证键的唯一。
如果键要存储的是自定义对象，需要重写hashCode和equals方法。
基于哈希表。增删改查的性能都较好。

实际上：Set系列集合的底层就是Map实现的，只是Set集合中的元素只要键数据，不要值数据而已

```java
public HashSet() {
    map = new HashMap<>();
}
```

#### 8.4LinkedHashMap

由键决定：有序、不重复、无索引。
这里的有序指的是保证存储和取出的元素顺序一致
原理：底层数据结构是依然哈希表，只是每个键值对元素又额外的多了一个双链表的机制记录存储的顺序。

#### 8.5TreeMap

由键决定特性：不重复、无索引、可排序
可排序：按照键数据的大小默认升序（有小到大）排序。只能对键排序。
注意：TreeMap集合是一定要排序的，可以默认排序，也可以将键按照指定的规则进行排序
TreeMap跟TreeSet一样底层原理是一样的。

TreeMap集合自定义排序规则有2种
类实现Comparable接口，重写比较规则。
集合自定义Comparator比较器对象，重写比较规则。

```java
public static void main(String[] args) {
    HashMap<Student, Integer> studentIntegerHashMap = new HashMap<>();
    Student student = new Student("佩奇", 6);
    Student student1 = new Student("佩奇", 6);
    Student student2 = new Student("乔治", 5);
    studentIntegerHashMap.put(student,1);
    studentIntegerHashMap.put(student1,2);
    studentIntegerHashMap.put(student2,3);
//    System.out.println(studentIntegerHashMap.get(student));
    System.out.println(studentIntegerHashMap);
    Set<Student> students = studentIntegerHashMap.keySet();
    System.out.println(students);
    Set<Map.Entry<Student, Integer>> entries = studentIntegerHashMap.entrySet();
    System.out.println(entries);
    studentIntegerHashMap.forEach((k,v)->{
        System.out.println(k + "" + v);
    });

}
```

### 9.不可变集合of

在List、Set、Map接口中，都存在of方法，可以创建一个不可变的集合。

这个集合不能添加，不能删除，不能修改。

| 方法名称                                  | 说明                               |
| ----------------------------------------- | ---------------------------------- |
| static  <E> List<E> of(E…elements)        | 创建一个具有指定元素的List集合对象 |
| static  <E> Set<E> of(E…elements)         | 创建一个具有指定元素的Set集合对象  |
| static <K  , V>  Map<K，V> of(E…elements) | 创建一个具有指定元素的Map集合对象  |

```java
public static void main(String[] args) {
    List<? extends Serializable> a = List.of("1", 2, 'a');
    Set<? extends Serializable> set = Set.of("1", 1);
    Map<String, Integer> k2 = Map.of("1", 1, "k2", 2);
    System.out.println(a);   //[1, 2, a]
    System.out.println(set);  //[1, 1]
    System.out.println(k2);  //{k2=2, 1=1}
}
```



### 10.stream流（重要）

```java
public static void main(String[] args) {
    List<Student> students = new LinkedList<>();

    Student student1 = new Student("佩奇", 6);
    Student student2 = new Student("佩奇2", 5);
    students.add(student1);
    students.add(student2);

    List<Student> collect = students.stream().sorted(Comparator.comparingInt(Student::getAge)).collect(Collectors.toList());
    System.out.println(collect);
}
```

[Stream流的常用方法 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/339038230)

[Stream流常用方法_TayGo的博客-CSDN博客_stream流常用方法](https://blog.csdn.net/m0_46434219/article/details/109049369)

```java
    public static void main(String[] args) {
        List<Student> students = new LinkedList<>();

        Student student = new Student("乔治", 5);
        Student student1 = new Student("佩奇", 6);
        Student student2 = new Student("佩奇2", 4);
        Student student3 = new Student("佩奇2", 4);
        Student student4 = new Student("佩奇3", 7);

        students.add(student);
        students.add(student1);
        students.add(student2);
        students.add(student3);
        students.add(student4);

        System.out.println(students.stream().map(Student::getAge).reduce(0, (o1, o2) -> o1 + o2));  //全部学生岁数之和//26
        System.out.println(students.stream().map(Student::getAge).reduce(0, Integer::sum));  //全部学生岁数之和//26
        students.stream().peek(s->s.setAge(s.getAge()+1)).forEach(System.out::print);  
        //Student{name='乔治', age=6}Student{name='佩奇', age=7}Student{name='佩奇2', age=5}Student{name='佩奇2', age=5}Student{name='佩奇3', age=8}
        System.out.print("\n");
        List<Integer> second = students.stream().map(Student::getAge).distinct().sorted(Comparator.reverseOrder()).skip(1).limit(1).collect(Collectors.toList()); 
        System.out.println(second); //取年龄为一集合、去重、倒序、跳过一个数、取一个数收集到新集合中
        //[7]
        students = students.stream().distinct().filter(s->s.getAge()<6).sorted(Comparator.comparingInt(Student::getAge)).collect(Collectors.toList());

        System.out.println(students); //[Student{name='佩奇2', age=5}]
    }
```

## 七.IO

### 1.File类***

| 方法名称                                      | 说明                                               |
| --------------------------------------------- | -------------------------------------------------- |
| **public**  File(String pathname)             | 根据文件路径创建文件对象                           |
| **public** File(String  parent, String child) | 根据父路径名字符串和子路径名字符串创建文件对象     |
| **public** File(File parent, String child)    | 根据父路径对应文件对象和子路径名字符串创建文件对象 |

File对象可以定位文件和文件夹
File封装的对象仅仅是一个路径名，这个路径可以是存在的，也可以是不存在的。

![Snipaste_2022-12-15_16-30-56](images\Snipaste_2022-12-15_16-30-56.png)

| 方法名称                         | 说明                                 |
| -------------------------------- | ------------------------------------ |
| public  boolean isDirectory()    | 判断此路径名表示的File是否为文件夹   |
| public  boolean isFile()         | 判断此路径名表示的File是否为文件     |
| public  boolean  exists()        | 判断此路径名表示的File是否存在       |
| public long  length()            | 返回文件的大小（字节数量）           |
| public  String getAbsolutePath() | 返回文件的绝对路径                   |
| public  String getPath()         | 返回定义文件时使用的路径             |
| public  String getName()         | 返回文件的名称，带后缀               |
| public  long lastModified()      | 返回文件的最后修改时间（时间毫秒值） |

| 方法名称                       | 说明                 |
| ------------------------------ | -------------------- |
| public boolean createNewFile() | 创建一个新的空的文件 |
| public boolean mkdir()         | 只能创建一级文件夹   |
| public boolean mkdirs()        | 可以创建多级文件夹   |

| 方法名称                 | 说明                                   |
| ------------------------ | -------------------------------------- |
| public  boolean delete() | 删除由此抽象路径名表示的文件或空文件夹 |

delete方法默认只能删除文件和空文件夹，delete方法直接删除不走回收站

| 方法名称                        | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| public String[] list()          | 获取当前目录下所有的"一级文件名称"到一个字符串数组中去返回。 |
| public File[] listFiles()(常用) | 获取当前目录下所有的"一级文件对象"到一个文件对象数组中去返回（重点） |

listFiles方法注意事项：

当文件不存在时或者代表文件时，返回null
当文件对象代表一个空文件夹时，返回一个长度为0的数组
当文件对象是一个有内容的文件夹时，将里面所有文件和文件夹的路径放在File数组中返回
当文件对象是一个有隐藏文件的文件夹时，将里面所有文件和文件夹的路径放在File数组中返回，包含隐藏文件
当没有权限访问该文件夹时，返回null

遍历所有文件名：

```java
import java.io.File;

public class MyFile {
    public static void main(String[] args) {
        File file = new File("C:\\workspace2\\zzz");
        met(file);
    }

    static void met(File file){
        if (file.isFile()){
            System.out.println(file.getName());
        }
        if(file.isDirectory()){
            File[] files = file.listFiles();
            if (files.length==0){
                return;
            }
            for (File file1 : files) {
                if(file1.isDirectory()){
                    met(file1);
                }
                if (file1.isFile()){
                    System.out.println(file1.getName());
                }
            }
        }
    }
}
```



递归删除文件夹

```java
import java.io.File;

public class MyFile {
    public static void main(String[] args) {
        File file = new File("C:\\workspace2\\zzz");
        met(file);
    }

    static void met(File file){
        if (file.isFile()){
            System.out.println(file.getName());
            file.delete();
        }
        if(file.isDirectory()){
            File[] files = file.listFiles();
            if (files.length==0){
                file.delete();
                return;
            }
            for (File file1 : files) {
                if(file1.isDirectory()){
                    met(file1);
                }
                if (file1.isFile()){
                    System.out.println(file1.getName());
                    file1.delete();
                }
            }
            file.delete();
        }
    }
}
```

![Snipaste_2022-12-16_18-03-12](images\Snipaste_2022-12-16_18-03-12.png)

### 2.文件字节输入流FileInputStream***

**作用：以内存为基准，把磁盘文件中的数据以字节的形式读取到内存中去。**

| 构造器                                   | 说明                               |
| ---------------------------------------- | ---------------------------------- |
| public  FileInputStream(File file)       | 创建字节输入流管道与源文件对象接通 |
| public  FileInputStream(String pathname) | 创建字节输入流管道与源文件路径接通 |

| 方法名称                        | 说明                                                   |
| ------------------------------- | ------------------------------------------------------ |
| public int  read()              | 每次读取一个字节返回，如果字节已经没有可读的返回-1     |
| public int  read(byte[] buffer) | 每次读取一个字节数组返回，如果字节已经没有可读的返回-1 |

| 方法名称                                        | 说明                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| public byte[] readAllBytes() throws IOException | 直接将当前字节输入流对应的文件对象的字节数据装到一个字节数组返回 |

### 3.文件字节输出流FileOutputStream***

**作用：以内存为基准，把内存中的数据以字节的形式写出到磁盘文件中去的流。**

| 构造器                                                   | 说明                                           |
| -------------------------------------------------------- | ---------------------------------------------- |
| public FileOutputStream(File file)                       | 创建字节输出流管道与源文件对象接通             |
| public FileOutputStream(File file，boolean append)       | 创建字节输出流管道与源文件对象接通，可追加数据 |
| public FileOutputStream(String filepath)                 | 创建字节输出流管道与源文件路径接通             |
| public FileOutputStream(String filepath，boolean append) | 创建字节输出流管道与源文件路径接通，可追加数据 |

| 方法名称                                             | 说明                         |
| ---------------------------------------------------- | ---------------------------- |
| public void write(int a)                             | 写一个字节出去               |
| public void write(byte[] buffer)                     | 写一个字节数组出去           |
| public void write(byte[] buffer , int pos , int len) | 写一个字节数组的一部分出去。 |

### 4.流的关闭和刷新***

| 方法    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| flush() | 刷新流，还可以继续写数据                                     |
| close() | 关闭流，释放资源，但是在关闭之前会先刷新流。一旦关闭，就不能再写数据 |

字节输出流如何实现写出去的数据能换行
os.write(“\r\n”.getBytes())

如何让写出去的数据能成功生效？
flush()刷新数据
close()方法是关闭流，关闭包含刷新，关闭后流不可以继续使用了。

手动释放

```java
public class MyFileInputStream {
    public static void main(String[] args) throws IOException {
        FileInputStream fileInputStream = new FileInputStream("C:\\code\\aaa\\a.jpg");
        FileOutputStream fileOutputStream = new FileOutputStream("C:\\code\\b.jpg");
        byte[] bytes = fileInputStream.readAllBytes();
        fileOutputStream.write(bytes);
        fileInputStream.close();
        fileOutputStream.close();
    }
}
```

### 5.资源释放***

![Snipaste_2022-12-16_18-29-53](images\Snipaste_2022-12-16_18-29-53.png)

相当于复制再加重命名

```java
public class MyFileInputStream {
    public static void main(String[] args) throws IOException {
        FileInputStream fileInputStream = new FileInputStream("C:\\code\\aaa\\a.jpg");
        FileOutputStream fileOutputStream = new FileOutputStream("C:\\code\\b.jpg");
        try(fileInputStream;fileOutputStream){
            byte[] bytes = fileInputStream.readAllBytes();
            fileOutputStream.write(bytes);
        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            System.out.println("完成！");
        }
    }
}
```

### 6.文件字符输入流FileReader

**作用：以内存为基准，把磁盘文件中的数据以字符的形式读取到内存中去。**

| 构造器                              | 说明                               |
| ----------------------------------- | ---------------------------------- |
| public FileReader(File file)        | 创建字符输入流管道与源文件对象接通 |
| public FileReader(String  pathname) | 创建字符输入流管道与源文件路径接通 |

| 方法名称                        | 说明                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| public int read()               | 每次读取一个字符返回，如果字符已经没有可读的返回-1           |
| public int  read(char[] buffer) | 每次读取一个字符数组，返回读取的字符个数，如果字符已经没有可读的返回-1 |

### 7.文件字符输出流FileWriter

| 构造器                                             | 说明                                           |
| -------------------------------------------------- | ---------------------------------------------- |
| public FileWriter(File file)                       | 创建字符输出流管道与源文件对象接通             |
| public FileWriter(File file，boolean append)       | 创建字符输出流管道与源文件对象接通，可追加数据 |
| public FileWriter(String filepath)                 | 创建字符输出流管道与源文件路径接通             |
| public FileWriter(String filepath，boolean append) | 创建字符输出流管道与源文件路径接通，可追加数据 |

| 方法名称                                   | 说明                 |
| ------------------------------------------ | -------------------- |
| void  write(int c)                         | 写一个字符           |
| void  write(char[] cbuf)                   | 写入一个字符数组     |
| void  write(char[] cbuf, int off, int len) | 写入字符数组的一部分 |
| void  write(String str)                    | 写一个字符串         |
| void  write(String str, int off, int len)  | 写一个字符串的一部分 |

| 方法    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| flush() | 刷新流，还可以继续写数据                                     |
| close() | 关闭流，释放资源，但是在关闭之前会先刷新流。一旦关闭，就不能再写数据 |

### 8.字节缓冲流***

**作用：缓冲流自带缓冲区、可以提高原始字节流、字符流读写数据的性能**

**缓冲流也称为高效流、或者高级流。之前学习的字节流可以称为原始流。**

字节缓冲输入流自带了8KB缓冲池，以后我们直接从缓冲池读取数据，所以性能较好。
字节缓冲输出流自带了8KB缓冲池，数据就直接写入到缓冲池中去，写数据性能极高了。

字节缓冲输入流：BufferedInputStream，提高字节输入流读取数据的性能。
 字节缓冲输出流：BufferedOutputStream，提高字节输出流读取数据的性能。

| 构造器                                       | 说明                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| public BufferedInputStream(InputStream is)   | 可以把低级的字节输入流包装成一个高级的缓冲字节输入流管道，从而提高字节输入流读数据的性能 |
| public BufferedOutputStream(OutputStream os) | 可以把低级的字节输出流包装成一个高级的缓冲字节输出流，从而提高写数据的性能 |

```java
public class MyFileInputStream {
    public static void main(String[] args) throws IOException {
        FileInputStream fileInputStream = new FileInputStream("C:\\code\\aaa\\a.jpg");
        BufferedInputStream bufferedInputStream = new BufferedInputStream(fileInputStream);
        FileOutputStream fileOutputStream = new FileOutputStream("C:\\code\\b.jpg");
        BufferedOutputStream bufferedOutputStream = new BufferedOutputStream(fileOutputStream);

        byte[] bytes = bufferedInputStream.readAllBytes();
        bufferedOutputStream.write(bytes);

        bufferedInputStream.close();
        fileInputStream.close();
        bufferedOutputStream.close();
        fileOutputStream.close();
    }
}
```

### 9.字符缓冲流

字符缓冲输入流：BufferedReader。
作用：提高字符输入流读取数据的性能，除此之外多了按照行读取数据的功能。

| 构造器                           | 说明                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| public  BufferedReader(Reader r) | 可以把低级的字符输入流包装成一个高级的缓冲字符输入流管道，从而提高字符输入流读数据的性能 |

字符缓冲输入流新增功能

| 方法                      | 说明                                                 |
| ------------------------- | ---------------------------------------------------- |
| public  String readLine() | 读取一行数据返回，如果读取没有完毕，无行可读返回null |



字符缓冲输出流：BufferedWriter。
 作用：提高字符输出流写取数据的性能，除此之外多了换行功能

| 构造器                           | 说明                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| public BufferedWriter(Writer  w) | 可以把低级的字符输出流包装成一个高级的缓冲字符输出流管道，从而提高字符输出流写数据的性能 |

字符缓冲输出流新增功能

| 方法                   | 说明     |
| ---------------------- | -------- |
| public  void newLine() | 换行操作 |



### 10.转换流

字符输入转换流：InputStreamReader，可以把原始的字节流按照指定编码转换成字符输入流。

| 构造器                                                    | 说明                                                         |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| public InputStreamReader(InputStream is)                  | 可以把原始的字节流按照代码默认编码转换成字符输入流。几乎不用，与默认的FileReader一样。 |
| public InputStreamReader(InputStream is ，String charset) | 可以把原始的字节流按照指定编码转换成字符输入流，这样字符流中的字符就不乱码了(重点) |

字符输入转换流：OutputStreamWriter，可以把字节输出流按照指定编码转换成字符输出流。

| 构造器                                                      | 说明                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| public OutputStreamWriter(OutputStream os)                  | 可以把原始的字节输出流按照代码默认编码转换成字符输出流。几乎不用。 |
| public OutputStreamWriter(OutputStream os，String  charset) | 可以把原始的字节输出流按照指定编码转换成字符输出流(重点)     |

### 11.对象序列化***

对象序列化：
作用：以内存为基准，把内存中的对象存储到磁盘文件中去，称为对象序列化。
使用到的流是对象字节输出流：ObjectOutputStream

| 构造器                                       | 说明                                       |
| -------------------------------------------- | ------------------------------------------ |
| public ObjectOutputStream(OutputStream  out) | 把低级字节输出流包装成高级的对象字节输出流 |

| 方法名称                                  | 说明                                 |
| ----------------------------------------- | ------------------------------------ |
| public final void writeObject(Object obj) | 把对象写出去到对象序列化流的文件中去 |

**对象序列化的含义是什么？**
**把对象数据存入到文件中去。**

对象序列化用到了哪个流？
对象字节输出流ObjectOutputStram
public void writeObject(Object obj)

序列化对象的要求是怎么样的？
对象必须实现序列化接口



对象反序列化：
使用到的流是对象字节输入流：ObjectInputStream
作用：以内存为基准，把存储到磁盘文件中去的对象数据恢复成内存中的对象，称为对象反序列化。

| 构造器                                     | 说明                                       |
| ------------------------------------------ | ------------------------------------------ |
| public ObjectInputStream(InputStream  out) | 把低级字节输如流包装成高级的对象字节输入流 |

| 方法名称                    | 说明                                                 |
| --------------------------- | ---------------------------------------------------- |
| public  Object readObject() | 把存储到磁盘文件中去的对象数据恢复成内存中的对象返回 |

**对象反序列化的含义是什么？**
**把磁盘中的对象数据恢复到内存的Java对象中。**

对象反序列化用到了哪个流？
对象字节输入流ObjectInputStram
public Object readObject()

首先对象Student实现 implements Serializable接口

```java
public class MySerializable {
    public static void main(String[] args) throws IOException, ClassNotFoundException {
        FileOutputStream fileOutputStream = new FileOutputStream("C:\\code\\myser.txt");
        FileInputStream fileInputStream = new FileInputStream("C:\\code\\myser.txt");

        Student student = new Student("佩奇", 6);

        ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream);
        objectOutputStream.writeObject(student);

        ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream);
        Student student1 = (Student) objectInputStream.readObject();

        System.out.println(student1);
        //Student{name='佩奇', age=6}

        fileInputStream.close();
        objectInputStream.close();
        fileOutputStream.close();
        objectOutputStream.close();

    }
}
```

### 12.打印流

作用：打印流可以实现方便、高效的打印数据到文件中去。打印流一般是指：PrintStream，PrintWriter两个类。
可以实现打印什么数据就是什么数据，例如打印整数97写出去就是97，打印boolean的true，写出去就是true。

PrintStream

| 构造器                              | 说明                         |
| ----------------------------------- | ---------------------------- |
| public PrintStream(OutputStream os) | 打印流直接通向字节输出流管道 |
| public PrintStream(File f)          | 打印流直接通向文件对象       |
| public PrintStream(String filepath) | 打印流直接通向文件路径       |

| 方法                       | 说明                   |
| -------------------------- | ---------------------- |
| public void print(Xxx  xx) | 打印任意类型的数据出去 |





PrintWriter

| 构造器                               | 说明                         |
| ------------------------------------ | ---------------------------- |
| public PrintWriter(OutputStream os)  | 打印流直接通向字节输出流管道 |
| public PrintWriter (Writer w)        | 打印流直接通向字符输出流管道 |
| public PrintWriter (File f)          | 打印流直接通向文件对象       |
| public PrintWriter (String filepath) | 打印流直接通向文件路径       |

| 方法                       | 说明                   |
| -------------------------- | ---------------------- |
| public void print(Xxx  xx) | 打印任意类型的数据出去 |



PrintStream和PrintWriter的区别
打印数据功能上是一模一样的，都是使用方便，性能高效（核心优势）
PrintStream继承自字节输出流OutputStream，支持写字节数据的方法。
PrintWriter继承自字符输出流Writer，支持写字符数据出去。



PrintStream ps = new PrintStream("文件地址")
 System.*setOut*(ps);

### 13.IO工具类

引入commons-io-x.x.jar

lcommons-io是apache开源基金组织提供的一组有关IO操作的类库，可以提高IO功能开发的效率。

lcommons-io工具包提供了很多有关io操作的类。有两个主要的类FileUtils, IOUtils

**FileUtils主要有如下方法:**

| 方法名                                                      | 说明                         |
| ----------------------------------------------------------- | ---------------------------- |
| String  readFileToString(File  file, String encoding)       | 读取文件中的数据, 返回字符串 |
| void  copyFile(File  srcFile, File destFile)                | 复制文件。                   |
| void  copyDirectoryToDirectory(File  srcDir,  File destDir) | 复制文件夹。                 |

### 14.Properties

其实就是一个Map集合，但是我们一般不会当集合使用，因为HashMap更好用。

![Snipaste_2022-12-16_23-08-06](images\Snipaste_2022-12-16_23-08-06.png)

Properties代表的是一个属性文件，可以把自己对象中的键值对信息存入到一个属性文件中去。
属性文件：后缀是.properties结尾的文件,里面的内容都是 key=value，后续做系统配置信息的。

| 构造器                                               | 说明                                                         |
| ---------------------------------------------------- | ------------------------------------------------------------ |
| void load(InputStream inStream)                      | 从输入字节流读取属性列表（键和元素对）                       |
| void  load(Reader reader)                            | 从输入字符流读取属性列表（键和元素对）                       |
| void  store(OutputStream out, String comments)       | 将此属性列表（键和元素对）写入此  Properties表中，以适合于使用 load(InputStream)方法的格式写入输出字节流 |
| void  store(Writer writer, String comments)          | 将此属性列表（键和元素对）写入此  Properties表中，以适合使用 load(Reader)方法的格式写入输出字符流 |
| public Object setProperty(String  key, String value) | 保存键值对（put）                                            |
| public String getProperty(String  key)               | 使用此属性列表中指定的键搜索属性值  (get)                    |
| public Set<String> stringPropertyNames()             | 所有键的名称的集合 (keySet())                                |

Properties的作用？
可以存储Properties属性集的键值对数据到属性文件中去：
void store(Writer writer, String comments)
可以加载属性文件中的数据到Properties对象中来：
void load(Reader reader)

## 八.Thread线程

### 1.多线程的创建

1.自定义类继承Thread、重写run方法、在别处创建自定义的类、调用其start()方法

优点：编码简单
缺点：线程类已经继承Thread，无法继承其他类，不利于扩展。

```java
public class MyThread extends Thread{
    @Override
    public void run() {
        System.out.println("111");
    }
}

 class MyTest1 {
    public static void main(String[] args) {
        MyThread myThread = new MyThread();
        myThread.start();   //直接调用run方法会当成普通方法执行，此时相当于还是单线程执行。
        for (int i = 0; i < 100; i++) {
            System.out.print("-");
        }
//        ------------------------------------------------------------------111
//        ----------------------------------
    }
}
```

2.自定义类实现Runnable接口、重写run()方法、在别处创建自定义类对象、将其对象交给Thread处理、最后调用start()方法

优点：线程任务类只是实现接口，可以继续继承类和实现接口，扩展性强。
缺点：编程多一层对象包装，如果线程有执行结果是不可以直接返回的。

| 构造器                                        | 说明                                         |
| --------------------------------------------- | -------------------------------------------- |
| public Thread(String name)                    | 可以为当前线程指定名称                       |
| public Thread(Runnable target)                | 封装Runnable对象成为线程对象                 |
| public Thread(Runnable target ，String name ) | 封装Runnable对象成为线程对象，并指定线程名称 |

```java
public class MyRunnable implements Runnable{
    @Override
    public void run() {
        System.out.println("222");
    }
}


class MyTest2 {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread 我的线程 = new Thread(myRunnable, "我的线程");
        我的线程.start();
        for (int i = 0; i < 100; i++) {
            System.out.print("-");
        }
        //        -------------222
        //        ---------------------------------------------------------------------------------------
    }
}
```

2.2使用匿名内部类、lamda表达式

```java
class MyTest22 {
    public static void main(String[] args) {
        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("222");
            }
        }, "t1");
        Thread t2 = new Thread(() -> System.out.println("333"), "t2");

        t1.start();
        t2.start();

        for (int i = 0; i < 100; i++) {
            System.out.print("-");
        }
//----------------------------------------------------------------333
//222
//------------------------------------
    }
}
```

3.利用Callable、FutureTask接口实现。

、得到任务对象
定义类实现Callable接口，重写call方法，封装要做的事情。
用FutureTask把Callable对象封装成线程任务对象。
、把线程任务对象交给Thread处理。
、调用Thread的start方法启动线程，执行任务
、线程执行完毕后、通过FutureTask的get方法去获取任务执行的结果。

| 方法名称                           | 说明                                 |
| ---------------------------------- | ------------------------------------ |
| public FutureTask<>(Callable call) | 把Callable对象封装成FutureTask对象。 |
| public V get() throws Exception    | 获取线程执行call方法返回的结果。     |

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.FutureTask;

public class MyCallableFutureTask implements Callable {

    @Override
    public Object call() throws Exception {
        System.out.println("321");
        return "123";
    }
}


class MyTest3 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        MyCallableFutureTask myCallableFutureTask= new MyCallableFutureTask();
        FutureTask futureTask = new FutureTask<>(myCallableFutureTask);
        Thread myTask = new Thread(futureTask, "myTask");
        myTask.start();


        for (int i = 0; i < 100; i++) {
            System.out.print("-");
        }
        Object o = futureTask.get();
        System.out.println(o);
        //----------------------------------------------------------------321
        //------------------------------------123
    }
}
```

使用匿名内部类

```java
class MyTest3 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
   //     MyCallableFutureTask myCallableFutureTask= new MyCallableFutureTask();
        FutureTask<String> futureTask = new FutureTask<String>(()->{
            System.out.println("321");
            return "123";
        });
        Thread myTask = new Thread(futureTask, "myTask");
        myTask.start();


        for (int i = 0; i < 100; i++) {
            System.out.print("-");
        }
        String str = futureTask.get();
        System.out.println(str);
        //----------------------------------------------------------------321
        //------------------------------------123
    }
}
```

### 2.Thread类常用方法

| 方法名称                                | 说明                                          |
| --------------------------------------- | --------------------------------------------- |
| String  getName()                       | 获取当前线程的名称，默认线程名称是Thread-索引 |
| void  setName(String  name)             | 设置线程名称                                  |
| public  static Thread currentThread()： | 返回对当前正在执行的线程对象的引用            |
| public  static void sleep(long time)    | 让线程休眠指定的时间，单位为毫秒。            |
| public  void run()                      | 线程任务方法                                  |
| public  void start()                    | 线程启动方法                                  |

构造器

| 构造器                                         | 说明                                       |
| ---------------------------------------------- | ------------------------------------------ |
| public  Thread(String name)                    | 可以为当前线程指定名称                     |
| public  Thread(Runnable target)                | 把Runnable对象交给线程对象                 |
| public  Thread(Runnable target ，String name ) | 把Runnable对象交给线程对象，并指定线程名称 |

### 3.线程的6种状态



| 线程状态                | 描述                                                         |
| ----------------------- | ------------------------------------------------------------ |
| NEW(新建)               | 线程刚被创建，但是并未启动。                                 |
| Runnable(可运行)        | 线程已经调用了start()等待CPU调度                             |
| Blocked(锁阻塞)         | 线程在执行的时候未竞争到锁对象，则该线程进入Blocked状态；。  |
| Waiting(无限等待)       | 一个线程进入Waiting状态，另一个线程调用notify或者notifyAll方法才能够唤醒 |
| Timed Waiting(计时等待) | 同waiting状态，有几个方法有超时参数，调用他们将进入Timed Waiting状态。带有超时参数的常用方法有Thread.sleep 、Object.wait。 |
| Teminated(被终止)       | 因为run方法正常退出而死亡，或者因为没有捕获的异常终止了run方法而死亡。 |

![Snipaste_2023-01-01_16-54-26](images\Snipaste_2023-01-01_16-55-21.png)

## 九.Junit常用注解

![Snipaste_2023-01-05_15-03-37](images\Snipaste_2023-01-05_15-03-37.png)

![Snipaste_2023-01-05_15-04-17](images\Snipaste_2023-01-05_15-04-17.png)

![Snipaste_2023-01-05_15-05-22](images\Snipaste_2023-01-05_15-05-22.png)

## 十.反射

### 1.反射概述

![Snipaste_2023-01-05_15-06-05](images\Snipaste_2023-01-05_15-06-05.png)

### 2.获取构造器并使用

![Snipaste_2023-01-05_16-59-08](images\Snipaste_2023-01-05_16-59-08.png)

![Snipaste_2023-01-05_17-00-12](images\Snipaste_2023-01-05_17-00-12.png)

```java
public class MyGetClass {
    public static void main(String[] args) throws ClassNotFoundException, InvocationTargetException, InstantiationException, IllegalAccessException, NoSuchMethodException {
        Class<?> studentClass1 = Class.forName("Student");
        Constructor<?> constructor = studentClass1.getDeclaredConstructor(String.class,Integer.class);
        Student student = (Student) constructor.newInstance("佩奇", 6);
        System.out.println(student);

        Class<Student> studentClass2 = Student.class;
        Constructor<Student> studentClass2DeclaredConstructor = studentClass2.getDeclaredConstructor(String.class);
        studentClass2DeclaredConstructor.setAccessible(true);      //此构造方法为私有
        Student student1 = studentClass2DeclaredConstructor.newInstance("乔治");
        System.out.println(student1);

        Student student2 = new Student("佩奇", 5);
        Class<? extends Student> studentClass3 = student2.getClass();


        System.out.println(studentClass1);
        System.out.println(studentClass2);
        System.out.println(studentClass3);
        //都相同啊、同一个类
    }
}
```

### 3.成员变量的获取使用

![Snipaste_2023-01-05_17-09-22](images\Snipaste_2023-01-05_17-09-22.png)

```java
public class MyGetClassField {
    public static void main(String[] args) throws ClassNotFoundException, InvocationTargetException, InstantiationException, IllegalAccessException, NoSuchMethodException, NoSuchFieldException {


        Class<Student> studentClass2 = Student.class;
        Constructor<Student> studentClass2DeclaredConstructor = studentClass2.getDeclaredConstructor(String.class);
        studentClass2DeclaredConstructor.setAccessible(true);      //次构造方法为私有
        Student student1 = studentClass2DeclaredConstructor.newInstance("乔治");
        
        Student student2 = new Student("佩奇", 5);
        Class<? extends Student> studentClass3 = student2.getClass();
        
        
        Field name = studentClass3.getDeclaredField("name");
        name.setAccessible(true);
        name.set(student2,"苏西");
        name.set(student1,"苏西");
        System.out.println(student1);
        System.out.println(student2);

    }
}
```

### 4.方法的获取使用

![Snipaste_2023-01-05_17-40-17](images\Snipaste_2023-01-05_17-40-17.png)

![Snipaste_2023-01-05_17-42-06](images\Snipaste_2023-01-05_17-42-06.png)

```java
public class MyGetClassMethods {
    public static void main(String[] args) throws ClassNotFoundException, InvocationTargetException, InstantiationException, IllegalAccessException, NoSuchMethodException, NoSuchFieldException {
        
        Student student = new Student("佩奇", 5);
        Class<? extends Student> studentClass = student.getClass();

        Field name = studentClass.getDeclaredField("name");
        name.setAccessible(true);
        name.set(student,"苏西");
        System.out.println(student);

        Method toString2 = studentClass.getMethod("toString");

        System.out.println(student.toString());
        System.out.println(toString2.invoke(student));

        Method myAdd = studentClass.getDeclaredMethod("myAdd", Integer.class, Integer.class);
        myAdd.setAccessible(true);
        System.out.println(myAdd.invoke(student, 2, 3));

    }
}
```

