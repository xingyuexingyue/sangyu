

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
    public static void main(String[] args){
        List<Integer> list = new ArrayList<>();
        Random random = new Random();
        for(int i = 0; i < 10; i++){
            list.add(random.nextInt(100));
        }
        
        for (Integer integer : list){
            System.out.println("元素：" + integer);
        }
        
        Collections.sort(list);
        
        for (Integer integer : list){
                    System.out.println("元素：" + integer);
        }
    }
}
```

2. 对 String  泛型的 List 排序

排序规则：先按照首字母进行排序，如果第一个首字母相同，则按照第二位进行排序

排列顺序：0-9    A-Z    a-z

3. 自定义类型的 list 集合排序：

定义 student 实体类，必须继承 Comparable 接口，重写它的 compareTo 方法

compareTo() 方法返回正数表示大，负数表示小，0表示相等

```java
public class Student implements Comparable<Student>{
    private Integer id;
    private String stuject;
    private String name;
    
    public Student(Integer id,String subject,String name){
        this.id = id;
        this.stuject = stuject;
        this.name = name;
    }
    
    // 省略 setter 和 getter

    @Override
    public String toString() {
        return " [id=" + id + ", subject=" + subject + ", name=" + name + "]";
    }

    @Override
    public int compareTo(Student stu){
        return this.id.compareTo(stu.id); // 单一属性比较
    }
}







```

