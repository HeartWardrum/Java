---
title:  笔记_001_java
tag: 
	- java
categories: 
	- java
---

# 第一天

## 面向对象

一个类的某个对象是另外一个类的方法的参数
把现实生活的事物以及关系，抽象成类，通过继承，实现，组合的方式把万事万物都给容纳了。实现了对现实世界的数学建模

举个例子： 想吃蛋炒饭
面向过程：自己去买鸡蛋，米饭，起锅浇油炒饭，最后吃到
面向对象：对老妈喊我要吃蛋炒饭，根本不需要知道怎么做，饭来张口就能吃到

- 面向过程是具体化的，流程化的，解决一个问题，你需要一步一步的分析，一步一步的实现。
- 面向对象是模型化的，只需抽象出一个类，这是一个封闭的盒子，在这里我们拥有数据也拥有解决问题的方法，需要什么功能直接使用就可以了，至于这个功能是如何实现的，我们不必知道

面向对象是为了模拟现实：就好比想吃饭的只需要知道怎么咀嚼，而不需要知道怎么下厨

### 面向对象的三大特性
1、封装
隐藏对象的属性和实现细节，仅对外提供公共访问方式，将变化隔离，便于使用，提高复用性和安全性。
2、继承
子类从父类继承方法，使得子类具有父类相同的行为。继承是多态的前提
3、多态
父类或接口定义的引用变量可以指向子类或具体实现类的实例对象。提高了程序的拓展性。

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
     | 基本数据类型(值类型) |  缺省值  |
     | :------------------: | :------: |
     | byte short int long  |    0     |
     |     float double     |   0.0    |
     |         char         | '\u0000' |
     |       boolean        |  false   |

     

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
  //只要强引用存在，垃圾回收器将永远不会回收被引用的对象，哪怕内存不足时，JVM也会直接抛出OutOfMemoryError，不会去回收。如果想中断强引用与对象之间的联系，可以显式地将强引用赋值为null，这样一来，JVM就可以适时的回收对象了
  ~~~~

- 软引用

  ~~~~java
  //软引用是用来描述一些非必需但仍有用的对象。在内存足够的时候，软引用对象不会被回收，只有在内存不足时，系统才会回收软引用对象，如果回收了软引用对象之后仍然没有足够的内存，才会抛出内存溢出异常。这种特性常常被用来实现缓存技术，比如网页缓存，图片缓存等
  ~~~~

- 弱引用
- 虚引用

### 构造方法 

用来创建对象的方法，被new关键字调用；其方法名与类同名；

~~~~java
//格式
类名 对象名 = new 类名(); //左边的对象存储一个来自堆的地址
~~~~

当我们不写构造方法，系统会自动提供默认无参构造方法；当我们自己手写时，系统就不会提供默认构造方法；构造方法没有返回值，前面也不能加void

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

虚拟机在内存中识别数据来进行处理

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
- 实现一个接口，就必须重写接口中所有的抽象方法
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

<img src="D:\GitHub\MyImageHost\异常类的结构图.png" alt="异常类的结构图" style="zoom:67%;" />

### String

不可变的字符序列（关于它的变化都会创建一个新字符串）

我们可以通过String 变量名 = "字符串"  来创建一个String对象，它存放在常量区

当我们new String(字符串)时，它实际上创建了两个对象，将指定的字符串对象拷贝了一份

~~~~java
String str = new String("aa");//1.常量池里创建一个 "aa"对象，这是第一个对象
                              //2. 执行该行代码时new一个"aa"的String对象存放在Java堆中，这是第二个对象
						    //3. 栈上的str会指向第二个对象
~~~~

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



## 第五天 (多线程真tm难)

### Arrays.sort(arr);

//对数组arr进行升序排序

### 读取键盘输入

~~~~java
Scanner sc = new Scanner(System.in);  //System.in 标准输入  

        System.out.println("请输入一个int型的整数：");
        int num = 0;
        try {
            num = sc.nextInt();       //读取整型输入 
        } catch (Exception e) {
            System.out.println("对不起，输入数值非法");
            return;
        }finally {
            sc.close();
        }
        System.out.println("您输入的整数为：" + num);
~~~~

### enum

枚举类型，在定义类型的时候指定它允许的若干值

~~~~java
enum 枚举类型 {
    val1,val2...
};
~~~~

### switch

switch语句允许传入那些类型的变量：byte short int char enum 以及JDK1.7版本之后的String

### 基本数据类型的包装类

我们可以将8种数据类型各自定义为其包装类；包装类的对象中包着基本数据类型的值

~~~~java
Integer 对应 int
Character 对应 char
剩下的六种首字母大写
包装类的对象转基本数据类型 .xxxValue();
//例如：
Integer integer = new Integer(100);
int i = integer.intValue();

//String 转 double  字符串解包
String s = "3.1415926";
double d3 = Double.parseDouble(s);  //parseXxx(String s) 将字符串中的内容转型成基本数据类型
System.out.println(d3);//3.1415926


Double d4 = Double.valueOf(s); //valueOf(string s)将字符串中的内容转型成基本数据类型包装类的对象
System.out.println(d4);//3.1415926 
~~~~

### 自动打包和自动解包

也叫做自动装箱和自动拆箱

- 凡是需要包装类对象的地方，直接传入基本数据类型值即可，系统会自动创建对象
- 凡是需要基本数据类型值的地方，直接传入包装类对象即可，系统会自动将值取出

### 获取当前时间

~~~~java
//方法一 
System.out.println(new Date());//Fri Jul 08 11:23:08 CST 2022

//方法二
SimpleDateFormat sdf = new SimpleDateFormat("hh:mm:ss yyyy/MM/dd");
String s = sdf.format(new Date());
System.out.println(s);//11:23:08 2022/07/08
~~~~

### 进程

- 一段程序的执行过程

### 线程 

- 进程中的一条执行路径
- 线程中的五种状态：

![](https://cdn.jsdelivr.net/gh/HeartWardrum/MyImageHost/线程的五种状态.png)

![线程中的五种状态](D:\GitHub\MyImageHost\线程的五种状态.png)

- 新建状态:
  使用 new 关键字和 Thread 类或其子类建立一个线程对象后，该线程对象就处于新建状态。它保持这个状态直到程序 start() 这个线程。

- 就绪状态:
  当线程对象调用了start()方法之后，该线程就进入就绪状态。就绪状态的线程处于就绪队列中，要等待JVM里线程调度器的调度。

- 运行状态:
  如果就绪状态的线程获取 CPU 资源，就可以执行 run()，此时线程便处于运行状态。处于运行状态的线程最为复杂，它可以变为阻塞状态、就绪状态和死亡状态。

- 阻塞状态:
  如果一个线程执行了sleep（睡眠）、suspend（挂起）等方法，失去所占用资源之后，该线程就从运行状态进入阻塞状态。在睡眠时间已到或获得设备资源后可以重新进入就绪状态。可以分为三种：

  ​			等待阻塞：运行状态中的线程执行 wait() 方法，使线程进入到等待阻塞状态。
  ​			同步阻塞：线程在获取 synchronized 同步锁失败(因为同步锁被其他线程占用)。
  ​			其他阻塞：通过调用线程的 sleep() 或 join() 发出了 I/O 请求时，线程就会进入到阻塞状态。当sleep() 状态超时，join() 等待线程终止或超时，或者 I/O 处理完毕，线程重新转入就绪状态。
  
- 死亡状态:
  一个运行状态的线程完成任务或者其他终止条件发生时，该线程就切换到终止状态。


线程阻塞：通常是指一个线程在执行过程中暂停（例如sleep），以等待某个条件的触发



### 多线程

- 多个线程同时执行

- 实现多线程的方式：

  1. 继承Thread类并重写run()方法，然后利用该类对象调用start()方法启动一个新的线程执行run()方法

     （这种方法不好）
  
     ~~~~java
     package com.iweb.Test;
     public class TestThread extends Thread {
         @Override
         public void run() {
             for (int i = 0; i < 200; i++) {
     
                 System.out.println("我是run方法，我打印到：" + i);
             }
         }
     
         public static void main(String[] args) {
     
             TestThread t = new TestThread();
             t.start();
     
             for (int i = 0; i < 200; i++) {
                 System.out.println("我是main方法，我打印到：" + i);
             }
         }
     }
     //打印结果 两边交替打印，但是所分配时间并不均匀
     我是main方法，我打印到：0
     我是main方法，我打印到：1
     我是main方法，我打印到：2
     我是main方法，我打印到：3
     我是main方法，我打印到：4
     我是run方法，我打印到：0
     我是main方法，我打印到：5
     我是run方法，我打印到：1
     我是main方法，我打印到：6
     我是run方法，我打印到：2
     我是main方法，我打印到：7
     我是main方法，我打印到：8
     我是main方法，我打印到：9
     我是main方法，我打印到：10
     我是main方法，我打印到：11
     我是main方法，我打印到：12
         ......
     ~~~~

     
  
  2. 实现Runnable接口并重写run()方法，使用的时候：
  
     > 首先创建该类对象
     >
     > 然后将该类对象当作参数传入Thread构造方法创建Thread
     >
     > 最后再由Thread对象调用start()方法启动一个新的线程来执行run()方法

~~~~java
public class TestRunnable implements Runnable {
    @Override
    public void run() {
            for (int i = 0; i < 200; i++) {
                System.out.println("我是run方法，我打印到：" + i);
            }
    }

    public static void main(String[] args) {

        TestRunnable tr = new TestRunnable();//先创建该类对象 tr
        Thread t = new Thread(tr);//将tr当作参数传入Thread构造方法创建Thread
        t.start();//Thread对象调用start()

        for (int i = 0; i < 200; i++) {
            System.out.println("我是main方法，我打印到：" + i);
        }
    }
}
//打印结果同第一种
~~~~

**注意**：第二种方法比较好，因为java是单继承多实现，我们应该尽可能将继承的机会留给业务逻辑



#### 常用方法

- sleep(毫秒数) ---- 使当前线程休眠毫秒数

  ~~~~java
  package com.iweb.Test;
  
  import java.text.SimpleDateFormat;
  import java.util.Date;
  
  public class MySleep implements Runnable {
      @Override
      public void run() {
          while (true) {
              SimpleDateFormat sdf = new SimpleDateFormat("hh:mm:ss yyyy/MM/dd");
              String s = sdf.format(new Date());
              System.out.println(s);
              try {
                  Thread.sleep(1000);//
              } catch (InterruptedException e) {  //如果睡眠被中断，直接跳出循环
                  return;    
              }
          }
      }
  }
  ~~~~

  ~~~~java
    //测试类
    package com.iweb.Test;
    import java.util.concurrent.ThreadLocalRandom;
    
    public class Test2 {
    
        public static void main(String[] args) {
            MySleep ms = new MySleep();
            Thread t = new Thread(ms);
            t.start();
    
            try {
                Thread.sleep(10000);//睡10s
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            t.interrupt();
        }
    }
    
    //打印结果   每隔一秒打印当前时间  十秒后停止
    11:31:03 2022/07/08
    11:31:04 2022/07/08
    11:31:05 2022/07/08
    11:31:06 2022/07/08
    11:31:07 2022/07/08
    11:31:08 2022/07/08
    11:31:09 2022/07/08
    11:31:10 2022/07/08
    11:31:11 2022/07/08
    11:31:12 2022/07/08

- join() ---- 使指定线程和当前线程合并为同一个线程

~~~java
package com.iweb.Test;

public class TestRunnable implements Runnable {
    @Override
    public void run() {
        for (int i = 0; i < 200; i++) {
            System.out.println("我是run方法，我打印到：" + i);
        }
    }


    public static void main(String[] args) {

        TestRunnable tr = new TestRunnable();
        Thread t = new Thread(tr);
        t.start();
        try {
            t.join();      // 使指定线程和当前线程合并为同一个线程
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        for (int i = 0; i < 200; i++) {
            System.out.println("我是main方法，我打印到：" + i);
        }
    }
}
//打印结果  run方法先打印完再开始打印main方法
~~~

- yield() ---- 让出当前CPU使自己处于就绪状态

  ~~~java
  package com.iweb.Test;
  
  public class TestRunnable implements Runnable {
      @Override
      public void run() {
          for (int i = 1; i < 201; i++) {
  
  
              System.out.println("我是run方法，我打印到：" + i);
              if (i % 10 == 0) {
                  Thread.yield();
              }
          }
      }
  
  
      public static void main(String[] args) {
  
          TestRunnable tr = new TestRunnable();
          Thread t = new Thread(tr);
          t.start();
  
  
          for (int i = 1; i < 201; i++) {
  
              System.out.println("我是main方法，我打印到：" + i);
              if (i % 10 == 0) {
                  Thread.yield();  //整十的时候更容易发生切换
              }
          }
      }
  }
  
  //打印结果  //整十的时候更容易发生切换
  我是main方法，我打印到：1
  我是main方法，我打印到：2
  我是run方法，我打印到：1
  我是run方法，我打印到：2
  我是main方法，我打印到：3
  我是main方法，我打印到：4
  我是main方法，我打印到：5
  我是run方法，我打印到：3
  我是run方法，我打印到：4
  我是run方法，我打印到：5
  我是main方法，我打印到：6
  我是run方法，我打印到：6
  我是run方法，我打印到：7
  我是run方法，我打印到：8
  ~~~

  - setName(线程名) ---- 可以设定线程的名字
  - currentThread().getName() ---- 获得当前线程的名字

  ~~~~java
  package com.iweb.Test;
  
  public class TestRunnable implements Runnable {
      @Override
      public void run() {
          for (int i = 1; i < 201; i++) {
  
              System.out.println("我是"+Thread.currentThread().getName()+"线程,我打印到：" + i);
          }
      }
  
      public static void main(String[] args) {
  
          TestRunnable tr = new TestRunnable();
          Thread t = new Thread(tr);
          t.setName("啦啦啦");
          t.start();
  
  
          for (int i = 1; i < 201; i++) {
  
              System.out.println("我是main线程,我打印到：" + i);
          }
      }
  }
  
  ~~~~

  

  - setPriority(int i) ---- 设置优先级 1 - 10 

  ~~~~java
  package com.iweb.Test;
  
  public class TestRunnable implements Runnable {
      @Override
      public void run() {
          for (int i = 1; i < 201; i++) {
  
  
              System.out.println("我是main线程,我的优先级为：" + Thread.currentThread().getPriority() + "我打印到：" + i);
  
          }
      }
  
  
      public static void main(String[] args) {
  
          TestRunnable tr = new TestRunnable();
          Thread t = new Thread(tr);
          t.setName("啦啦啦");
          t.setPriority(10);
          t.start();
  
          Thread.currentThread().setPriority(1);
          for (int i = 1; i < 201; i++) {
  
              System.out.println("我是main线程,我的优先级为：" + Thread.currentThread().getPriority() + "我打印到：" + i);
          }
      }
  }
  ~~~~

  

  - getPriority() ---- 获得优先级

  

#### 线程不同步实例

~~~~java
package com.iweb.Test;
public class Time {
    int i = 0;

   void add(String str) {  //第一种方法： synchronized void add(String str) 则线程同步
        this.i++;
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(str + "你好，你是第" + i + "个访问该对象的线程");
    }
}
~~~~

~~~~java
package com.iweb.Test;

public class TestSync implements Runnable {
    Time time;

    TestSync() {
        time = new Time();
    }

    @Override
    public void run() {
        time.add(Thread.currentThread().getName());
    }
}
~~~~

~~~java
//测试类
package com.iweb.Test;

public class Test11 {


    public static void main(String[] args) {
        TestSync testSync = new TestSync();
        Thread t1 = new Thread(testSync);
        Thread t2 = new Thread(testSync);
        t1.setName("t1");
        t2.setName("t2");
        t1.start();
        t2.start();
    }
}
~~~

- synchronized ----- 可以添加在方法的声明处，使得当前方法线程同步，也就是说当一个线程方法访问某对象的该方法，其他线程无法访问该对象的该方法

~~~java
synchronized(对象){
    不可分割的代码块
}
~~~

~~~java
package com.iweb.Test;

public class Time {
    int i = 0;

    void add(String str) {
        synchronized (this) {  //第二种方法  线程同步
            this.i++;
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(str + "你好，你是第" + i + "个访问改对象的线程");
        }
    }
}
~~~

### 死锁

多个线程同时锁定了对方想要锁定的对象，导致相互等待

 简单死锁：

~~~~java
package com.iweb.test;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-22/0022
 * 描述：简单死锁实例
 */

public class TestDeadLock implements Runnable {
    boolean flag;


    public boolean isFlag() {
        return flag;
    }

    public void setFlag(boolean flag) {
        this.flag = flag;
    }

    //必须要静态变量
    static Object o1 = new Object();
    static Object o2 = new Object();


    @Override
    public void run() {

        if (flag) {
            synchronized (o1) {
                System.out.println(Thread.currentThread().getName() + "开始工作");
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                synchronized (o2) {
                    System.out.println("work is done");
                }

            }
        } else {
            synchronized (o2) {
                System.out.println(Thread.currentThread().getName() + "开始工作");
                try {
                    Thread.sleep(2000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                synchronized (o1) {
                    System.out.println("work is done");
                }

            }
        }
    }

    public static void main(String[] args) {

        //测试
        TestDeadLock r1 = new TestDeadLock();
        r1.setFlag(true);
        Thread t1 = new Thread(r1);
        t1.setName("线程1");

        TestDeadLock r2 = new TestDeadLock();
        r2.setFlag(false);
        Thread t2 = new Thread(r2);
        t2.setName("线程2");

        t1.start();
        t2.start();
    }
}
~~~~

避免死锁：尽可能将加锁的粒度加粗

- 解锁如下：

~~~java
//只需要修改run()方法
@Override
public void run() {

    if (flag) {
        synchronized (this) {
            System.out.println(Thread.currentThread().getName() + "开始工作");
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            //synchronized (o2) {
            System.out.println("work is done");
            //}

        }
    } else {
        synchronized (this) {
            System.out.println(Thread.currentThread().getName() + "开始工作");
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            //synchronized (o1) {
            System.out.println("work is done");
            //}

        }
    }
}
~~~

注意：1. 当一个线程进入了某个加锁的方法时，其他线程完全可以访问其他没有加锁的方法

~~~java
package com.iweb.Test2;

public class T implements Runnable {

    int i = 100;

    synchronized void m1() {
        this.i = 1000;
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    void m2() {
        System.out.println(i);
    }

    @Override
    public void run() {
        m1();
    }
}
~~~

~~~java
package com.iweb.Test2;

public class Test13 {
    public static void main(String[] args) {
        T t = new T();
        Thread thread = new Thread(t);
        thread.start();

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        t.m2();
    }
}
~~~

	2. 没有加锁的方法会对加锁的方法造成影响
	2. 各自加锁的方法在执行的过程中互斥

### Object类中线程相关的方法

- wait() ---- 使当前线程处于等待状态
- notify() ---- 唤醒当前对象上某个wait中的线程
- notifyAll() ---- 唤醒当前对象上所有wait中的线程

### wait和sleep的区别

1. sleep 是 Thread 类的静态本地方法，wait 则是 Object 类的本地方法
2. sleep会自动醒，wait如果没有指定毫秒数则需要notify唤醒
3. 某个线程在sleep的过程中不会释放线程锁，而在wait的过程中会释放线程锁
4. sleep 一般用于当前线程休眠，或者轮循暂停操作，wait 则多用于多线程之间的通信
5. sleep 会让出 CPU 执行时间且强制上下文切换，而 wait 则不一定，wait 后可能还是有机会重新竞争到锁继续执行的。

### 多线程经典例题：生产消费

~~~java
/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-22/0022
 * 描述：消费者
 */

public class Customer implements Runnable {
    MantouStack mantouStack;

    public Customer() {
    }

    public Customer(MantouStack mantouStack) {
        this.mantouStack = mantouStack;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {//没买到20个都要继续买
            Mantou mt = mantouStack.pop();//从框中取走一个
            try {
                Thread.sleep((long) (Math.random() * 1000)); //休息个[0,1)秒再接着买
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

~~~

~~~java
package com.iweb.test3;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-22/0022
 * 描述：生产者
 */

public class Producer implements Runnable {
    MantouStack mantouStack = new MantouStack();

    public Producer() {
    }

    public Producer(MantouStack mantouStack) {
        this.mantouStack = mantouStack;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {//生产完二十个馒头下班回家
            Mantou mt = new Mantou(i);
            mantouStack.push(mt);//馒头放进框内

            //捏累了休息一会
            try {
                Thread.sleep((long) (Math.random() * 1000));//[0,1)随机秒数
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
    }
}

~~~

~~~java
package com.iweb.test3;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-22/0022
 * 描述：馒头类
 */

public class Mantou {
    int id;

    public Mantou() {
    }

    public Mantou(int id) {
        this.id = id;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    @Override
    public String toString() {
        return "馒头编号：" + id;
    }
}

~~~

~~~java
package com.iweb.test3;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-22/0022
 * 描述：馒头框
 */

public class MantouStack {

    Mantou[] mantous = new Mantou[6];//馒头框里最多放六个馒头
    int countOfMantou = 0;//当前框里的馒头数


    //放入馒头
    public synchronized void push(Mantou mantou) {
        while (mantous.length == countOfMantou) {//框里馒头满了
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        //框里空出来了
        notify();
        mantous[countOfMantou] = mantou;
        countOfMantou++;
        System.out.println("放进来一个馒头 " + mantou);
    }

    //取出馒头
    public synchronized Mantou pop() {
        while (countOfMantou == 0) {//框里没馒头了
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        //有馒头了
        notify();
        countOfMantou--;
        System.out.println("取走了 " + mantous[countOfMantou]);
        return mantous[countOfMantou];
    }

}
~~~

~~~java
package com.iweb.test3;

/**
 * @Author HearWardrum
 * 联系方式：tianxiayifan@qq.com
 * @Date 2022-08-22/0022
 * 描述：测试类
 */

public class Test {


    public static void main(String[] args) {
        MantouStack mantouStack = new MantouStack();//得使用同一个馒头框
        Producer p = new Producer(mantouStack);
        Customer c = new Customer(mantouStack);
        Thread producerThread = new Thread(p);
        Thread customerThread = new Thread(c);

        producerThread.start();
        customerThread.start();
    }
}
~~~

改写生产者消费者的代码:
两个师傅各生产20个馒头 : 张师傅,李师傅
四个学生各消费10个馒头 : 小明,小王,小强,小红

~~~~java
//馒头类
public class ManTou {
    private int id;
    static int sid = 1;

    public ManTou() {
        this.id = sid++;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    @Override
    public String toString() {
        return "ManTou{" +
                "id=" + id +
                '}';
    }
}
~~~~



~~~java
//馒头框类
public class ManTouStack {
    ManTou[] arr = new ManTou[6];//创建一个可以存放6个馒头的数组
    int index = 0;//表示当前框中的馒头数

    //生产
    synchronized void push(String ProducerName) {//传入生产者的名字
        while (arr.length == index) {//如果馒头框满了，线程等待
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        notify();
        ManTou mt = new ManTou();
        arr[index] = mt;
        index++;
        System.out.println(ProducerName + "生产了馒头：" + mt);
    }


    //消费
    synchronized ManTou pop(String ConsumerName) {

        while (index == 0) {
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        notify();
        index--;
        System.out.println(ConsumerName + "消费了馒头：" + arr[index]);
        return arr[index];
    }
}
~~~

~~~~java
//生产者类
public class Producer implements Runnable {

    ManTouStack manTouStack;
    String name;

    public Producer(ManTouStack manTouStack, String name) {
        this.manTouStack = manTouStack;
        this.name = name;
    }

    public Producer() {
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            //ManTou mt = new ManTou();
            //manTouStack.push( mt,this.name);
            manTouStack.push(this.name);
            try {
                Thread.sleep((long) (Math.random() * 1000));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
    }
}
~~~~

~~~~java
//消费者类
public class Consumer implements Runnable {


    ManTouStack manTouStack;
    String name;

    public Consumer() {
    }

    public Consumer(ManTouStack manTouStack, String name) {
        this.manTouStack = manTouStack;
        this.name = name;
    }

    @Override
    public void run() {
        for (int i = 0; i <= 10; i++) {
            ManTou mt = manTouStack.pop(this.name);
            try {
                Thread.sleep((long) (Math.random() * 2000));
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
~~~~

~~~java
//测试类
public class Test {

    public static void main(String[] args) {
        ManTouStack mts = new ManTouStack();
        Producer p1 = new Producer(mts, "张师傅");
        Producer p2 = new Producer(mts, "李师傅");
        Consumer c1 = new Consumer(mts, "小明");
        Consumer c2 = new Consumer(mts, "小王");
        Consumer c3 = new Consumer(mts, "小强");
        Consumer c4 = new Consumer(mts, "小红");

        Thread thread1 = new Thread(p1);
        Thread thread2 = new Thread(p2);
        Thread thread3 = new Thread(c1);
        Thread thread4 = new Thread(c2);
        Thread thread5 = new Thread(c3);
        Thread thread6 = new Thread(c4);

        thread1.start();
        thread2.start();
        thread3.start();
        thread4.start();
        thread5.start();
        thread6.start();
    }
}
~~~

## 第六天

### 集合

- 结构图：

![](https://cdn.jsdelivr.net/gh/HeartWardrum/MyImageHost/集合结构图.png)

![](D:\GitHub\MyImageHost\集合结构图.png)

- ArrayList ---- 这是一个常用的集合类，它实现了List接口

  - 常用方法：

    > `add(对象) ---- 往集合中添加一个对象`
    >
    > `get(下标) ---- 获取集合中指定位置的对象，注意：下标从0开始`
    >
    > `size() ---- 获取集合的长度`
    >
    > `remove() ---- 从当前集合中删除与指定对象相等的对象，注意：是否相等看的是equals方法`
    >
    > `contains(对象) ---- 判断当前集合中是否包含指定的对象，注意：是否包含看的是equals方法`

~~~~java
//例如 
public static void main(String[] args) {
        List list = new ArrayList();
        list.add(new Student("1111","张三",20));
        list.add(new Student("2222","王五",20));
        list.add(new Student("3333","李四",20));
        list.add(1000);
        list.add(1.1);
        System.out.println("当前list长度为： " + list.size());
    
    	//使用简单for遍历
        for (int i = 0; i < list.size(); i++) { 
            System.out.println(list.get(i));
        }
        //使用foreach遍历
    	for(类型名 变量 : 集合名){
			使用变量
		}
    	for (Object o : list) {
            System.out.println(o);
         }

    	//在自己定义的Student类中重写equals方法后，可以删除一个Student类型的元素
    	list.remove(new Student("1111", "张三", 20));
    	//当我们传入int类型的时候,为了移除制定的元素而不至于引起混淆，可以将传入的int先封装一下
        list.remove((Integer)1000);//不封装的话则默认删除下标为1000的元素
    }
~~~~

- 注意：ArrayList 、Vector 和 LinkedList 都是实现了List接口的实现类，他们所提供的方法都是一样的

  - 区别: 

    > ArrayList 和 LinkedList 线程不同步，效率高；Vector 线程同步，效率低
    >
    > ArrayList 底层是数组，擅长查询；LinkedList 底层是链表，擅长插入和删除

    

### 迭代器 Iterator

> 同来遍历一个集合，
>
> 我们使用  集合对象.iterator()  获取迭代器
>
> 使用迭代器的 hasNext() 方法判断是否遍历到集合末尾
>
> 使用迭代器的remove()删除集合中的每一个元素  
>
> 注意：在迭代的过程中不可以使用集合对象的remove()删除元素

~~~java
//foreach的底层   迭代器
Iterator iterator = list.iterator();//获取迭代器
while(iterator.hasNext()){
	System.out.println(iterator.next());
}

//迭代器中删除元素
Iterator iterator = list.iterator();
while(iterator.hasNext()){
	iterator.remove();
}
~~~

















# 问题

```
public ManTou() {
    synchronized (sid){
        this.id = id;
    }
    
}//没看到，估计写得不对，在上午第二节课开始处

```
