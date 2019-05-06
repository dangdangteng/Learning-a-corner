```java
package com.angle.alita.mimor;

import java.sql.SQLOutput;
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

/***
 * @creation purpose : 测试3者的执行效率
 * @data : 19:52,2019-05-06
 * @author : 『Ezreal』
 * @Character description : 最帅的那个就是我
 ***/
public class ForForeachStream {
    public ForForeachStream() {

    }

    public static void main(String[] args) {
        List alist = new ArrayList();

        for (int i=0;i<1000000;i++){
            alist.add(i);
        }
        long foreachSystemCuTimeStart = System.currentTimeMillis();
        for (Object a: alist
             ) {
            System.out.println("foreach 执行效率...");
        }
        long foreachSystemCuTimeEnd = System.currentTimeMillis();
        for (int i=0;i<alist.size();i++){
            System.out.println("for 执行效率...");
        }
        long forSystemCuTimeEnd = System.currentTimeMillis();
        alist.stream().forEach(o -> {
            System.out.println("stream 执行效率...");
        });
        long streamSystemCuTimeEnd = System.currentTimeMillis();
        alist.stream().spliterator().forEachRemaining(o -> {
            System.out.println("stream spliterator 执行效率...");
                }
        );
        long streamSpliteratorSystemCuTimeEnd = System.currentTimeMillis();
        System.out.println(foreachSystemCuTimeEnd-foreachSystemCuTimeStart);
        System.out.println(forSystemCuTimeEnd-foreachSystemCuTimeEnd);
        System.out.println(streamSystemCuTimeEnd-forSystemCuTimeEnd);
        System.out.println(streamSpliteratorSystemCuTimeEnd-streamSystemCuTimeEnd);
    }
}

执行效率很有意思
```

