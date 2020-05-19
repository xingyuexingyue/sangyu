```java
public class MyTest {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<Integer>();
        for (int i = 10; i >= 0; i--) {
            list.add(i); // add() 添加元素
        }
        List<Integer> list1 = new ArrayList<Integer>();
        list1.addAll(list); // addAll() 添加全部元素 传入的参数是 Collections 子类型
        System.out.println(list.contains(1)); // contains() 判断是否包含某元素
        System.out.println(list.containsAll(list1)); // 判断容器中是否包含另一个容器中的所有元素
        System.out.println(list.isEmpty()); // 判断是否包含元素
        Iterator it = list.iterator(); // 返回一个Iterator 对象，遍历容器中的元素
        while (it.hasNext()) {
            Integer i = (Integer) it.next();
            System.out.println(i);
        }
        Object[] o = list.toArray(); // toArray() 返回数组，类型是Object
        for (int i = 0; i < o.length;i++){
            System.out.println(o[i]);
        }

        Integer[] a = new Integer[2];
        Integer[] o1 = list.toArray(a); // toArray() 返回的数组类型与传入的数组类型是一样的
        for (int i = 0; i < o1.length;i++){
            System.out.println(o[i]);
        }
    }
}
```
