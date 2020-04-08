在ArraysList中确定一个元素是否属于某个List，发现某个元素的索引，以及从某个List中移除一个元素时，都会用到equals()方法，
它是Object类一部分（所以类的父类），比如现在有个User类，
每个User类都被定义为唯一的对象，并将它添加到List中，这时在创建一个Use对象，并把它创建给indexOf()方法，其结果是-1，表示没有找到，
而且尝试remove()也会返回false。对于其他的类equals()的定义可能有所不同，例如，两个String只有在内容完全一样的情况下，才会是等价的。
因此，为了防止意外，就必须意识到List的行为根据equals()的行为而有所变化



一、java当中的数据类型和“==”的含义：

基本数据类型（也称原始数据类型） ：byte,short,char,int,long,float,double,boolean。他们之间的比较，应用双等号（==）,比较的是他们的值。
引用数据类型：当他们用（==）进行比较的时候，比较的是他们在内存中的存放地址（确切的说，是堆内存地址）。
注：对于第二种类型，除非是同一个new出来的对象，他们的比较后的结果为true，否则比较后结果为false。因为每new一次，都会重新开辟堆内存空间。

 

二、equals()方法介绍：

JAVA当中所有的类都是继承于Object这个超类的，在Object类中定义了一个equals的方法，equals的源码是这样写的：

public boolean equals(Object obj) {
    //this - s1
    //obj - s2
    return (this == obj);
}
可以看到，这个方法的初始默认行为是比较对象的内存地址值，一般来说，意义不大。所以，在一些类库当中这个方法被重写了，如String、Integer、Date。在这些类当中equals有其自身的实现（一般都是用来比较对象的成员变量值是否相同），而不再是比较类在堆内存中的存放地址了。
所以说，对于复合数据类型之间进行equals比较，在没有覆写equals方法的情况下，他们之间的比较还是内存中的存放位置的地址值，跟双等号（==）的结果相同；如果被复写，按照复写的要求来。

我们对上面的两段内容做个总结吧：

 == 的作用：
　　基本类型：比较的就是值是否相同
　　引用类型：比较的就是地址值是否相同
equals 的作用:
　　引用类型：默认情况下，比较的是地址值。
注：不过，我们可以根据情况自己重写该方法。一般重写都是自动生成，比较对象的成员变量值是否相同

三、String类的equals()方法：

```
 public boolean equals(Object anObject) {
 2         if (this == anObject) {
 3             return true;
 4         }
 5         if (anObject instanceof String) {
 6             String anotherString = (String)anObject;
 7             int n = value.length;
 8             if (n == anotherString.value.length) {
 9                 char v1[] = value;
10                 char v2[] = anotherString.value;
11                 int i = 0;
12                 while (n-- != 0) {
13                     if (v1[i] != v2[i])
14                         return false;
15                     i++;
16                 }
17                 return true;
18             }
19         }
20         return false;
21     }
```