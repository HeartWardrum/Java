---
title:  笔记_002_java
tag: 
	- java
categories: 
	- java
---

## 第七天

### Set

Set和List都是Collection接口下的子接口，区别：

- List是有序的，可重复的
- Set是无序的，不可重复的
- 对于Set来讲没有get方法，因为它没有下标的概念；而对于List来讲，正因为它有下标的概念，所以它可以使用add(下标，对象)来将对象插入到指定位置

Set常用方法：

> `add(对象) ---- 添加对象`
>
> 

~~~java
Set set = new HashSet();
set.add(100);
set.add("hello");
set.add(new Student("1001","张三",20));
~~~

### Map

存放的是键值对，通过每一个键可以得到每一个值

>put(key,value) ---- 存入键值对
>
>get(key) ---- 根据键得到值
>
>containsKey(key) ---- 判断当前Map中是否包含指定的键
>
>containsValue(value) ---- 判断当前Map中是否包含指定的值

注意：对于Map来讲键值对的键不可重复，如果重复，则后加入的键值对会将先加入的键值对覆盖

~~~java
Map map = new HashMap();
map.put("one", new Integer(100));
map.put("two",new String("hello"));
map.put(null,new Integer(200));
~~~

遍历map

~~~java
for (Map.Entry<Character, Integer> entry: map.entrySet()) {
                System.out.println("\""+entry.getKey()+"\""+"的数量是:"+entry.getValue());
            }
~~~



HashMap和HashTable的区别：

- HashMap线程不同步，效率高；HashTable线程同步，效率低
- HashMap可以使用null作为键 HashTable不可以

### Collections

这是一个帮助类，帮助我们对Collection集合中的元素进行各种处理，例如`Collections.sort()`可以实现对List进行各种排序

### Arrays.sort()

可以对一个数组进行升序排序

### 泛型

在定义集合的时候使用<>同时来定义集合中的对象类型，它可以增强程序的可读性和稳定性

Map中的键、值都可以使用泛型来定义

~~~~java
List<String> list = new ArrayList<>();
Map<String,Integer> map = new HashMap<>();
~~~~

~~~~java
List<Map<String,Object>> list = new ArrayList<>();

for (int i = 0; i < 3; i++) {
     Map<String, Object> m1 = new HashMap<>();
     for (int j = 0; j < 5; j++) {
         m1.put("key" + i + j, "value" + i + j);

     }
            list.add(m1);
}
for (Map<String, Object> stringObjectMap : list) {
     System.out.println(stringObjectMap);
}
~~~~

我们可以使用List<Map<String,Object>>类型来整合一组数据库中的数据

### 泛型类

`Class 类名<泛型标识>{}`

使用泛型类定义对象：`类名<泛型> 变量名 = new 类名<>();`

注意：

- 如果定义对象的时候不使用泛型，那么它的泛型就是Object型
- 某个泛型类下的多个对象，当他们的泛型不同时，他们的类型依然是相同的

### Random

随机数   我们可以使用`该对象.nextXxx(上限值)`返回上限值以内的随机数

简单抽奖：

~~~~java
public class ProductGetter<T> {
    //奖品
    private T product;

    //抽奖池
    List<T> productList = new ArrayList<>();

    static Random random = new Random();

    //往奖池中投放若干奖品
    void putProduct(T product) {
        productList.add(product);
    }
    
    //从奖池中随机抽一个奖品
    T getProduct() {
        return productList.get(random.nextInt(productList.size()));
    }

}
~~~~

~~~java
public class Test {

    public static void main(String[] args) {
        //抽实物
        String[] arr = new String[]{"苹果", "华为", "扫帚", "咖啡机"};
        ProductGetter<String> productGetter = new ProductGetter<>();
        for (String s : arr) {
            productGetter.putProduct(s);

        }
        String product = productGetter.getProduct();
        System.out.println(product);

		//抽现金
        int[] arr2 = new int[]{1000, 2000, 3000, 4000};
        ProductGetter<Integer> productGetter1 = new ProductGetter<>();
        for (int i : arr2) {
            productGetter1.putProduct(i);

        }
        int product2 = productGetter1.getProduct();
        System.out.println(product2);

    }

}

~~~

### 泛型中的继承

1. 当父类是泛型类时，如果子类也是泛型类，则定义子类时，它的泛型标识必须和父类一致

~~~java
//父类
public class Parent<T> {
    T value;

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }

    public Parent(T value) {
        this.value = value;
    }

    public Parent() {
    }
}
~~~

~~~java
//子类1
public class Child<E> extends Parent<E> {

    @Override
    public E getValue() {
        return super.getValue();
    }

    @Override
    public void setValue(E value) {
        super.setValue(value);
    }
}
~~~

2. 当父类是泛型类时，如果子类不是泛型类，需要指明父类的泛型类型

~~~java
//子类2
public class Child2 extends Parent {

    @Override
    public Object getValue() {
        return super.getValue();
    }

    @Override
    public void setValue(Object value) {
        super.setValue(value);
    }
}
~~~

~~~java
    //测试类
public static void main(String[] args) {
        Child<String> child = new Child<>();
        child.setValue("abc");
        System.out.println(child.getValue());

        Child2 child2 = new Child2();
        child2.setValue("hello");
        System.out.println(child2.getValue());
        
    }
~~~

### 泛型接口

1. 当接口是泛型接口时，如果实现类也是泛型类，则定义实现类时，它的泛型标识必须和接口一致

~~~java
public interface GenericInterface<T> {
    T getValue(T t);
}
~~~

~~~java
public class MyImplement<T> implements GenericInterface<T> {
    @Override
    public T getValue(T t) {
        return t;
    }
}
~~~

2. 当接口是泛型接口时，如果实现类不是泛型类，则定义实现类时，需要指明接口的泛型类型

### 泛型方法

我们在方法声明的地方添加 <泛型标识> ,这样的方法称为泛型方法，它可以在用户调用方法的时候来指明具体的泛型

注意：如果方法是静态的，我们可以定义多个泛型

~~~java
static <T, E, K> void test1(T t, E e, K k){
        System.out.println(t.getClass());
        System.out.println(e.getClass());
        System.out.println(k.getClass());
    }
~~~

~~~java
ProductGetter.test1(false,10,"hello");
//打印结果
class java.lang.Boolean
class java.lang.Integer
class java.lang.String
~~~

### 可变参数的泛型方法

在定义泛型方法的时候，参数列表使用`泛型标识...变量`来表示可变参数

实际接收到的参数是一个泛型参数的数组

~~~java
static <T> void test2(T...t){
        System.out.println("参数数组的个数： " + t.length);
        for (int i = 0; i < t.length; i++) {
            System.out.print(t[i] + "   ");
        }
    }
~~~

~~~java
productGetter.test2(1,2,3,4,5);
//打印结果
参数数组的个数： 5
1   2   3   4   5
~~~

### 泛型中的通配符 

`?` 在泛型中表示通配符，它可以修饰某个类型的变量，该变量可以接收任何泛型的该类对象

~~~java
List<?> list1 = new ArrayList<>();
List<String> list2 = new ArrayList<>();
list1 = list2;
~~~

~~~java
Map<?,?> map1 = new HashMap<>();
Map<String,Integer> map2 = new HashMap<>();
map1 = map2;
~~~

### Arrays.copyOf(旧数组，新数组的长度) 

创建一个新数组，然后将旧数组拷贝到新数组中，返回新数组的引用

## 第八天

### Vector 集合对象如何扩容

在我们创建Vector对象的时候，可以指定初始容量和扩容容量，每次就按照自己指定的扩容容量来扩容，如果没有指定扩容容量，则每次扩容时容量翻倍

### LinkedList

单链表 ---- 每个节点存放数据的同时，还存放下一个节点的地址

双向链表 ---- 每个节点存放数据的同时，还存放上一个节点和下一个节点的地址

JDK中的LinkedList是一个双向链表

### 栈

- 先进后出，后进先出
- 在java当中，我们使用Deque接口，只对其一端进行操作，来表示栈

~~~java
//十进制转2进制
public static void main(String[] args) {

        int t = 255;

        Deque deque = new LinkedList();
        do {
            int mod = t % 2;
            deque.push(mod);
            t /= 2;
        } while (t > 0);
        while (!deque.isEmpty()) {
            System.out.print(deque.poll());
        }


    }
}
~~~



### 队列

- 先进先出，后进后出
- 在java中，有两个接口：
   - Queue ---- 队列
     - `add() ---- 入队`
     - `poll() ---- 出队`
     - `peek() ---- 获取队首元素`
   - Deque ---- 双端队列 ：两端都可以入队出队
     - `addFirst() ---- 从队首入队`
     - `addLast() ---- 从队尾入队`
     - `pollFisrt() ---- 从队首出队`
     - `pollLast() ---- 从队尾出队`
     - `peekFirst() ---- 获取队首元素`
     - `peekLast() ---- 获取队尾元素`

注意：java中通常使用LinkedList来实现栈和队列

### 树

树是一个集合以及在该集合上定义的一种关系结构

- 节点的度 ---- 节点拥有的子树的数目就是节点的度
- 树的度 ---- 各个节点最大的度，就是树的度

有序树：如果将树中的节点各个子树看成从左至右是有序的，就称为有序树，否则就是无序树

m叉树：一棵树的任一节点往下，最多分几个叉就是几叉树

二叉树：每个节点的度均不超过2的有序树

 - 满二叉树 ：除了叶子节点，每个层的节点都达到最大数

 - 完全二叉树：在满二叉树基础上，最下层从最右侧起，去掉若干相邻的子节点得到的二叉树

   

二叉树的特性：度为2的节点数量 + 1 = 终端节点的数量

注意：在java中数组和链表都可以表达二叉树，但是数组并不好0用，我们常常使用链表来表达二叉树

### 二叉树的遍历

按照某种访问的次序对二叉树中的所有节点依次访问，而且每个节点恰好访问一次

二叉树的遍历方式：

- 先序： 根   左子树  右子树
- 中序：左子树  根   右子树
- 后序： 左子树  右子树   根

面试题：
中序：4513267
后序：5437621
求先序

1. 先看后序的最后一个数就是根 此处为 1

2. 看中序，分出根的左右子树

3. 看后序，54的顺序决定了4是左子树的根
    到此为止：先序：145...

  注意：由中序可知4在前5在后，所以5是4的右孩子

4. 看后序，2是右子树的根

  到此为止：先序：1452...

5. 看中序，3是2的左孩子，67是2的右孩子

  到此为止：先序：14523...

6. 再看2的右子树，由后序可知，76的顺序是7在前，6在后，那么6就是7的父亲，所以6就是2的右子树的根

  到此为止：先序：1452367

7. 最后由中序可知7是6的右孩子

### 简单递归

~~~java
static int dg(int i) {
int sum = 0;
if (i == 1)
    return 1;
else
    sum = i + dg(i - 1);
return sum;
}
~~~

## 第十天

###  IO流

- 按照传输的方向来分:

  > 输入流：数据流向了CPU，所以读文件是输入流
  >
  > 输出流：数据从CPU流出去，所以写文件是输出流
  >
  > 注意：输入和输出的方向问题，永远都是站在CPU的角度来看待的

- 按照传输的最小单位分：

  > 字节流 ---- 按照字节为单位进行传输
  >
  > 字符流 ---- 按照字符为单位进行传输

- 按功能的强弱分：
  
  > 节点流 ---- 基本功能的数据流，数据往往按照最小单位传输
  >
  > 处理流 ---- 功能强大的一些数据流，数据往往是批量传输

在Java中，所有的流都继承自以下4个抽象类：

`InputStream ---- 字节输入流`

`OutputStream ---- 字节输出流`

`Reader ---- 字符输入流`

`Writer ---- 字符输出流`

### FileInputStream 

文件输入流，用来读文件；当我们new一个FileInputStream对象时，需要传入文件路径，换句话说相当于一根管道怼到了该文件上，这根管道可以用来从文件中抽水

`read() ---- 抽一个字节出来返回给CPU 返回值是一个unicode编码 类型为int`

`close() ---- 关闭该输入流`

Windows的文件分割符默认为反斜杠，Linux是正斜杠；Java中的`File.separator() `返回的是当前操作系统的文件分隔符

在实际开发中，我们其实只需要写正斜杆，因为Windows会智能地将其转为反斜杠

~~~java
  public static void main(String[] args) {
        InputStream is = null;
        //String path = File.separator;
        try {
            is = new FileInputStream("D:/GitHub/Java/算法.md");
            int i = 0;
            while ((i = is.read()) != -1) {
                System.out.print((char) i); //将i转成char型 不然打印结果为一堆数字
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (is != null)// 提高代码健壮性 如果路径失效 压根没开启is 就不用close
                    is.close();//相当于截断管道
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
//打印结果中的中文字会变成乱码
~~~

注意：字节流每读取一个中文字，实际上是读取到中文字的一半的编码，所以不能直接打印，我们可以使用字符流来读取并打印

### FileReader

文件字符输入流，用来读文件；当我们new一个FileReader对象时，需要传入文件路径，换句话说相当于一根管道怼到了该文件上，这根管道可以用来从文件中抽水

~~~java
public static void main(String[] args) {
        Reader is = null;
        //String path = File.separator;
        try {
            is = new FileReader("D:/java/MyProject/Test20220708/src/com/iweb/test/Test.java");
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
                if (is != null)// 提高代码健壮性 如果路径失效 就不用close
                    is.close();//相当于截断管道
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
~~~

### FileOutputStream

文件字节输出流，用来写文件；当我们new一个FileOutputStream对象时，需要传入文件路径，如果路径不存在，则会自动创建。换句话说相当于一根管道怼到了该文件上，这根管道可以用来向文件中注水

`write(int) ---- 将一个字节通过该字节流输出到文件中`

`close() ---- 关闭该输入流`

~~~java
public static void main(String[] args) {
        InputStream is = null;
        OutputStream os = null;
        //String path = File.separator;
        try {
            is = new FileInputStream("D:/java/MyProject/Test20220708/src/com/iweb/test/Test.java");
            os = new FileOutputStream("D:/Desktop/hello.txt");
            int i = 0;
            while ((i = is.read()) != -1) {
                os.write(i);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (is != null)// 提高代码健壮性 如果路径失效 就不用close
                    is.close();//相当于截断管道
                if (os != null)
                    os.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
~~~

### FileWriter

文件字符输出流，用来写文件；当我们new一个FileWriter对象时，需要传入文件路径，如果路径不存在，则会自动创建。换句话说相当于一根管道怼到了该文件上，这根管道可以用来向文件中注水

`write(int) ---- 将一个字节通过该字节流输出到文件中`

`close() ---- 关闭该输入流`

注意：构造方法的第二个参数

- 是true表示追加
- 是false表示覆盖

~~~java
public static void main(String[] args) {
        Writer w = null;
        try {
            w = new FileWriter("D:/Desktop/hello.txt");// FileWriter(路径,Boolean boolean)
            for (int i = 0; i < 50000; i++) {
                w.write(i);
            }
            System.out.println("创建完毕");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (w != null) {
                try {
                    w.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
~~~

### BufferedInputStream和BufferedOutputStream

字节输入/输出缓冲流

他们的read方法和write方法会一次性从硬盘读取/写入8k个字节到缓存，然后针对缓存进行操作；当缓存用完之后才会再访问硬盘，减少了硬盘的访问次数

他们都是处理流

注意：处理流是包在节点流外面的，当处理流关闭时，节点流自动关闭

~~~java
public static void main(String[] args) {
        InputStream is = null;
        BufferedInputStream bis = null;
        try {
            is = new FileInputStream("D:/java/MyProject/Test20220708/src/com/iweb/test/Test.java");
            bis = new BufferedInputStream(is);
            int i = 0;
            while ((i = bis.read()) != -1) {
                System.out.print((char) i);
            }
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (bis != null)// 提高代码健壮性 如果路径失效 就不用close
                    bis.close();//相当于截断管道
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
~~~

### BufferedReader

字符输入缓冲流，它可以读文件

`readLine() ---- 每次从文件中读一行，返回该字符串`

`close() ---- 关闭该缓冲流`

### BufferedWriter

字符输出缓冲流，它可以写文件

`write(String s) ---- 写入一个字符串`

`newLine() ---- 另起一行`

`flush() ---- 清空缓冲区`

`close() ---- 关闭该输出流`

~~~java
public static void main(String[] args) {
        BufferedReader br = null;
        BufferedWriter bw = null;
        try {
            bw = new BufferedWriter(new FileWriter("D:/Desktop/random.txt"));
            br = new BufferedReader(new FileReader("D:/Desktop/random.txt"));
            for (int i = 0; i < 100; i++) {
                String s = String.valueOf(Math.random());
                bw.write(s);
                bw.newLine();//另起一行
            }
            bw.flush();//清空缓冲区
            String s1 = "";
            while ((s1 = br.readLine()) != null) {
                System.out.println(s1);
            }

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
~~~

### PrintWriter

打印流

用来打印日志，它只有输出，没有输入，不会抛出异常

提供各种重载的print()方法和println()方法用来打印

它自带缓冲功能，具有flush()方法

### InputStreamReader

这是将字节流转字符流的桥梁，传入一个字节流，它返回一个字符流

注意：该字符流是一个节点流

~~~java
public static void main(String[] args) {
        String s = null;
        PrintWriter pw = null;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        try {
            FileWriter fw = new FileWriter("D:/Desktop/log.txt", true);
            pw = new PrintWriter(fw);
            while ((s = br.readLine()) != null) {
                if ("exit".equals(s)) {
                    break;
                }
                System.out.println(s);
                pw.println("--------");
                pw.println(s);
            }
            pw.println("======" + new Date() + "======");
            pw.flush();

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (pw != null)
                    pw.close();
                if (br != null)
                    br.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
~~~

### DataInputStream 和 DataOutputStream

数据流，往往用于网络上的数据传输，它们的readUTF()方法和writeUTF()方法可以实现UTF-8的编码格式来传输数据

UTF-8 ---- 可变长度的Unicode编码格式

### ServerSocket

这是网络编程中的服务器类，它可以调用accept()方法来接收某个客户端向它发起是请求，并返回Socket对象

### Socket

这是网络编程中的客户端类，它可以向服务器发起请求，该类对象可以调用getInputStream()和getOutputStream()获取当前请求响应的数据流中的字节流对象

### 简单服务器

~~~java
//服务器端
public class TcpServer {

    public static void main(String[] args) {
        System.out.println("我是服务器，我开始启动了");
        ServerSocket ss = null;
        Socket s = null;
        DataInputStream dis = null;
        DataOutputStream dos = null;
        try {
            ss = new ServerSocket(9527);
            while (true) {
                s = ss.accept();
                InputStream is = s.getInputStream();
                dis = new DataInputStream(is);
                String str = dis.readUTF();
                System.out.println(str);
                dos = new DataOutputStream(s.getOutputStream());
                dos.writeUTF("Hello I am Server!");
                dos.flush();


            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (s != null)
                    s.close();
                if (dis != null)
                    dis.close();
                if (dos != null)
                    dos.close();
                if (ss != null)
                    ss.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

~~~

~~~java
//客户端
public class TcpClient {
    public static void main(String[] args) {
        System.out.println("我是客户端，我即将向服务器发起请求");
        Socket s = null;
        DataOutputStream dos = null;
        DataInputStream dis = null;
        try {
            s = new Socket("127.0.0.1", 9527);
            dos = new DataOutputStream(s.getOutputStream());
            dos.writeUTF("Hello,I am Client!");
            dis = new DataInputStream(s.getInputStream());
            System.out.println(dis.readUTF());

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (dos != null)
                    dos.close();
                if (dis != null) {
                    dis.close();
                }
                if (s != null)
                    s.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
~~~

### 设计模式

#### 单例Singleton

一个类只能创建出一个对象

- 饿汉模式：
  1. 构造方法私有化
  2. 提供`static finally 当前类型的成员变量`，初始化为当前类的对象
  3. 提供一个public static 返回当前类型的方法，用来返回该唯一对象

~~~java
//单例类  饿汉模式
public class Singleton1 {

    static final Singleton1 only = new Singleton1();

    private Singleton1() {

    }

    public static Singleton1 getSingleton1() {
        return only;
    }
}
~~~

~~~java
//测试类
public class Test {
    public static void main(String[] args) {
        Singleton1 s1  = Singleton1.getSingleton1();

    }
}
~~~

- 懒汉模式：

  1. 构造方法私有化
  2. 提供 `static  当前类型的成员变量`
  3. 提供一个`public static` 返回当前类型的方法，判断成员变量是否为空，如果为空则创建唯一对象，返回该唯一对象

  注意： 懒汉模式需要做线程同步

~~~java
public class Singleton2 {

    static Singleton2 only;

    private Singleton2() {

    }

    public synchronized static Singleton2 getSingleton1() {
        if (only == null)
            only = new Singleton2();
        return only; 
    }
}
~~~

#### 工厂模式

提供一个工厂类，将创建的对象的工作封装起来，提供公共的静态的工厂方法给访问者调用，返回它所需要的对象

- 静态工厂模式：创建对象以及封装对象的过程放在静态代码块中，用户无需创建工厂，而可以直接调用静态的工厂方法获得产品对象

~~~java
public class Car {
    private String cno;
    private String brand;
    private double price;

    @Override
    public String toString() {
        return "Car{" +
                "cno='" + cno + '\'' +
                ", brand='" + brand + '\'' +
                ", price=" + price +
                '}';
    }

    public Car(String cno, String brand, double price) {
        this.cno = cno;
        this.brand = brand;
        this.price = price;
    }

    public Car() {
    }


    public String getCno() {
        return cno;
    }

    public void setCno(String cno) {
        this.cno = cno;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }
}
~~~

~~~java
public class CarFactory {


    private static Map<String, Car> map = new HashMap<>();

    static {
        map.put("1001", new Car("1001", "Audi", 300000.0));
        map.put("1002", new Car("1002", "Ford", 150000.0));
        map.put("1003", new Car("1003", "Volvo", 200000.0));

    }

    public static Car getCar(String id) {
        return map.get(id);
    }
}
~~~

~~~java
public class Test2 {

    public static void main(String[] args) {
        Car car = CarFactory.getCar("1002");
        System.out.println(car);
    }
}
~~~

- 实例工厂模式：创建对象以及封装对象的过程放在工厂类的构造方法中，用户首先需要创建工厂对象，然后通过工厂对象调用工厂方法

~~~java
public class CarFactory2 {
    private static Map<String, Car> map;

    CarFactory2() {
        map = new HashMap<>();
        map.put("1001", new Car("1001", "Audi", 300000.0));
        map.put("1002", new Car("1002", "Ford", 150000.0));
        map.put("1003", new Car("1003", "Volvo", 200000.0));

    }

    public static Car getCar(String id) {
        return map.get(id);
    }
}
~~~

~~~java
public class Test3 {

    public static void main(String[] args) {
        CarFactory2 cf2 = new CarFactory2();
        Car car = cf2.getCar("1003");
        System.out.println(car);
    }
}
~~~

#### 代理模式

首先要有主题业务，在主题业务的周边还存在许多次要的业务，代理类就是负责处理主题业务的同时再去处理这些周边的业务

这样一来，主体类只需要专注于主体业务，降低了程序的耦合度

实际操作过程中，我们需要提供业务的接口，主体类和代理类同时实现该接口，代理类中包含主体类的对象，并在业务方法中调用主体方法，同时执行其他周边的业务操作

~~~java
public interface CarSale {

    public void sale();
}
~~~

~~~java
//主体类
public class CarFactory implements CarSale {


    private static Map<String, Car> map = new HashMap<>();

    static {
        map.put("1001", new Car("1001", "Audi", 300000.0));
        map.put("1002", new Car("1002", "Ford", 150000.0));
        map.put("1003", new Car("1003", "Volvo", 200000.0));

    }

    public static Car getCar(String id) {
        return map.get(id);
    }


    @Override
    public void sale() {
        System.out.println("工厂正在卖车");
    }
}
~~~

~~~java
//代理类
public class Car4s implements CarSale {
    CarFactory cf = new CarFactory();

    @Override
    public void sale() {
        System.out.println("办个车展");
        System.out.println("开展促销优惠活动");
        cf.sale();
        System.out.println("帮忙上保险");
        System.out.println("帮忙上牌照");
        System.out.println("提供售后服务");

    }
}
~~~

~~~java
 public static void main(String[] args) {
        CarSale cs = new Car4s();
        cs.sale();
    }
~~~

## 第十一天

### 反射

当某个类加载到内存中的静态代码区时，系统自动创建Class类的对象，这个对象称为反射对象，它就像一面镜子一样把当前类的所有成员变量及方法看的清清楚楚。它还可以创建当前类的对象，调用当前类的方法

获取Class对象的三种方式：

1. `类名.class`
2. `Class.forName("当前类的全类名")`
3. `对象名.getClass()`

~~~java
        System.out.println("获取Class对象的三种方式---------------------------");
        System.out.println("第一种：");
        Class c1= Person.class;
        System.out.println(c1);
        System.out.println("第二种：");
        Class<Person> c2 = null;
        try {
            c2 = (Class<Person>)Class.forName("com.iweb.test9.Person");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        System.out.println(c2);
        System.out.println("第三种:");
        Person p1 = new Person();
        Class c3 = p1.getClass();
        System.out.println(c3);
~~~

我们可以通过Class对象调用`getFields()`得到当前类中的public的成员变量，返回Field 数组

也可以调用`getDeclaredFields()`得到当前类中的所有成员变量，返回Field数组

注意：在反射看来，每一个成员变量其实都是Field对象

~~~java
        Field[] fields1 = c2.getFields();
        System.out.println("Person类中public方法数目为：" + fields1.length);
        for(Field field : fields1){
            System.out.println(field);
        }
        Field[] fields2 = c2.getDeclaredFields();
        System.out.println("Person类中所有方法数目为："  + fields2.length);
        for (Field field : fields2) {
            System.out.println(field);
        }
//打印结果
Person类中public方法数目为：1
public java.lang.String com.iweb.test9.Person.pno
Person类中所有方法数目为：3
public java.lang.String com.iweb.test9.Person.pno
private java.lang.String com.iweb.test9.Person.pname
private java.lang.String com.iweb.test9.Person.page
~~~

我们可以通过Class对象调用`getDeclaredMethods()`获取当前类中的所有方法，返回Method数组

我们可以通过Class对象调用`getDeclaredConstructor()`获取当前类中所有的构造方法，返回Constructor数组

注意：构造方法不属于传统意义的方法，只是名字类似

~~~java
System.out.println("----------------------------------------------");
Method[] methods = c2.getDeclaredMethods();
System.out.println(methods.length);
for (Method method : methods) {
	System.out.println(method);
}
System.out.println("----------------------------------------------");
Constructor[] constructors = c2.getDeclaredConstructors();
for (Constructor constructor : constructors) {
	System.out.println(constructor);
}
~~~

我们可以调用Class对象的`newInstance()`方法来获取当前类的对象，我们还可以调用Class对象的`getField("成员变量名")`获取某个public的成员变量的Field对象

我们通过Field调用set方法传入当前类对象和属性值来给成员变量赋值

~~~java
            Person p1 = c2.newInstance();
            Field f1 = c2.getField("pno");//获取当前类中指定的成员变量
            f1.set(p1, "1001");
            System.out.println(p1);
~~~

我们可以通过Class调用`getDeclaredConstructor()`传入参数的反射对象来得到Constructor对象，在由该类Constructor对象调用newInstance方法去执行有参构造方法来得到当前类的对象

~~~java
            Person p2 = null;
            Constructor<Person> c4 = c2.getDeclaredConstructor(String.class, String.class, String.class);
            p2 = c4.newInstance("1002", "Jerry", "20");
            System.out.println(p2);
~~~

对于非public的成员变量，我们可以通过Class对象调用getDeclaredField("变量名")得到Field对象，然后将Field调用setAccessible(true)进行授权

最后才可以调用set()方法进行赋值

~~~java
            Field f3 = c2.getDeclaredField("page");
            f3.setAccessible(true);
            f3.set(p1, "20");
            System.out.println(p1);
~~~

我们可以通过Class对象调用getDeclaredMethod("方法名")获取对应的Method对象，再由Method对象调用invoke(当前类对象)完成无参方法调用

~~~java
            Method m1 = c2.getDeclaredMethod("show");
            m1.invoke(p2);
~~~

我们可以通过Class对象调用getDeclaredMethod(方法名,参数类型的Class对象)获取对应的Metho的对象，再由Method对象调用Invoke(当前类对象,参数值)完成对有参方法的调用

~~~java
            Method m2 = c2.getDeclaredMethod("display", String.class);
            m2.invoke(p2,"中国");
~~~



### &和&&区别

区别在于 & 两边都运算，而 && 先算 && 左侧，若左侧为 false 那么右侧就不运算了。因此从效率上来说，判断语句中推荐使用 &&





























# 问题

