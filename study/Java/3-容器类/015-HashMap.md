```java
public class HashMapTest{
    public static void main(String[] args){
        HashMap<String,Integer> hashMap = new HashMap<>();
        // 添加 key-value，如果 key 不存在添加，如果 key 存在使用 value 替换旧值
        hashMap.put("aa",1);
        hashMap.put("bb",2);
        // 元素遍历，第一种方式
        Iterator iterator = hashMap.keySet().iterator();
        while(iterator.hasNext()){
            String key = (String)iterator.next();
            System.out.println(key + "=" + hashMap.get(key));
        }
        // 元素遍历，第二种方式
        Iterator iterator1 = hashMap.entrySet().iterator();

        while(iterator1.hasNext){
            Map.Entry entry = (Map.Entry) iterator1.next();
            String key = (String) entry.getKey();
            Integer value = (Integer) entry.getValue();
            System.out.println(key + "=" + value);
        }
    }
}
```