## for 和 foreach

1. for 循环在遍历集合时使用下标来定位集合中的元素。

2. foreach 适用于数组或实现了 iterator 的集合类。foreach 就是对实现了 Iterator 接口的集合遍历的。
   
3. 在用 foreach 循环遍历一个集合时，不能改变集合中的元素，如增加元素、修改元素。否则会抛出ConcurrentModificationException异常。想了解原因的可以研究一下源码。
   
   也不能修改集合中的元素（不报异常），但可以修改元素的属性。

# Iterator 和 foreach

所有实现了 Collection 接口的容器类都有一个 iterator() 方法，返回一个实现了iterator接口的对象。Iterator对象称作迭代器，用以方便的实现对容器内元素的遍历操作。

Iterator接口定义了如下方法：

![](https://upload-images.jianshu.io/upload_images/2765653-edd1ee7628ddec44.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

