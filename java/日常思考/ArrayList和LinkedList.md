# ArrayList 制定初始大小对于数据的增添会加快速度

减少了数组的扩容

```java
private static int len = 16;

    public static void main(String[] args) {
        List arrayList = new ArrayList();
        List brrayList = new ArrayList(len);
        long time_1 = System.nanoTime();
        for (int i=0;i<len;i++){
            arrayList.add(i);
        }
        long time_2 = System.nanoTime();
        for (int j=0;j<len;j++){
            brrayList.add(j);
        }
        long time_3 = System.nanoTime();
        System.out.println(time_2-time_1);
        System.out.println(time_3-time_2);

    }
```

> 数组的连续内存,会有一部分或全部数据一起进入到cpu缓存,而链表还需要再去内存中根据上下标查找:CPU缓存比内存快太多
>
> 数据大小固定不适合动态存储,动态添加,内存为一连续的地址,可随机访问查询较快,链表大小可变,扩展性强,只能顺着指针方向查询,速度较慢