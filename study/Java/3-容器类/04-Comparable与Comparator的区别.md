## Comparable 自然排序

Comparable 在 java.lang 包下，是一个接口，内部只有一个方法 compareTo()：

```java
public interface Comparable<T> {
    public int compareTo(T o);
}
```

Comparable 可以让实现它的类的对象进行比较，具体的比较规则是按照 compareTo 方法中的规则进行。这种顺序称为 自然顺序。（如 String、Integer已经实现了Comparable接口，自己就可以完成比较大小操作）

如果一个对象被用于任何种类的排序容器中，例如SortedSet（TreeSet是其唯一实现），那么它必须实现这个接口。

compareTo 方法的返回值有三种情况：

e1.compareTo(e2) > 0 即 e1 > e2
e1.compareTo(e2) = 0 即 e1 = e2
e1.compareTo(e2) < 0 即 e1 < e2

## Comparator 定制排序

Comparator 在 java.util 包下，也是一个接口，JDK 1.8 以前只有两个方法：

```java
public interface Comparator<T> {

    public int compare(T lhs, T rhs);

    public boolean equals(Object object);
}
```


从上面内容可知使用自然排序需要类实现 Comparable，并且在内部重写 comparaTo 方法。

而 Comparator 则是在外部制定排序规则，然后作为排序策略参数传递给某些类，比如 Collections.sort(), Arrays.sort(), 或者一些内部有序的集合（比如 SortedSet，SortedMap 等）。

使用方式主要分三步：

1. 创建一个 Comparator 接口的实现类，并赋值给一个对象
    - 在 compare 方法中针对自定义类写排序规则
3. 将 Comparator 对象作为参数传递给 排序类的某个方法
4. 向排序类中添加 compare 方法中使用的自定义类

```java
public class Test{
    public static void main(String[] args){

// 1.创建一个实现 Comparator 接口的对象
        Comparator comparator = new Comparator() {
            @Override
            public int compare(Object object1, Object object2) {
                if (object1 instanceof NewBookBean && object2 instanceof NewBookBean){
                    NewBookBean newBookBean = (NewBookBean) object1;
                    NewBookBean newBookBean1 = (NewBookBean) object2;
                    //具体比较方法参照 自然排序的 compareTo 方法，这里只举个栗子
                    return newBookBean.getCount() - newBookBean1.getCount();
                }
                return 0;
            }
        };

    //2.将此对象作为形参传递给 TreeSet 的构造器中
    TreeSet treeSet = new TreeSet(comparator);
    
    //3.向 TreeSet 中添加 步骤 1 中 compare 方法中设计的类的对象
    treeSet.add(new NewBookBean("A",34));
    treeSet.add(new NewBookBean("S",1));
    treeSet.add( new NewBookBean("V",46));
    treeSet.add( new NewBookBean("Q",26));
}
}

```
