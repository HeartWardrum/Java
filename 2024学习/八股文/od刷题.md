## 1.[字符串序列判断](https://gw-c.nowcoder.com/api/sparta/jump/link?link=https%3A%2F%2Fwww.nowcoder.com%2Fdiscuss%2F634152267439951872)

~~~java
    public static void main(String[] args) throws IOException {

        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        String s = bufferedReader.readLine();
        String l = bufferedReader.readLine();
        System.out.println(findIt(s,l));

    }

    private static int findIt(String s, String l) {
        int i = 0;
        int j = 0;
        while (i < s.length() && j < l.length()) {
            if (s.charAt(i) == l.charAt(j)) {
                i++;
            }
            j++;
        }
        if (i == s.length()) {
            return j - 1;
        } else {
            return -1;
        }
    }
~~~

