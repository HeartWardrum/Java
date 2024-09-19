# 题目描述

存在一种虚拟IPv4地址，由4小节组成，每节的范围为0~255，以#号间隔，虚拟IPv4地址可以转换为一个32位的整数，例如：

- 128#0#255#255，转换为32位整数的结果为2147549183（0x8000FFFF）
- 1#0#0#0，转换为32位整数的结果为16777216（0x01000000）

现以字符串形式给出一个虚拟IPv4地址，限制第1小节的范围为1 ~ 128，即每一节范围分别为(1 ~ 128)#(0~255)#(0~255)#(0~255)，要求每个IPv4地址只能对应到唯一的整数上。

如果是非法IPv4，返回invalid IP

# 输入描述

输入一行，虚拟IPv4地址格式字符串

# 输出描述

输出一行，按照要求输出整型或者特定字符

# 备注

输入不能确保是合法的IPv4地址，需要对非法IPv4（空串，含有IP地址中不存在的字符，非合法的#分十进制，十进制整数不在合法区间内）进行识别，返回特定错误

# 用例1

## 输入

```none
100#101#1#5
```



## 输出

```none
1684340997
```



# 用例2

## 输入

```none
1#2#3
```



## 输出

```none
invalid IP
```



~~~java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        test(br);
        br.close();
    }

    static void test(BufferedReader br) throws IOException {
        String ipv4 = br.readLine();
        if (!ipv4.contains("#")) {
            System.out.println("invalid IP");
            return;
        }
        String[] sArr = ipv4.split("#");

        if (sArr.length != 4) {
            System.out.println("invalid IP");
            return;
        }
        int result = 0;
        for (int i = 0; i < 4; i++) {
            int number;
            try {
                number = Integer.parseInt(sArr[i]);
            } catch (NumberFormatException e) {
                System.out.println("invalid IP");
                return;
            }
            result |= number << ((3 - i) * 8);
        }
        System.out.println(result);
    }
~~~

