为了方便的处理集合中元素，Java 中提供了一些方法专门处理集合中的元素，例如删除和获取集合中的元素，该对象就叫做迭代器（Iterator）

通过 iterator() 方法获得的迭代器，所有集合类都通过内部类的方式提供了迭代器，可以通过此方法来获得

## Iterable

Iterable 接口只提供了一个方法 iterator()，这个方法可以返回一个迭代器，这个迭代器支持增强 for 循环，Collection 继承了 Iterable，所以 Collection 中都具备获得迭代器的方法，只不过每个子类集合实现方式不同（因为数据结构不同）

## Iterator

Itreator 接口是集合的迭代器接口类，定义了常见的迭代方法：

```
1：boolean hasNext() 判断集合中是否有元素，如果有元素可以迭代，就返回true。
						
2：E next()  返回迭代的下一个元素，注意： 如果没有下一个元素时，调用 next 元素会抛出 NoSuchElementException
						
3：void remove() 从迭代器指向的集合中移除迭代器返回的最后一个元素（可选操作）
```

## 迭代器的遍历

第一种方式：while 循环

```java
public class IteratorTest {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        list.add("哈哈是只小狗狗狗");
        list.add("喵喵是只小猫猫猫");
        list.add("妞妞是只小可爱鱼");
        Iterator<String> it = list.iterator();
        while (it.hasNext()){
            System.out.println(it.next());
        }
    }
}
```

第二种方式：for 循环

```java
public class IteratorTest01 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        list.add("哈哈是只小狗狗狗");
        list.add("喵喵是只小猫猫猫");
        list.add("妞妞是只小可爱鱼");
        for (Iterator<String> it = list.iterator(); it.hasNext(); ) {
            System.out.println(it.next());
        }
    }
}
```

使用迭代器清空集合

```java
public class IteratorTest02 {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        list.add("哈哈是只小狗狗狗");
        list.add("喵喵是只小猫猫猫");
        list.add("妞妞是只小可爱鱼");
        System.out.println("移除前" + list);
        Iterator<String> it = list.iterator();
        while (it.hasNext()) {
            it.next();
            it.remove();
        }
        System.out.println("移除后" + list);
    }
}
```

需要注意的细节如下：

细节一：

如果迭代器的指针已经指向了集合的末尾，那么如果再调用 next() 会返回 NoSuchElementException 异常

![](https://upload-images.jianshu.io/upload_images/2765653-854c2b825cb1122a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

细节二：

如果调用 remove 之前没有调用 next 是不合法的，会抛出 IllegalStateException

![](https://upload-images.jianshu.io/upload_images/2765653-fd6609f346a7e924.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 迭代器的原理

查看ArrayList源码

```java
     
private class Itr implements Iterator<E> {
 
		int cursor = 0;
 
		int lastRet = -1;
 
		int expectedModCount = modCount;
 
		public boolean hasNext() {
			return cursor != size();
		}
 
		public E next() {
			checkForComodification();
			try {
				E next = get(cursor);
				lastRet = cursor++;
				return next;
			} catch (IndexOutOfBoundsException e) {
				checkForComodification();
				throw new NoSuchElementException();
			}
		}
 
		public void remove() {
			if (lastRet == -1)
				throw new IllegalStateException();
			checkForComodification();
 
			try {
				AbstractList.this.remove(lastRet);
				if (lastRet < cursor)
					cursor--;
				lastRet = -1;
				expectedModCount = modCount;
			} catch (IndexOutOfBoundsException e) {
				throw new ConcurrentModificationException();
			}
		}
}
```

注意：

1. 在对集合进行迭代过程中，不允许出现迭代器以外的对元素的操作，因为这样会产生安全隐患，java会抛出异常并发修改异常（ConcurrentModificationException），普通迭代器只支持在迭代过程中的删除动作。

2. ConcurrentModificationException: 当一个集合在循环中即使用引用变量操作集合又使用迭代器操作集合对象， 会抛出该异常。

```java

public class IteratorTest {
	public static void main(String[] args) {
		List<String> list = new ArrayList<String>();
        list.add("哈哈是只小狗狗狗");
        list.add("喵喵是只小猫猫猫"i);
        list.add("妞妞是只小可爱鱼");
		Iterator<String> it = list.iterator();
		while (it.hasNext()) {
			it.next();
			it.remove();
			list.add("abc"); // 出现了迭代器以外的对元素的操作
		}
		System.out.println(list);
	}
}
```

## List 特有的迭代器 ListIterator

如果是 List 集合，想要在迭代中操作元素可以使用 List 集合的特有迭代器 ListIterator，该迭代器支持在迭代过程中，添加元素和修改元素。

```

---| Iterator
		hasNext()
		next()
		remove()
	   ------| ListIterator Iterator子接口 List专属的迭代器
                  add(E e)    将指定的元素插入列表（可选操作）。该元素直接插入到 next 返回的下一个元素的前面（如果有）
                  void set(E o)   用指定元素替换 next 或 previous 返回的最后一个元素
                  hasPrevious()    逆向遍历列表，列表迭代器有多个元素，则返回 true。
                  previous() 

```

Iterator在迭代时，只能对元素进行获取 next() 和删除 remove()的操作

对于 Iterator 的子接口 ListIterator 在迭代 list 集合时，还可以对元素进行添加 add(obj)，修改 set(obj) 的操作

1. next() 

```java
public class IteratorTest {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        list.add("哈哈是只小狗狗狗");
        list.add("喵喵是只小猫猫猫");
        list.add("妞妞是只小可爱鱼");
        ListIterator<String> lit = list.listIterator();
        while (lit.hasNext()){
            System.out.println(lit.next());
        }
    }
}
```

2. 倒序遍历

```java
public class IteratorTest {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        list.add("哈哈是只小狗狗狗");
        list.add("喵喵是只小猫猫猫");
        list.add("妞妞是只小可爱鱼");
        ListIterator<String> lit = list.listIterator();
        while (lit.hasNext()){
            System.out.println(lit.next());
        }
        while (lit.hasPrevious()) {
            String next = lit.previous();
            System.out.println(next);
        }
    }
}
```

3. set() 重新指定元素内容

```java
public class IteratorTest {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        list.add("哈哈是只小狗狗狗");
        list.add("喵喵是只小猫猫猫");
        list.add("妞妞是只小可爱鱼");
        list.add("最后一个哈哈哈");
        System.out.println("替换前" + list);
        ListIterator<String> lit = list.listIterator();
        lit.next();
        lit.next();
        lit.next();
        lit.next();
        lit.set("替换啦");
        System.out.println("替换后" + list);
    }
}
```

4. add() 添加新元素

```java
public class IteratorTest {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        list.add("哈哈是只小狗狗狗");
        list.add("喵喵是只小猫猫猫");
        list.add("妞妞是只小可爱鱼");
        System.out.println("添加前" + list);
        ListIterator<String> lit = list.listIterator();
        lit.next();
        lit.next();
        lit.next();
        lit.add("最后一个哈哈哈");
        System.out.println("添加后" + list);
    }
}
```