博客园狂神java学习记录

--------

JDK: Java Development Kit  Java开发工具

JRE: Java Runtime Environment  Java运行环境

JVM: Java Virtual Machine Java虚拟机

DOS: Disk Operating System  磁盘操作系统

## 强类型语言和弱类型语言

强类型语言：所有变量都必须先定义后才能使用。一旦一个变量被指定了某种数据类型，如果不经过强制类型转换，那么它就永远是这个数据类型。例如：你不能把一个整型变量当作一个字符串来处理。

主要语言：Java，C#，Python，Object-C、Ruby

弱类型语言：数据类型可以被忽略，一个变量可以赋不同数据类型的值。一旦给一个整型变量a赋一个字符串值，那么a就变成了字符串类型。

## 动态语言和静态语言

动态语言：在运行时可以改变其结构的语言，例如：新的函数、对象甚至代码可以被引进，已有的函数可以被删除或是其他结构上的变化。

静态语言：在**编译**时进行类型检查的语言，静态语言的编译器能在编译时发现潜在的类型错误，因此静态语言具有较强的类型安全性。例如：java、C、C++，C#等

## 注释

1、单行注释  //
2、多行注释  /*  */
3、文档注释 /**  */

文档注释和多行注释的区别：
文档注释可以在dos界面使用javadoc命令提取文档注释内同生成html文档

## 标识符

Java所有的组成部分都需要名字。类名，变量名，方法名都叫做java的标识符

- 所有的标识符都应该以java字母（包括中文字）、美元符$ 或 下划线_ 开始
- 首字符之后可以是java字母，美元符$ 、下划线_ 或数字的任何字符组合
- 关键字不能作为标识符
- 标识符大小写敏感
- 合法标识符举例：age、$salary、_value、__1_value，你好
- 非法标识符举例：123abc、-salary 、#abc
- 可以使用中文命名，但不建议使用

## 数据类型

### 基本类型

八种

byte
8位、有符号的，以二进制补码表示的整数。
-128~127
默认值是0 
byte类型用在大型数组中节约空间，主要用来代替整型，因为byte变量占用空间只有int类型的四分之一。
例子：byte a = 100, byte b = -50

short
16位、有符号的二进制补码表示的整数
-32768~32767 万级
short数据类型也可以像byte那样节省空间，一个short变量是int型变量所占空间的二分之一
默认值是0

int
32位、有符号的二进制补码表示的整数
-2^31 ~ 2^31-1   十亿级
一般的整型变量默认为int类型
默认值0

long
64位，有符号的二进制补码表示的整数
-2^63~2^63-1
主要使用在需要比较大整数的系统上
默认值是  0L
![long类型测试](https://res.cloudinary.com/dvqgs9esp/image/upload/v1688384024/javaStudy/long_qwhsxv.png)

float 
是单精度、32位，符合IEEE 754标准的浮点数
float在储存大型浮点数组的时候可节省内存空间
默认值是 0.0f
浮点数不能用来表示精确的值，如货币。
例子：`float f1 = 234.5f`
后面要加f，因为java中浮点数的默认数据类型是double，当我们将一个浮点数赋值给任何类型变量时，这个浮点数默认是double类型
如果我们将整数赋值给float，因为float的取值范围大于int，会自动进行转换
如果我们将浮点数赋值给float，因为float的取值范围小于double，此时需要在后面加上F进行强转。

double
双精度、64位，符合IEEE 754标准的浮点数
浮点数的默认类型为double类型
double类型同样不能表示精确的值，如货币。
默认值是 0.0d 可省略
例子：`double d1  = 123.4`

boolean
虽然 boolean 类型只有两个取值，即 true 和 false，理论上可以使用一个 bit（1位）来表示，但由于计算机内存通常以字节为最小单位进行存储，因此 boolean 类型在内存中通常被分配一个字节的空间。

char
是单一的16位Unicode字符
最小值是\u0000 (即为0)
最大值是\uffff  (即为65535)
char数据类型可以储存任何字符
例如：`char letter = 'A'`

### 数据类型面试题

```java
    int bin_num = 0b10; // 二进制0b开头
    int oct_num = 010; //八进制 0 开头
    int dec_num = 10;
    int hex_num = 0x10;  //16进制0x开头
    //默认输出10进制
    System.out.println(bin_num);//2
    System.out.println(oct_num);//8
    System.out.println(dec_num);//10
    System.out.println(hex_num);//16
```

#### 浮点数精度会有丢失

所以银行业务不用float，用BigDecimal

最好完全避免使用浮点数进行比较

```java
    float num1 = 4.0f;
    float num2 = 3.6f;
    System.out.println(num1 - num2);//0.4000001
```

如何解释出现4.0-3.6 =  0.4000001
答：二进制小数无法精确的表示10进制小数，计算机在计算4.0-3.6时，先将两数转成2进制形式，用二进制计算后再将结果转成十进制，这期间出现了误差。

### BigDecimal

1、创建BigDecimal对象

~~~java
BigDecimal number1 = new BigDecimal("10.25");
BigDecimal number2 = new BigDecimal(5.75);
~~~

2、基本运算

~~~java
BigDecimal sum = number1.add(number2);
BigDecimal difference = number1.subtract(number2);
BigDecimal product = number1.multiply(number2);
BigDecimal quotient = number1.divide(number2, 2, RoundingMode.HALF_UP);//除法比较麻烦，要设置精确度，和舍入规则，不然要报错
~~~

3、比较两个BigDecimal对象

~~~java
int result = number1.compareTo(number2);//返回值为整数。如果结果为负数，则表示第一个对象小于第二个对象；如果结果为正数，则表示第一个对象大于第二个对象；如果结果为零，则表示两个对象相等。
~~~



#### 字符串扩展

```java
    char ch = 'A';
    System.out.println(ch);//A
    System.out.println((int)ch);//65
    System.out.println('\u0041');//A
    // 底层原理 是 '\u0041'  十进制的65 -> 十六进制41
    //所有字符本质还是数字
```

#### 什么是字节

- 位（bit）：是计算机内部数据储存的最小单位，1100 1100 是一个八位二进制数
- 字节（byte）：是计算机中数据处理的基本单位，习惯上用大写B来表示
- 1B(byte,字节) = 8 bit（位）
- 字符：是指计算机中使用的字母、数字、字和符号

### 引用类型(reference type)

除了八大基本数据类型之外其他都是引用类型

如 类，接口，数组等

- 在Java中，引用类型的变量非常类似于C/C++的指针，引用类型指向一个对象，指向对象的变量是引用变量。
  这些变量在声明时被指定为一个特定的类型，变量一旦声明后，类型就不能被改变了。
- 对象，数组都是引用数据类型
- 所有引用类型的默认值都是null
- 一个引用变量可以用来引用任何与之兼容的类型

### 浮点储存模型

二进制的科学计数法来保存浮点数

例如：5.5，其二进制数为101.1，则用二进制的科学计数法可以表示为1.011*2^2,这样的小数点的位置就是固定的。

任何一个浮点数可以表示为下面的形式（国际标准IEEE 754）

```
(-1)^ S * M * 2 ^ E
(-1)^ S表示符号位，当S=0时，为正；当S=1时，为负
M表示有效数字，M>=1且M<2
2 ^ E表示指数位
```

上面的例子中，S=0，M=1.011，E=2。
所以当存储浮点数时，只需要将上述三个数字保存起来，就可以了。
单精度浮点数存储模型：S占一位，E占8位，M占23位

### 类型转换

整型、实型（常量）、字符型数据可以混合运算，运算中，不同类型的数据先转化为同一类型，然后进行运算。

转换从低级到高级

低---------------------------------------------------------------------> 高

byte,short,char ->int->long ->float -> double

数据类型转换必须满足如下规则：

- 不能对boolean类型进行类型转换。

- 不能把对象类型转换成不相关类的对象。

- 在把容量大的类型转换为容量小的类型时必须使用强制类型转换。

- 转换过程可能导致溢出或损失精度，例如：

  ```java
          int i = 128;
          byte b = (byte)i;
          System.out.println(b);//-128
  ```

  因为byte类型是8位，最大值为127，所以当int强制转换为byte类型时就会导致溢出

- 浮点数到整数的转换是通过舍弃小数得到，而不是四舍五入，例如：

  ```java
          System.out.println((int)23.6);//23
  ```

  
### 自动类型转换（低到高）

  必须满足转换前的数据类型的位数要低于转换后的数据类型，例如：

  short数据类型的位数为16位，就可以自动转换位数为32的int类型

### 强制类型转换（高到低）

条件是转换的数据类型必须是兼容的

### 隐含强制类型转换

整数的默认类型是int

浮点型不存在这种情况，因为在定义float类型时必须在数字后面跟上F或f

```java
        int i = 128;
        byte b = (byte)i;//高->低 强制类型转换
        double d = i;//低->高 自动类型转换
        System.out.println(b);//-128  溢出了
        System.out.println(d);//128.0
        System.out.println('a');//a
        System.out.println('a' + 1);//98
        System.out.println("---------------------------------------");
        //jdk7 特性
        int num =  10_0000_0000;
        System.out.println(num);//1000000000
        System.out.println(num*20);//-1474836480  // int 的范围21亿多，现在结果200亿溢出
        System.out.println((long)num*20);//20000000000  //先转换再计算
        System.out.println((long)(num*20));//-1474836480  //先计算再转换
```

## 变量、常量

在java中所有变量在使用前必须声明。声明的基本格式如下：

`type varName[ = value][,varName[ = value]...]`刁公式根本不是人看的，简而言之：
类型 变量名 = 初值，变量名2 = 初值...

   作用域：

- 类变量：独立于方法之外的变量，用static修饰
- 实例变量：独立于方法之外的变量，不过没有static修饰
- 局部变量：类的方法中的变量

```java
public class Hello {

    static int allClicks = 0;//类变量
    String str = "hello world";//实例变量

    public void method() {
        int i = 0;//局部变量
    }
}
```

### 类变量（静态变量）

- 在类中以static关键字声明，但必须在方法之外
- 无论一个类创建了多少个对象，类只拥有类变量的一分拷贝。
- 静态变量除了被声明为常量外很少使用。
- 静态变量在类加载时被初始化，并在整个应用程序的执行过程中持续存在，直到应用程序结束或类被卸载。
- 静态变量可以通过：`类名.变量名` 的方式访问
- 类变量被声明为public static final 类型时，类变量名称一般建议使用大写字母。如果静态变量不是public 和 final类型，其命名方式与实例变量以及局部变量的命名方式一致。

### 实例变量

- 声明在一个类中，但在方法、构造方法和语句块之外。
- 当一个对象被实例化之后，每个实例变量的值就跟着确定。
- 实例变量在对象创建的时候创建，在对象销毁的时候销毁
- 实例变量的值应该至少被一个方法、构造方法或者语句块引用，使得外部能够通过这些方法获取实例变量信息
- 实例变量可以声明在使用前或者使用后
- 访问修饰符可以修饰实例变量
- 实例变量对于类中的方法、构造方法或者语句块是可见的。一般情况下应该把实例变量设为私有。通过使用访问修饰符可以使实例变量对子类可见。
- 实例变量具有默认值。数值型变量的默认值是0，布尔型变量的默认值是false，引用类型变量的默认值是null，变量的值可以在声明时指定，也可以在构造方法中指定。
- 实例变量可以直接通过变量名访问。但在静态方法以及其他类中，就应该使用完全限定名：ObjectReference.VariableName

### 局部变量

- 局部变量声明在方法、构造方法或者语句块中
- 局部变量在方法、构造方法、或者语句块被执行的时候创建，当它们执行完成后，变量将会被销毁。
- 访问修饰符不能用于局部变量
- 局部变量只在声明它的方法、构造方法或者语句块中可见。
- 局部变量是在栈上分配的。
- 局部变量没有默认值，所以局部变量被声明后，必须经过初始化，才可以使用

### 常量

常量在程序运行时是不能被修改的。

在java中使用final关键词来修饰常量，声明方式和变量类似。

~~~java
final double PI = 3.14159265358979323846
~~~

### 转义字符

\n ---- 换行符

\r ---- 回车：当在字符串中使用 `\r` 时，它将移动光标到当前行的开头位置。

~~~java
// 在控制台输出多行文本
System.out.println("Line 1\rLine 2");
//输出结果为Line 2
//在这个例子中，\r 的作用是将光标移动到行的开头位置，覆盖了原本的 "Line 1" 部分，因此输出结果只显示了 "Line 2"。
~~~

\b ---- 退格符：当在字符串中使用 `\b` 时，它会删除前一个字符，相当于将光标向左移动一个位置。

\0 ---- 空字符，它对应ASCII码值为0的字符。在字符串中使用`\0`可以插入一个空字符，空字符是一个不可见的字符，通常在字符串末尾作为结束符使用。

修饰符不区分先后顺序：

~~~java
//以下均合法
static final double PI = 3.1415927;
final static double PI = 3.1415927;
~~~

### 运算符

java关系运算符中还有个  instanceof，用于检查对象是否属于某个特定的类或其子类的实例。

位运算符中还有个`>>>`，是无符号右移运算为，该运算符用于将一个数的二进制表示向右移动指定的位数，并在左侧插入零。与右移运算符（`>>`）不同，无符号右移运算符不考虑数的符号位，而是将所有位都右移。

## `&`和`&&`的区别

单&时，左边无论真假，右边都进行运算
双&时，如果左边为真，右边参与运算，如果左边为假，那么右边不参与运算

`|`和`||`区别同理

## Scanner 类

~~~java
import java.util.Scanner;
Scanner s=new Scanner(System.in);//创建扫描器对象，用于接受键盘数据
if(s.hasNext()){
	String str=s.next();
	System.out.println(str);
}
s.close();//凡是属于IO流的类如果不关闭会一直占用资源，用完要关闭
~~~

`next()` ---- 有效字符之前的空白自动去掉，之后的空白作为分隔符或结束符
`nextLine()` ---- 以Enter作为结束符
`s.hasNextInt()` ---- 一次执行后退出

## 方法的重载

重载就是在一个类中，有相同的函数名称，但形参不同的函数

方法的重载规则：

- 方法名称必须相同
- 参数列表必须不同（个数不同或类型不同或参数排列顺序不同等）
- 方法的返回类型无所谓，仅仅返回类型不同不足以成为方法的重载

实现原理：

方法名称相同时，汇编器会根据调用方法的参数个数、参数类型等去逐个匹配，以选择对应的方法，如果匹配失败，则编译器报错。

## 可变参数

从JDK1.5开始，Java支持传递同类型的可变参数给一个方法。

在方法声明中，在指定参数类型后加一个省略号

一个方法只能指定一个可变参数，它必须是方法的最后一个参数

## 递归

A方法调用A方法，就是自己调用自己

递归结构包括两个部分：

- 递归头：什么时候不调用自身方法。如果没有头，将陷入死循环
- 什么时候调用自身方法

## 数组

### 1、声明和创建

~~~java
int[] nums = new int[10];
~~~

或者

~~~java
//1.声明一个数组
int[] nums;
//2.创建一个数组
nums = new int[10];
~~~

### 2、三种初始化方式

- 静态初始化

~~~java
//静态初始化：创建 + 赋值；
int[] a = {1,2,3,4,5};
~~~

- 动态初始化

~~~java
//动态初始化：包含默认初始化
int[] b = new int[10];
b[0] = 10;
~~~

- 默认初始化

数组是引用类型，它的元素相当于类的实例变量，因此数组一经分配空间，其中的每个元素也被按照实例变量同样的方式被隐式初始化。

## 面向过程和面向对象

### 面向过程

步骤清晰简单，第一步做什么，第二步...

适合处理一些较为简单的问题

### 面向对象的思想

分类的思维模式，思考问题首先会解决问题需要哪些分类，然后对这些分类进行单独思考，最后才对某个分类下的细节进行面向过程的思索。

适合处理复杂的问题，适合处理需要多人协作的问题

**面向对象所封装的就是面向过程** ---- HeartWardrum

对于描述复杂的事务，为了从宏观上把握、从整体上合理分析，我们需要使用面向对象的思路来分析整个系统。但是，具体到微观操作，仍然需要面向过程的思路去处理。

## 类和对象的关系

**类**是一种抽象的数据类型，它是对某一类事务整体描述/定义，但是并不能代表某一个具体的事务。

如：动物、植物、手机、电脑等等

**对象**是抽象概念的具体实例

张三就是一个具体的人，张三家的旺财就是动物的一个具体实例

能够体现出特点，展现出功能的是具体的实例，而不是一个抽象的概念。

## 创建对象

对象是根据类创建的。在java中，使用关键字new来创建一个新的对象。创建对象需要以下三步：

- 声明：声明一个对象，包括对象的名称和对象类型
- 实例化：使用关键词new来创建一个对象
- 初始化：使用new创建对象时，会调用构造方法初始化对象。

~~~java
public class Application {
    public static void main(String[] args) {
        // 类：抽象的模板 Student类
        // 对象：具体的个体 小明
        Student xiaoMing = new Student();
        xiaoMing.name = "小明";
        xiaoMing.age = 18;
        xiaoMing.study();

        // 实例化得到 小红 对象
        Student xiaoHong = new Student();
        xiaoHong.name = "小红";
        xiaoHong.age = 18;
        xiaoHong.study();
    }
}

class Student {

    // 属性：字段
    String name;
    int age;

    // 方法
    public void study(){
        System.out.println(this.name+"在学习");
    }
}
~~~

## 构造器

构造器也称构造方法，每个类都有构造方法

构造方法的特点：

- 必须和类名相同
- 不能有返回类型，也不能写void

作用：

- new 本质在调用构造方法
- 初始化对象的值

如果没有显式地为类定义构造方法，Java编译器将会为该类提供一个默认的构造方法

在创建一个对象的时候，至少要调用一个构造方法，一个类可以有多个构造方法

如果在java代码中没有显式定义构造方法，编译器在每个类编译成对应的class文件时，将添加一个无参构造器

## 方法

### 什么是方法

java方法是语句的集合，它们在一起执行一个功能

- 方法是解决一类问题的步骤的有序组合
- 方法包含于类或对象中
- 方法在程序中被创建，在其他地方被引用

### 方法的定义

一般情况下，定义方法包含以下语法：

~~~java
修饰符 返回值类型 方法名(参数类型 参数名){
    ...
        方法体
    ...
        return 返回值;
    
}
~~~

参数像是一个占位符

### 修饰符

java中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。

- public：对所有类可见。使用对象：类，接口、变量、方法

- protected：对同一包内的类和所有子类可见。使用对象：变量、方法。注意：不能修饰类（外部类）

- default：在同一包内可见，使用对象：类、接口、变量、方法

- protected：对同一包内的类和所有子类可见。

  | 修饰符      | 当前类 | 同一包内 | 子孙类(同一包) | 子孙类(不同包) | 其他包 |
  | ----------- | ------ | -------- | -------------- | -------------- | ------ |
  | `public`    | Y      | Y        | Y              | Y              | Y      |
  | `protected` | Y      | Y        | Y              | Y/N（说明）    | N      |
  | `default`   | Y      | Y        | Y              | N              | N      |
  | `private`   | Y      | N        | N              | N              | N      |

### 非访问修饰符

static修饰符，用来修饰类方法和类变量

final修饰符，用来修饰类、方法和变量
final修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。

abstract： 用来创建抽象类和抽象方法

synchronized 和 volatile 主要用于线程的编程

### 可变参数

JDK1.5开始，java支持传递同类型的可变参数给一个方法

方法的可变参数的声明如下：

~~~java
typeName... parameterName
~~~

~~~java
public class Changeable {
    public static void main(String[] args) {
        changeableValue(0,1,2,3,1,2,3);
    }

    public static void changeableValue(int... i) {
        for (int o : i) {
            System.out.println(o);
        }
    }
}
~~~

### 静态方法

static关键字用来声明独立于对象的静态方法。静态方法与类共存，对象还未实例化时就已经存在。

静态方法不能使用类的非静态变量，也不能调用非静态方法（存在的东西 不能调用 不存在的东西）

静态方法推荐以 `类名.方法名`调用

### 非静态方法

无static修饰，需要实例化对象，才能调用方法

~~~java
public class StaticTest {
    public static void main(String[] args) {
        say();
    }

    public static void say() {
        System.out.println("静态方法类加载时就已经存在，独立于对象");
        //nonStatic();// 调用不存在的方法！报错
        new StaticTest().nonStatic(); // 需要创建对象才产生非静态方法！
    }

    public void nonStatic(){
        System.out.println("这是个非静态方法，需要对象实例化才存在");
        // say();  // 调用已存在的方法，没问题
    }
}
~~~

静态方法和非静态方法的本质区别：

- 静态方法是类中使用static修饰的方法，在类定义的时候已经被装载和分配。
- 而非静态方法是不加static关键字的方法，在类定义时没有占用内存，只有在类被实例化成对象时，对象调用该方法才被分配内存

### 实际参数

传递给被调用方法的值，预先创建并赋予确定值

### 形式参数

用来接收调用该方法时传递的参数，只有在被调用的时候才分配内存空间，一旦调用结束，就释放内存空间，因此仅仅在方法内有效。

### 值传递

形参是实参的拷贝，改变形参的值不会影响外部实参的值

### 引用传递

在调用函数时将实际参数的地址直接传递到函数中，那么在函数中对参数进行修改，将影响到实际参数。

~~~java
class Hello{

	public static void main(String[] args){
		StringBuffer stringBuffer = new StringBuffer("hello");
		System.out.println(stringBuffer.toString());
		change(stringBuffer);
		System.out.println(stringBuffer.toString());
	}

	private static void change(StringBuffer s){
		s.append(" world");
	}
}
~~~

注意：在Java中，字符串是不可变的（immutable）。这意味着一旦创建了一个字符串对象，它的值就不能被改变。当你尝试对字符串进行修改时，实际上是创建了一个新的字符串对象，而原始的字符串对象保持不变。

~~~java
public class Quote {
    public static void main(String[] args) {
        String str = "hello";
        System.out.println(str);//hello
        change(str);
        System.out.println(str);//hello
    }

    private static void change(String s) {
        s = "hello world";
    }
}

~~~

在给定的代码中，当`change`方法被调用时，它接收一个字符串参数`s`。然后，在`change`方法内部将`s`赋值为新的字符串`"hello world"`。这个赋值操作只是将`s`引用指向了一个新的字符串对象，而原始的字符串对象`"hello"`并没有发生改变。

在`main`方法中，虽然调用了`change`方法并将`str`作为参数传递，但在`change`方法内部对`s`的修改不会影响到`main`方法中的`str`。这是因为字符串是不可变的，对于传递给方法的参数，其实际上是参数值的一个副本。在方法内部对副本的修改不会影响到原始的变量。

因此，最终在`main`方法中打印`str`时，它的值仍然是原始的字符串`"hello"`，并没有发生改变。

### 通过命令行传参

有时候你希望运行一个程序时候再传递给它消息，这要靠传递命令行参数给main()函数实现

命令行参数是再执行程序时紧跟在程序名字后面的信息

实例：

~~~java
class Hello{

	public static void main(String[] args){
		
		for(String arg: args){
			System.out.println(arg);
		}
	}
	
}
//在命令行中输入：
//javac Hello.java
//java Hello  121 21
//打印：
//121
//
//
~~~



