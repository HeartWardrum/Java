#### 使用"流"获得列表中大于5的数

~~~java
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(1, 7, 3, 8, 2, 4, 9);
        List<Integer> result = getGt5Data(list);
        System.out.println(result);

    }

    /**
     * 使用流 来获得列表中大于5的数
     * @param list
     * @return
     */
    public static List<Integer> getGt5Data(List<Integer> list){
        return list.stream().filter(num -> num > 5).collect(toList());
    }
~~~

### Stream简介

#### 特点

- 元素的序列：与集合一样可以访问里面的元素，集合讲的是数据，而流讲的是操作。比如：filter、map；
- 源：流也需要有一个提供数据的源，顺序和生成时的顺序一致；
- 数据的操作：流支持类似于数据库的操作，支持顺序或者并行处理数据；
- 流水线操作：很多流的方法本身也会返回一个流，这样可以把多个操作连接起来，形成流水线操作。
- 内部迭代：与以往的迭代不同，流使用的内部迭代，用户只需要专注于数据处理；
- 只能遍历一次：遍历完成之后我们的流就已经消费完了，再次遍历的话会抛出异常；

### 使用Stream

使用一个流一般需要三个操作：

1. 定义一个数据源
2. 定义一个中间操作形成流水线
3. 定义终端操作，执行流水线，生成计算结果

#### 构建流

1、使用`Stream.of()`方法构建一个流

~~~java
Stream.of("hello","world",1212).forEach(System.out::println);
~~~

### 中间操作

#### filter

该操作接收一个返回boolean的，当返回false的元素将会被排除掉。

~~~java
        List<Integer> list = Arrays.asList(1, 7, 3, 8, 2, 4, 9);
        List<Integer> result = list.stream().filter(num -> num > 4).collect(toList());
        result.stream().forEach(System.out::print);
~~~

#### distinct

该操作将会排除掉重复的元素

~~~java
        List<Integer> data = Stream.of(1, 7, 3, 8, 2, 4, 9, 7, 9)
                .distinct().collect(toList());
        data.stream().forEach(i -> {
            System.out.print(i + ",");
        });
~~~

#### limit

该方法限制流只返回指定个数的元素

~~~java
         Stream.of(1, 7, 3, 8, 2, 4, 9, 7, 9)
                .distinct()
                 .limit(2)
                 .collect(toList())
                 .forEach(i ->{
                     System.out.print(i + " ");
                 });
~~~

#### skip

扔掉前指定个数的元素；配合limit使用可以达到翻页的效果

~~~java
         Stream.of(1, 7, 3, 8, 2, 4, 9, 7, 9)
                .distinct()
                 .skip(1)
                 .limit(2)
                 .collect(toList())
                 .forEach(i ->{
                     System.out.print(i + " ");
                 });
~~~

#### map

该方法提供一个函数，流中的每个元素都会应用到这个函数上，返回的结果将形成新类型的流继续后续操作。

~~~java
import lombok.Data;

@Data
public class Customer {

    private String name;
    private Integer age;

    public Customer(String name, Integer age) {
        this.name = name;
        this.age = age;
    }

    public Customer() {
    }
}

~~~

~~~java
    public static void main(String[] args) {
       Customer c1 = new Customer("张三",10);
       Customer c2 = new Customer("里斯",12);
       Customer c3 = new Customer("王武",13);

       List<Customer> customers = Stream.of(c1,c2,c3).collect(toList());
       customers.stream()
               .filter(customer -> customer.getAge() > 11)
               .map(customer -> customer.getName())
               .forEach(System.out::println);

    }
~~~

在调用map之前流的类型是`Stream<Customer>`,执行完map之后的类型是`Stream<String>`

#### flatMap

假如我们需要把客户的名字中的每个字符打印出来，代码如下：

~~~java
List<Customer> allCustomers = Arrays.asList(new Customer("silently9527", 30));
allCustomers.stream()
        .filter(customer -> customer.getAge() > 20)
        .map(customer -> customer.getName().split(""))
        .forEach(System.out::println);
~~~

执行本次结果，你会发现没有达到期望的结果，打印的结果为：

~~~java
[Ljava.lang.String;@38cccef
~~~

这是因为调用map之后返回的流类型是`Stream<String[]>`,所有forEach的输入就是`String[]`，这时我们需要使用flatMap把`String[]`中的每个元素都转换成一个流，然后把所有的流连接成一个流，修改后的代码如下：

~~~java
List<Customer> allCustomers = Arrays.asList(new Customer("silently9527", 30));
allCustomers.stream()
        .filter(customer -> customer.getAge() > 20)
        .map(customer -> customer.getName().split(""))
        .flatMap(Arrays::stream)
        .forEach(System.out::println);
~~~

#### sorted

对所有元素进行排序

~~~java
        List<Integer> list = Arrays.asList(1, 7, 3, 8, 2, 4, 9);
        list.stream().sorted().forEach(i -> {
            System.out.print(i + " ");
        });
~~~

#### anyMatch

如果流中有一个元素满足条件将返回true

~~~java
        Customer c1 = new Customer("张三", 10);
        Customer c2 = new Customer("里斯", 12);
        Customer c3 = new Customer("王武", 13);

        List<Customer> customers = Stream.of(c1, c2, c3).collect(toList());
        String name = "张三2";
        if (customers.stream().anyMatch(customer -> name.equals(customer.getName()))) {
            System.out.println("存在客户:" + name);
        } else {
            System.out.println("不存在客户:" + name);
        }
~~~

#### anyMatch

确保流中所有的元素都能满足

~~~java
        Customer c1 = new Customer("张三", 10);
        Customer c2 = new Customer("里斯", 12);
        Customer c3 = new Customer("王武", 13);

        List<Customer> customers = Stream.of(c1, c2, c3).collect(toList());
        Integer age = 10;
        if (customers.stream().allMatch(customer -> customer.getAge() > age)) {
            System.out.println("客户年龄都大于" + age + "岁");
        } else {
            System.out.println("客户年龄不全大于" + age + "岁");
        }
~~~

#### noneMatch

与allMatch操作相反，确保流中所有的元素都不满足

#### findAny

返回流中任意一个元素，比如返回大于20岁的任意一个客户

~~~java
        Optional<Customer> optional = customers.stream()
                .filter(customer -> customer.getAge() > 20)
                .findAny();

        try {
            System.out.println(optional.get());
        } catch (NoSuchElementException e) {
            System.out.println("没找到");
            System.err.println("错误信息：" + e);
        }
~~~

#### findFirst

返回流中的第一个元素

~~~java
        Optional<Customer> optional = customers.stream()
                .filter(customer -> customer.getAge() > 10)
                .findFirst();
~~~

#### reduce

接收两个参数：一个初始值，一个`BinaryOperator<T> accumulator`将两个元素合并成一个新的值，比如我们对一个数字list累加。

