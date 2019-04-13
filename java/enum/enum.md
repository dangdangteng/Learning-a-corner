# 枚举 enum

```
package com.angle.alita.mimor;

/***
 * created by huxueyan101
 * @data : 2019-04-14,2019
 ***/
public enum demo2 {
    a("1", 1),
    b("2", 2),
    c("3", 3);
    private String s;
    private Integer i;

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

class aba {

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

