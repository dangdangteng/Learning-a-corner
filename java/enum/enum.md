```java
public enum demo2 {
    a("1", 1),
    b("2", 2),
    c("3", 3);
    /**
        s 字符串
     */
    private String s;
    /**
        i 整数
     */
    private Integer i;

    /**
     *
     * @param s
     * @param i
     */
    demo2(String s, int i) {
        this.s = s;
        this.i = i;
    }

    public String getS() {
        return s;
    }

    public Integer getI() {
        return i;
    }
}

class A {

    public static void main(String[] args) {
        String test = demo2.a.getS();
        String test1 = demo2.b.getS();
        String test2 = demo2.c.getS();
        int ti = demo2.a.getI();
        int ti1 = demo2.b.getI();
        int ti2 = demo2.c.getI();
        System.out.printf("%s,%s,%s%n", test, test1, test2);
        System.out.println(ti+ti1+ti2);
    }
}
```



1）代码可读性差、易用性低。

2）类型不安全。

3）耦合性高，扩展性差。