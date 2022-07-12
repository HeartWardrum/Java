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

 - 完全二叉树：在满二叉树上，最下层从最右侧起，去掉若干相邻的子节点得到的二叉树

   

二叉树的特性：度为2的节点数量 +  = 终端节点的数量

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



