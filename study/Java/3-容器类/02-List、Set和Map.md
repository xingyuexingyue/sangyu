
## 一. 容器

Java集合框架主要包括两种类型的容器，一种是集合（Collection），存储一个元素集合，另一种Map，存键值对映射

Collection接口有3种子类型，List、Set和Queue，再下面是一些抽象类，最后是具体实现类，常用的有：ArrayList、LinkedList、HashSet、LinkedHashSet、HashMap、LinkedHashMap

![容器API简略图](https://upload-images.jianshu.io/upload_images/2765653-0049ad8faf5d347e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

另外，容器不能存储基本类型，只能是对象引用

## 二. Collection接口

Collection接口中定义了存取一组对象的方法，其子接口Set和List分别定义了存储方式

#### 1. Set

Set是最简单的一种集合，集合中的对象不按特定的方式排序，并且没有重复对象。Set接口主要实现了三个类

1) HashSet类: 按照哈希算法来存取集合中的对象，存取速度比较快。为快速查找设计Set。

2) TreeSet类：实现了SortedSet接口，能够对集合中的对象进行排序，（按照实现Comparable接口，并实现compareTo()方法）

3）LinkedHashSet：具有HashSet的查询速度，且内部使用链表维护元素的顺序（插入的次序）。因此在使用迭代器遍历Set时，结果会按元素插入的次序显示。

在使用HashSet类的时候要注意：存入HashSet的对象必须重写hashCode()，因为如果类没有父类的话，默认会继承Object类，父类提供hashCode()方法，它默认使用对象的地址计算散列码，HashSet使用哈希算法来存储集合中的对象，如果使用相同字段的信息创建两个对象，那么就可以将对象都保存到map，当我们在查找时，通过一个对象来查找查找另一个对象，发现是无法工作的。所以存入HashSet的对象必须重写hashCode()，JDK提供的类一般都会实现hashCode()方法,如果是自定义的类要存储到HashSet必须重写hashCode()方法，并且也要一定要重写equals()方法，因为要通过equals()方法判断重复性

#### 2. List

List按照插入的顺序保存元素，并且每个值可以重复

1) ArrayList：按照插入的顺序保存元素，代表长度可以改变的数组，可以对元素进行随机的访问，插入和删除元素的速度慢

2) LinkedList：按照插入的顺序保存元素，采用链表的数据结构，插入和删除速度快，访问速度慢

#### 3. Collection接口提供的方法


|  方法名   | 功能  |
|  ----  | ----  |
| boolean add(T)  | 确保容器持有泛型类型T的参数,如果参数没有添加进容器，返回false  |
| boolean addAll(Collection<? extends T>) | 添加参数中的所有元素，只要添加了任意元素就返回true |
| void clear() | 移除容器中的所有元素  |
| boolean contains(T) | 判断容器中是否持有泛型类型T此参数，则返回true |
| boolean containsAll(Collection<?> c) | 判断容器持有此参数中的所有元素，则返回true |
| boolean isEmpty() | 容器中没有元素返回true |
| Iterator<T> iterator() | 返回一个Iterator<T>，用来用来遍历容器中的元素 |
| boolean remove(Object)| 如果参数在容器中，则移除此元素的一个实例。则返回true |
| boolean removeAll(Collection<?>)| 移除参数中的所有元素。只要有移除动作发生就返回true() |
| boolean retainAll(Collection<?>)|只保存参数容器和当前容器交集的部分，只要Collection发生了改变就返回true |
| int size()| 返回容器中元素的数目 |
| Object[] toArray() | 返回一个数组，该数组包含容器中的所有元素 |
| <T> T[] toArray(T[] a)| 返回一个数组，数组元素中的类型，与类型数组a的类型相同  |

#### 4. SortedSet

TreeSet类是SortedSet接口的唯一实现，SortedSet中的元素可以保证处于排序状态，Comparator comparator()返回当前Set使用的Comparator；或者
返回null，表示以自然方式排序。Comparable 可以让实现它的类的对象进行比较，具体的比较规则是按照 compareTo 方法中的规则进行。这种顺序称为 自然顺序。

SortedSet按对象的比较函数对元素排序，而不是"元素插入的次序"，必须实现Comparable

## 三. Map接口

Map接口定义了存储键（key）-值（value）映射对的方法，从Map集合中检索元素时，只要给出键对象，就会返回对应的值对象。Map类中存储的键值对通过键来标识，所以键值不能重复。

1) HashMap：Map基于散列表的实现。插入和查询"键值对"的开销是固定的，没有按照任何明显的顺序来保存元素

2) LinkedHashMap: 键值对的顺序是其插入次序的，或者是最近最少使用（LRU）的次序，

3) TreeMap：按照比较结果的升序保存键


#### 1. 实现一个Map

```java
public class AssociativeArray<K, V> {
    private Object[][] pairs;
    private int index;

    public AssociativeArray(int length) {
        pairs = new Object[length][2];
    }

    public void put(K key, V value) {
        if (index >= pairs.length) {
            throw new ArrayIndexOutOfBoundsException();
        }
        pairs[index++] = new Object[]{key, value};
    }

    public V get(K key) {
        for (int i = 0; i < index; i++) {
            if (key.equals(pairs[i][0])) {
                return (V) pairs[i][1];
            }
        }
        return null;
    }

    @Override
    public String toString() {
        StringBuilder result = new StringBuilder();
        for (int i = 0; i < index; i++) {
            result.append(pairs[i][0].toString());
            result.append(" : ");
            result.append(pairs[i][1].toString());
            if (i < index - 1) {
                result.append("\n");
            }
        }
        return result.toString();
    }

    public static void main(String[] args) {
        AssociativeArray<String,String> map = new AssociativeArray<>(6);
        map.put("sky","blue");
        map.put("grass","green");
        map.put("ocean","dancing");
        map.put("tree","tall");
        map.put("earth","brown");
        map.put("sun","warm");
        try{
            map.put("extra","object");
        }catch (ArrayIndexOutOfBoundsException e){
            System.out.println("Too many objects!");
        }
        System.out.println(map);
        System.out.println(map.get("ocean"));
    }
}
```

#### 2. 性能

在上面的例子中简单的实现了一个map，使用get()方法，查找想要的key，他会将与之相关联的值作为返回结果返回，或者在找不到的情况下返回null。在上面的实现中，使用了比较差的的方式来定位值，从数组的头部开始，使用equals()方法依次比较键。

在HashMap中使用了特殊的值，称作散列码，来取代对键的缓慢搜索。

## 四. Queue

Queue按照排队规则来确定产生的顺序，通常与它们被插入的顺序相同，并且只允许在容器的一端插入对象，并从另外一端移除对象（先进先出）。







