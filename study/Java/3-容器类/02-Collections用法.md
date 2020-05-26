

## Collections.nCopies() 用法

Collections.nCopies() 传递给构造器的 List，填充 ArrayList

```java
public class FillingLists {
    public static void main(String[] args) {
        List<StringAddress> list = new ArrayList<StringAddress>(Collections.nCopies(4,new StringAddress("Hello")));
        System.out.println(list);
        Collections.fill(list,new StringAddress("World"));
        System.out.println(list);
    }
}

class StringAddress{
    private String s;
    public StringAddress(String s){
        this.s = s;
    }

    @Override
    public String toString() {
        return "StringAddress{" +
                "s='" + s + '\'' +
                '}';
    }
}
```

## Collections.fill() 用法

Collections.fill() 复制同一个对象应用来填充整个容器，但只能替换已经在 List 中存在的元素，而不能添加新的元素


```java
public class FillingLists {
    public static void main(String[] args) {
        List<StringAddress> list = new ArrayList<StringAddress>(Collections.nCopies(4,new StringAddress("Hello")));
        System.out.println(list);
        Collections.fill(list,new StringAddress("World"));
        System.out.println(list);
    }
}

class StringAddress{
    private String s;
    public StringAddress(String s){
        this.s = s;
    }

    @Override
    public String toString() {
        return "StringAddress{" +
                "s='" + s + '\'' +
                '}';
    }
}
```

## sort排序详解（Comparable & Comparator）

1. Collections.sort() 对 Integer 泛型的 List 排序

```java

public class MyTest{
    

}





```
