## 1. List

~~~java
//List 接口
public interface List {

    public int size();//返回当前List的长度

    public Object get(int i);//返回指定下标处的元素

    public boolean isEmpty();//判断当前数组是否为空

    public void add(Object e);//将传入的元素e插入到当前List集合最后一个位置

    public void add(int i,Object e);//在指定下标位置插入指定元素
}
~~~

#### 下标越界异常

~~~java
public class MyIndexOutOfBoundsException extends RuntimeException {
    public MyIndexOutOfBoundsException() {
    }

    public MyIndexOutOfBoundsException(String message) {
        super(message);
    }
}
~~~

### 1. ArrayList

~~~java
//ArrayList  动态数组
public class ArrayList implements List {

    private Object[] elementData;//底层的数组
    private int size;//当前集合中的元素个数

    public ArrayList() {
        elementData = new Object[4];
        size = 0;
    }

    public ArrayList(int initialCapacity) {
        elementData = new Object[initialCapacity];
        size = 0;
    }


    @Override
    public int size() {
        return size;
    }

    @Override
    public Object get(int i) {
        if (i < 0 || i >= size) {
            throw new MyIndexOutOfBoundsException("对不起，下标越界了！越界下标为：" + i);
        }
        return elementData[i];
    }

    @Override
    public boolean isEmpty() {
        return size == 0;
    }

    @Override
    public void add(Object e) {

//        if (size == elementData.length) {
////            //扩容
////            //创建一个新数组，长度是旧数组的1.5倍
////            Object[] newArr = new Object[elementData.length + (elementData.length >> 1)];
////            //将旧数组拷贝到新数组
////            for (int i = 0; i < elementData.length; i++) {
////                newArr[i] = elementData[i];
////            }
////            //将旧数组的变量指向新数组
////            elementData = newArr;
//            grow();
//        }
//        elementData[size] = e;
//        size++;
        this.add(size, e);
    }


    @Override
    public void add(int i, Object e) {
        if (i < 0 || i > size) {
            throw new MyIndexOutOfBoundsException("对不起，下标越界了！越界下标为：" + i);
        }
        if (size == elementData.length) {
            grow();
        }
        //依次后移
        for (int j = size; j > i; j--) {
            elementData[j] = elementData[j - 1];
        }
        elementData[i] = e;
        size++;
    }


    //扩容
    public void grow() {
        elementData = Arrays.copyOf(elementData, elementData.length + (elementData.length >> 1));

    }

    @Override
    public String toString() {
        if (size == 0) {
            return "[]";
        } else {
            StringBuffer stringBuffer = new StringBuffer("[");
            for (int i = 0; i < size - 1; i++) {
                stringBuffer.append(elementData[i]).append(",");
            }
            stringBuffer.append(elementData[size - 1]).append("]");
//            for (int i = 0; i < size; i++) {
//                if (i != size - 1) {
//                    stringBuffer.append(elementData[i]).append(",");
//                } else {
//                    stringBuffer.append(elementData[i]).append("]");
//                }
//            }
            return stringBuffer.toString();
        }
    }
}
~~~

~~~java
//测试类
public class Test {

    public static void main(String[] args) {
        List list = new ArrayList();
        list.add(000);
        list.add(100);
        list.add(200);
        list.add(300);
        list.add(400);
        list.add(500);
        list.add(2, 999);
        System.out.println("动态数组长度:" + list.size());
        System.out.println("动态数组是否为空：" + list.isEmpty());
        System.out.println("遍历动态数组-------------------");
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i) + "  ");
        }
        System.out.println();
        System.out.println("测试toString方法-------------------");
        System.out.println(list);
    }
}
~~~



### 2. SingleLinkedList

~~~java
//单链表
public class SingleLinkedList implements List {


    Node head = new Node(); //头结点  里面不存数据
    int size; //一共多少个节点


    @Override
    public int size() {
        return size;
    }

    @Override
    public Object get(int i) {
        if (i < 0 || i > size) {
            throw new MyIndexOutOfBoundsException("对不起，下标越界了！");
        }
        Node p = head;
        for (int j = 0; j <= i; j++) {
            p = p.next; //p指向下表为i的元素
        }
        return p.getData();


    }

    @Override
    public boolean isEmpty() {
        return size == 0;
    }

    @Override
    public void add(Object e) {
        this.add(size, e);

    }

    @Override
    public void add(int i, Object e) {
        if (i < 0 || i > size) {
            throw new MyIndexOutOfBoundsException("对不起，下标越界了！");
        }
        Node p = head;
        for (int j = 0; j < i; j++) {
            p = p.next;
        }
        Node newNode = new Node();
        newNode.data = e;
        newNode.next = p.next;
        p.next = newNode;
        size++;
    }


    @Override
    public String toString() {
        if (size == 0) {
            return "[]";
        } else {

            StringBuffer stringBuffer = new StringBuffer("[");
            Node p = head;
            for (int i = 0; i < size - 1; i++) {
                p = p.next;
                stringBuffer.append(p.getData()).append(",");
            }
            stringBuffer.append(p.next.getData()).append("]");
            return stringBuffer.toString();
        }
    }
}
~~~

~~~java
//测试类
public class Test2 {
    public static void main(String[] args) {
        List list = new SingleLinkedList();
        list.add(100);
        list.add(200);
        list.add(300);
        list.add(400);
        list.add(500);
        list.add(2, 999);
        System.out.println("单链表长度:" + list.size());
        System.out.println("单链表是否为空：" + list.isEmpty());
        System.out.println("遍历单链表-------------------");
        for (int i = 0; i < list.size(); i++) {
            System.out.print(list.get(i) + "  ");
        }
        System.out.println();
        System.out.println("测试toString方法-------------------");
        System.out.println(list);
    }
}
~~~







