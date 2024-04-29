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

~~~

