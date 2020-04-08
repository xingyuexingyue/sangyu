## for和foreach

普通for循环在遍历集合时使用下标来定位集合中的元素。java在JDK1.5开始支持foreach循环，foreach在一定程度上简化了对集合的遍历。但某些情况下，foreach是不能完全代替for循环的。

限制场景：

1. foreach适用于数组或实现了iterator的集合类。foreach就是使用Iterator接口来实现对集合的遍历的。
   
2. 在用foreach循环遍历一个集合时，不能改变集合中的元素，如增加元素、修改元素。否则会抛出ConcurrentModificationException异常。想了解原因的可以研究一下源码。
   
   也不能修改集合中的元素（不报异常），但可以修改元素的属性。



# Iterator和增强for循环

Iterator：所有实现了Collection接口的容器类都有一个iterator方法，用以返回一个实现了iterator接口的对象。Iterator对象称作迭代器，用以方便的实现对容器内元素的遍历操作。

Iterator接口定义了如下方法：

![](https://upload-images.jianshu.io/upload_images/2765653-edd1ee7628ddec44.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


  2、增强for循环主要用来取集合数组的数据。只能用在数组实现iterable接口的集合类上。