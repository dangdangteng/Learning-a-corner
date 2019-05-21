```java
    public static void main(String[] args) {
        Map<String,Object> hashMap = new HashMap<>(16);
        hashMap.put("test1",12345);
        hashMap.put("test2",109876);
        hashMap.forEach((key,value)->{
            if ("test1".equals(key)){
                System.out.println(value);
            }
        });
        for (Map.Entry<String,Object> entry : hashMap.entrySet()){
            System.out.println(entry.getKey()+entry.getValue());
        }
    }
```
