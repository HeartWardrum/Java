# 第一天

面向对象

一个类的某个对象是另外一个类的方法的参数

和类同名的方法——构造方法

### java标识符命名规则：

- 类名：首字母大写
- 变量名和方法名：首字母小写
  - 如果有多个单词，后面每个单词首字母大写（驼峰命名法）


### java代码的编写

1. 先有类后有对象

   - 我们使用class关键词定义一个类

   - 类：

     - 成员变量： 类型 变量名 = 初始值；

     - 方法： 返回值类型 方法名（参数1，参数2...）{

       方法体；

       }

  2. 每一句话都以分号结尾

  3. 
     |    基本数据类型     |  缺省值  |
     | :-----------------: | :------: |
     | byte short int long |    0     |
     |    float double     |   0.0    |
     |        char         | '\u0000' |
     |       boolean       |  false   |

     

 4. 引用类型默认值： null

 5. 定义多个变量 ： double x,y,z;

### 引用类型

如果 reference 类型的数据中存储的数值代表的是另外一块内存的起始地址，就称为这块内存代表着一个引用。

~~~~java
String s; //创建一个引用，引用可以独立存在，并不一定需要和一个对象相关联
String str = new String("123");//通过将这个叫“引用”的标识符指向某个对象，之后便可以通过这个引用来实现操作对象了。
~~~~

- 强引用

  ~~~~java
  //Java中默认声明的就是强引用，比如：
  Object obj = new Object(); //只要obj还指向Object对象，Object对象就不会被回收
  obj = null;  //手动置null
  //只要强引用存在，垃圾回收器将永远不会回收被引用的对象，哪怕内存不足时，JVM也会直接抛出OutOfMemoryError，不会去回收。如果想中断强引用与对象之间的联系，可以显示的将强引用赋值为null，这样一来，JVM就可以适时的回收对象了
  ~~~~

- 软引用

  ~~~~java
  //软引用是用来描述一些非必需但仍有用的对象。在内存足够的时候，软引用对象不会被回收，只有在内存不足时，系统则会回收软引用对象，如果回收了软引用对象之后仍然没有足够的内存，才会抛出内存溢出异常。这种特性常常被用来实现缓存技术，比如网页缓存，图片缓存等
  ~~~~

- 弱引用
- 虚引用

### 构造方法 

用来创建对象的方法，被new关键字调用；其方法名与类同名；

~~~~java
//格式
类名 对象名 = new 类名(); //左边的对象存储一个来自堆的地址
~~~~

当我们不写构造方法，系统会自动提供默认无参构造方法；当我们自己手写时，系统就不会提供默认构造方法；它没有返回值，前面也不能加void

手写有参构造方法时最好再配一个无参构造方法

手写有参构造方法时，往往利用传入的参数给当前对象赋属性值

~~~~java
public class Car{
	String brand;
    Car(String _brand)
    {
        brand = _brand;
}
    Car(){
        
    }
}
//调用
Car c = new Car("奥迪");
~~~~

### 内存解析

虚拟机在内存种识别数据来进行处理

内存被划分为5块：

- 栈：存放局部变量
- 堆：存放new出来的对象
- 方法区：存放人写的静态代码以及常量池
- 本地方法栈：与操作系统相关（仅了解）
- 程序计数器：与CPU相关（仅了解）

### 方法的重载

在一个类中，多个方法，方法名一样，参数不一样

参数不一样体现在要么参数的个数不一样，要么参数的类型不一样。在调用的时候，根据传入的参数，决定具体调用哪个方法。

构造方法也可以重载

### this

就是一个引用。它在当前对象的内部，存放的是当前对象的内存地址

我们可以通过 this.成员变量 来访问当前对象的成员变量；

还可以通过 this.方法来调用当前类的方法。

### static

1. static可以修饰成员变量，被static修饰的成员变量只有一份，它被当前类的所有对象共享；我们可以使用任一对象访问static的成员变量，也可以直接使用类名访问static的成员变量；static的成员变量往往可以用来计数。
2. static可以修饰方法，这样的方法叫作静态方法，静态方法可以被类名直接调用。静态方法种调用本类其他的静态方法，连类名也可以省略。静态方法种不能直接调用本类种其他非静态方法。

# 第二天

### 包

java中为了解决类名冲突的问题，引入了包的概念，包可以层层嵌套，同一个包下不允许有相同的类名；往往包名都是所在公司域名的倒写;

注意：同一个包下的类可以直接使用，前面不用加包名。

~~~~java
package 包名；//定义一个包
    //例如
    package com.iweb.test;
/////////////
import 全类名；//导入具体的某个包，然后再当前类中就可以直接使用（全类名：带有包名的类名）
    import com.iweb.test.Cat;//如导入包com.iweb.test中的Cat类
//注意：可以导入包.*  来使用该包下所有类
import com.iweb.test.*;
~~~~

包 java.lang 是唯一一个无需导入,所有包都可以使用其中的类的包。

## 问题：相同类名引入，如何使用？

### 答：遵循以下原则：

前置准备：

~~~~java
package com.a;
public class Test(){
    public int num1 = 1;
}
~~~~

~~~~java
package com.b;
public class Test(){
public int num2 = 2;
}
~~~~

1. 使用声明更具体的包的类

~~~~java
import com.a.*;
import com.b.Test:
//使用b中的Test类
~~~~

2. 导入包声明程度一样具体的——只能使用第一个，第二个直接报错

~~~~java
import com.a.Test;
import com.b.Test;
//只能使用a中的Test；
~~~~

3. 不同导入包都采用通配符声明——必须进行选择才可正常使用

~~~~java
import com.a.*;
import com.b.*;
public static void main(String[] args){
    com.a.Test a = new com.a.Test();//当写出这一行时，开头自动生成 import com.a.Test;
    Test b = new Test();
    //只能用a中的Test
}
~~~~

4. 主程序内采用完整包名新建一个对象，都可以使用

   ~~~~java
   public class Test3 {
       public static void main(String[] args) {
        
           com.a.Test a = new com.a.Test();
           com.b.Test b = new com.b.Test();
   
           System.out.println(a.num1);
           System.out.println(b.num2);
           //都能用
       }
   }
   ~~~~



### 继承

“xxx是一种xxx”  这句话说得通则两者存在继承关系

java只支持单继承，一个子类只能有一个父类

子类继承父类，子类就自动拥有了父类所有的属性和方法，子类还可以有自己新增的属性和方法

子类拥有父类的所有属性和方法，但是子类不能访问父类私有的属性和方法

语法：	class 子类名 extends 父类名

~~~~java
//例：学生类继承人类
public class Student extends Person{
    
}
~~~~

### 继承中的构造方法

1. 子类构造过程中必须先调用父类的构造方法来构造父类对象
2. 当子类中没有写明调用父类的哪个构造方法，则默认调用父类无参的构造方法
3. 我们在子类构造方法中，可以使用 super(参数列表) 来手动调用父类的某个指定的构造方法（注意：super(参数列表)必须写在方法第一行）
4. 如果没有手动调用，而父类中又没有无参的构造方法，则编译报错

### 访问控制符

用来修饰属性和方法

它们的作用范围：

|         | 同一个类 | 同一个包 | 子类 | 任何地方 |
| :-----: | :------: | :------: | :--: | :------: |
| private |    Y     |          |      |          |
|  不写   |    Y     |    Y     |      |          |
| protect |    Y     |    Y     |  Y   |          |
| public  |    Y     |    Y     |  Y   |    Y     |

对于class的修饰可以使用public或者不写，如果不写，只能在当前包中使用

### JavaBean

我们应该将Java中的实体封装成JavaBean，每一个成员变量都私有化，设置为private，针对每个成员变量都提供public 的 get方法来取值，public 的set方法来存值。JavaBean体现了Java面向对象的**封装性**

alt+ins ==> getter and setter 直接生成

### 方法的重写

父类和子类，子类对父类的方法进行重写时，方法名一样，返回值类型一样，参数也一样，根据调用者的类型来决定调用哪个方法

注意：在重写方法的时候可以添加@Override注解检查是否在重写；重写方法不能比被重写方法有更严格的访问权限；

### super

它是一个引用，它指向当前对象的父类对象，我们可以使用 super.成员变量 来访问父类的属性，我们可以使用 super.方法 来调用父类的方法

super(参数)来调用父类中某一个构造函数，调用super()必须写在子类构造方法的第一行，否则编译不通过



~~~~java
//我们可以使用this(参数列表)来调用本类其他构造方法来构造对象
package com.iweb.test2;

public class Person {

    String cardId;
    String name;
    String age;

    public Person(String cardId, String name, String age) {
        this.cardId = cardId;
        this.name = name;
        this.age = age;
    }

    public Person(String cardId) {
        this(cardId, "无名氏", "0");//给另外两个参数赋缺省值
    }

    public Person() {
        this("12313131", "无名氏", "0");//全部赋缺省值
    }
}

~~~~



### Object

这是所有类的根类，当某个类不继承任何类的时候，就相当于继承了Object，任何一个类都拥有并且可以使用Object类中的方法toString()——将当前对象以字符串的形式表现出来。Object中的toString()返回的是 全类名@哈希编码；我们可以自由的重写toString()来更好的描述当前对象。

### instanceof

对象名 instanceof 类名

判断一个类的对象是否是某个类的对象，返回一个boolean值

### “向下转型”和“向上转型”

父类引用可以指向其子类的对象，也就是说子类对象可以当做父类对象来用，这被称为“向上转型”

~~~~java
//父类Animal 	有方法run() 
//子类Cat 	重写方法run() 单独定义方法miaow()
Animal animal = new Cat();//声明的是父类，实际指向子类的一个对象
//注意：
//1. 向上转型后，子类单独定义的方法会丢失（父类并不知道子类定义的新属性与方法） animal.miaow();是错误的
//2. 父类引用可以指向子类对象，但是子类引用不能指向父类对象
//3. 如果子类中重写了父类的方法，那么调用这个方法的时候，将会调用子类中的方法
~~~~

我们可以将父类引用所指向的子类对象通过 (子类类型) 转为子类的类型，这被称为“向下转型”，目的是调用子类独有的方法;这种方法可扩展性好，防止甲方乱改方案。

~~~~java
package com.iweb.test;

//父类：动物类
public class Animal {
    String name;//动物名

    public Animal(String name) {
        this.name = name;
    }

    public void run() {
        System.out.println("会跑");
    }
}

//子类：猫咪类
 class Cat extends Animal {
    String eyesColor;  //猫咪瞳色
    
    public Cat(String name, String eyesColor) {
        super(name);
        this.eyesColor = eyesColor;
    }
    
    public void miaow() {
        System.out.println("喵喵叫");
    }
}
//测试类
 class ZTest {

    public static void main(String[] args) {

        Animal a = new Animal("动物");
        Cat c = new Cat("猫", "蓝色");

        f(a);//最终返回： 动物 该生物不是猫咪
        f(c);//最终返回： 猫 该生物是猫咪 猫 蓝色 喵喵叫

    }

    public static void f(Animal animal) {
        System.out.println(animal.name);

        if (animal instanceof Cat) { //该生物是猫咪 返回1
            System.out.println("该生物是猫咪");
            System.out.println(((Cat) animal).name); //((Cat) animal)即为向下转型
            System.out.println(((Cat) animal).eyesColor);
            ((Cat) animal).miaow();

        } else {
            System.out.println("该生物不是猫咪");
        }
    }
}
~~~~

## 第三天

### equals()方法

Object类的equals方法用来比较两个对象是否相等，它原生态的写法等同于“==”，只有当两个对象是同一对象时返回true；

我们应该按照自己的方式去重写equals()方法

~~~~java
//例题
//自行定义能满足需要的MyDate类，在MyDate类中重写equals方法，使其判断当两个MyDate类型对象的年月日都相同时，结果为true，否则为false

//MyDate类
package com.iweb.homework;

public class MyDate {
    int year, month, day;

    public MyDate() {

    }

    public MyDate(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }


    @Override
    public boolean equals(Object obj) {
        if (obj == null) {
            return false;
        } else {
            if (obj instanceof MyDate) {
                MyDate myDate = (MyDate) obj;
                if (this.year == myDate.year && this.month == myDate.month && this.day == myDate.day) {
                    return true;
                } else {
                    return false;
                }
            } else {
                return false;
            }
        }
    }
}
~~~~

~~~~java
//测试类
package com.iweb.homework;

public class ATest {
    public static void main(String[] args) {
        MyDate myDate1 = new MyDate(2000,1,1);
        MyDate myDate2 = new MyDate(2000,1,1);

        System.out.println(myDate1.equals(myDate2));
    }
}
~~~~

### 运行时多态

又叫做动态绑定

当父类引用指向子类对象的时候，父类的引用去调用父类的方法，实际调用到的是子类重写过后的方法

关键词：继承、重写、父类引用指向子类对象

### 抽象方法

定义：只有方法的声明而没有方法的实现，抽象方法需要被abstract关键字修饰

~~~~java
public abstract void draw();//抽向方法必须被重写
~~~~

### 抽象类 

含有抽象方法的类被称为抽象类

- 抽象类需要被abstract关键字修饰
- 抽象类不能被实例化（不能直接创建对象）
- 抽象类是用来被继承的，抽象方法是用来被重写的

### final

- 可以用来修饰一个类——最终类：它不能被继承

- 可以用来修饰一个变量，它的值不可改变

- 可以用来修饰一个方法，它不能被重写

### 常量

整个内存只有一份

~~~~java
public static final 数据类型 常量名 = 常量值； 
    
//常量有三种
public class HelloWorld {
    // 静态常量
    public static final double PI = 3.14;
    // 声明成员常量
    final int y = 10;

    public static void main(String[] args) {
        // 声明局部常量
        final double x = 3.3;
    }
}
~~~~

### 接口

- 如果一个类中所有的方法都是抽象的，那么这个类可以做成接口
- 接口使用interface定义
- 接口被实现类来实现，我们使用implements关键字进行实现
- 实现一个接口，就必须重写接口中所有的抽向方法
- 接口类型的引用可以指向实现类的对象，当它调用接口中的方法时，实际调用到的是实现类中重写过后的方法
- 一个类可以同时实现多个无关的接口
- 注意：当一个类实现多个接口时，该类对象可以多个接口之间转换
- 1. 接口中没有成员变量，只有常量，它是常量和抽象方法的集合
  2. 接口中所有方法都是public，而且只能是public
  3. 1.8及以后版本的jdk，接口中还可以存在static修饰的非抽象方法，使用  接口名.方法名  直接调用

~~~~java
//画家接口
package com.iweb.test2;

public interface Painter {
    public void draw();
    public void sleep();
    public void eat();
    public static void methodInterface(){   //1.8及以后版本的jdk，接口中还可以存在static修饰的非抽象方法，使用  接口名.方法名  直接调用  例如：在测试类中写   Painter.methodInterface();
        System.out.println("我是接口内的非抽象函数")；            
    }
    
}
~~~~

~~~~java
//歌手接口
package com.iweb.test2;

public interface Singer {
    public void sing();
    public void sleep();
}
~~~~

~~~~java
//老师类
package com.iweb.test2;
public class Teachers implements Singer,Painter { //用implements来实现一或多个接口


    @Override
    public void draw() {
        System.out.println("老师在画画");
    }

    @Override
    public void eat() {
        System.out.println("老师在吃饭");
    }

    @Override
    public void sing() {
        System.out.println("老师在唱歌");
    }

    @Override
    public void sleep() {
        System.out.println("老师在睡觉");
    }
}
~~~~

## 第四天

### getClass()

获得当前对象的全类名

### 异常

在代码运行的过程中发生的某些错误情况，例如：除0错误等

### try {    }    catch(){   }

一个try可以对应多个catch，这些catch按照先捕获小的异常再捕获大的异常这样的原则进行顺序编译，也可以只捕获大的异常。

~~~~java
try{
    //里面编写一些可能发生异常的代码
}
catch(异常类型 变量名){
    //catch块   当代码块发生异常时要做的事
}
~~~~

~~~~java
package com.iweb.test;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;

public class Test6 {

    public static void main(String[] args) {
        InputStream is = null;
        try {
            is = new FileInputStream("D:\\Desktop\\内容读取.txt");
            int i = 0;
            while ((i = is.read()) != -1) {
                System.out.print((char) i);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                is.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
~~~~

### finally{  }

它是跟在try/catch后面的第三个代码块，写在finally里面的代码是无论如何都一定会被执行

- 注意：如果finally代码块前面执行了return语句，它依然会执行，并且是在return之前执行

### throws

写在方法声明处【签名(方法的名称+参数类型)的尾部】，表示该方法可能抛出怎样的异常

当一个方法产生一个它不处理的异常时，那么就需要在该方法的头部声明这个异常，以便将该异常传递到方法的外部进行处理

~~~~java
static void b(int n, int m) throws ArithmeticException {
            int result = n / m;
            System.out.println(result);
    }
~~~~

### throw 

~~~~java
//人为的手动抛异常
throw new 异常对象 
~~~~

throw 和 throws 的区别：

- throws 用来声明一个方法可能抛出的所有异常，而 throw 则是抛出一个具体的异常类型
- 通常在一个方法的声明处通过 throws 声明方法可能抛出的所有异常信息，而在方法的内部声明一个具体的异常信息
- throws 通常不明显地捕获异常，而是由系统自动将所有捕获的异常信息抛给上级方法，throw 则需要程序员自己捕获相关的异常，然后再对其进行包装，最后将包装的异常信息抛出。



### 异常类的结构图

注意：RunTimeException在编译的过程中，可以不被try/catch或者throw/throws；而剩下的异常必须被try/catch或者throw/throws，否则边编译报错

<img src="https://cdn.jsdelivr.net/gh/HeartWardrum/MyImageHost/异常类的结构图.png" alt="异常类的结构图" style="zoom:67%;" />

### String

不可变的字符序列（关于它的变化都会创建一个新字符串）

我们可以通过String 变量名 = "字符串"  来创建一个String对象，它存放在常量区

当我们new String(字符串)时，它实际上创建了两个对象，将指定的字符串对象拷贝了一份

在比较两个字符串的时候，统一使用equals()方法，它比较的是字符串的内容相不相同

```java

String s1 = "hello",s2 = "HELLO",s3 = "e";
s1.equalsIgnoreCase(s2); //字符串比较，忽略大小写
s1.indexOf(s3);//返回指定字符在字符串中第一次出现处的索引，如果此字符串中没有这样的字符，则返回 -1

//字符串分割 spilit("正则表达式")
String s6 = "Tom,Jerry,Marry";
String[] arr = s6.split(",");
for (int i = 0; i < arr.length; i++) {
     System.out.println(arr[i]);
}

//字符串截取  substring(int beginString,int endString)
String s7 = s6.substring(4);
System.out.println(s7);  //Jerry,Marry
String s8 = s6.substring(4, 9);
System.out.println(s8); //Jerry

//取出字符串前后空格  trim()
String s10 = "     hello    ";
String s11 = s10.trim();
System.out.println("s11 =" + s11);//s11 =hello

//其他类型转字符串  String.valueOf()


    
```

详见API文档

### StringBuffer

可变的字符串

我们通过 new StringBuffer(String s)来构造一个StringBuffer对象

~~~~java
//append(String s)   在原字符串后面追加新的字符串
String s = "hello world";
StringBuffer stringBuffer = new StringBuffer(s);
System.out.println(stringBuffer);//hello world
stringBuffer.append(",Tom").append(",Jerry");//甚至可以多次追加
System.out.println(stringBuffer);//hello world,Tom,Jerry

//delete(起始位置，结束位置)   从起始位置删除到结束位置
//insert(位置，String s)    在指定位置插入字符串
 StringBuffer stringBuffer1 = new StringBuffer("0123456789");
 stringBuffer1.delete(4,stringBuffer1.length());
 System.out.println(stringBuffer1); //0123
 stringBuffer1.insert(1,arr);
 System.out.println(stringBuffer1);//0abc123
~~~~

### StringBuilder

可变的字符串

面试题：StringBuffer  和  StringBuilder的区别

- StringBuffer 线程安全（同步），性能较差
- StringBuilder  线程不安全，性能较好

### Math类

算数相关的类，提供各种算数运算的静态方法    Math.方法名

~~~~java
System.out.println(Math.round(3.14)); //4舍5入取整    此处返回3
System.out.println(Math.abs(-100));  //取绝对值  此处返回100
System.out.println(Math.sqrt(81.0));  //开方  此处返回9.0
~~~~

### BigDecimal类

大数值型，可以解决java中基本数据类型长度限制和计算精度的问题

~~~~java
double d3 = 1.2;
double d2 = 1.1;
System.out.println(d3 - d2);//0.09999999999999987

BigDecimal b1 = new BigDecimal("1.2");
BigDecimal b2 = new BigDecimal("1.1");
BigDecimal b3 = b1.subtract(b2);//b1-b2
System.out.println(b3);//0.1
double result = b3.doubleValue();//将此 BigDecimal转换为 double 
System.out.println(b3);//0.1

System.out.println("加法" + b1.add(b2));//2.3
System.out.println("乘法" + b1.multiply((b2)));//1.32
System.out.println("保留五位小数" + b1.divide(b2, 5, BigDecimal.ROUND_HALF_UP));//1.09091
  
~~~~

### 简单的文件读取

~~~~java
package com.iweb.test;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;

public class Test6 {

    public static void main(String[] args) {
        InputStream is = null;
        try {
            is = new FileInputStream("D:\\Desktop\\内容读取.txt");
            int i = 0;
            while ((i = is.read()) != -1) {
                System.out.print((char) i);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                is.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
~~~~



# 问题

