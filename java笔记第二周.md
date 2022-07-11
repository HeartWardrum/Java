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