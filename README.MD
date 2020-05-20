## Java 基础 

- Java 容器
    - [ ] Collection 接口
    - [ ] [Iterator 迭代器 ](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/017-%E8%BF%AD%E4%BB%A3%E5%99%A8%20Iterator.md)
    - [ ] Map 映射表的基础接口

    - java.util.Collections
        - [ ] fill() 填充容器，只能条换不能添加新元素 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/02-Collections%E7%94%A8%E6%B3%95.md#collectionsncopies-%E7%94%A8%E6%B3%95)
        - [ ] nCopies() 填充容器 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/02-Collections%E7%94%A8%E6%B3%95.md#collectionsfill-%E7%94%A8%E6%B3%95)
        
    - java.util.Collection [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/01-Collection%E6%8E%A5%E5%8F%A3%E6%8F%90%E4%BE%9B%E7%9A%84%E6%96%B9%E6%B3%95.md)
        - [ ] add() 添加元素
        - [ ] addAll() 添加全部元素
        - [ ] contains() 判断容器中是否存在某元素
        - [ ] containsAll() 判断容器中是否包含另一个容器中的所有元素
        - [ ] isEmpty() 判断是否包含元素
        - [ ] iterator() 返回一个Iterator对象，遍历容器中的元素
        - [ ] remove() 移除元素
        - [ ] removeAll() 移除所有元素
        - [ ] clear() 移除所有元素
        - [ ] size() 长度
        - [ ] toArray() 返回一个数组
        
    - Map [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/015-Map.md)
        - [ ] size()
        - [ ] isEmpty()
        - [ ] containsKey(Object key)
        - [ ] containsValue(Object value)
        - [ ] get(Object key)
        - [ ] put(K key, V value)
        - [ ] remove(Object key)
        - [ ] putAll(Map<? extends K, ? extends V> m)
        - [ ] clear()
        - [ ] keySet()
        - [ ] Collection<V> values()
        - [ ] Set<Map.Entry<K, V>> entrySet()       
        
    - 其他 
        - [ ] for 和 foreach 区别 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/05-for%E5%92%8Cforeach%E7%9A%84%E5%8C%BA%E5%88%AB.md)
        - [ ] equals 和 == 区别 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/06-equals()%E6%96%B9%E6%B3%95.md)

- Java 并发
    - 线程的创建方式 
        - [ ] 继承 Thread 类 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/00-%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F.md#%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F%E7%AC%AC%E4%B8%80%E7%A7%8D%E7%BB%A7%E6%89%BF-thread-%E7%B1%BB)
        - [ ] 实现 Runnable 接口 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/00-%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F.md#%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F%E7%AC%AC%E4%BA%8C%E7%A7%8D%E5%AE%9E%E7%8E%B0-runnable-%E6%8E%A5%E5%8F%A3)
        - [ ] 实现 Callable 接口 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/00-%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F.md#%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F%E7%AC%AC%E4%B8%89%E7%A7%8D%E5%AE%9E%E7%8E%B0-callable-%E6%8E%A5%E5%8F%A3-%E6%9C%89%E8%BF%94%E5%9B%9E%E5%80%BC)
        - [ ] 线程池的方式 ExecutorService [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/00-%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F.md#%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F%E7%AC%AC%E5%9B%9B%E7%A7%8D%E7%BA%BF%E7%A8%8B%E6%B1%A0%E7%9A%84%E6%96%B9%E5%BC%8F-executorservice)
            - newCachedThreadPool \ newFixedThreadPool \ newScheduledThreadPool \ newSingleThreadExecutor 
    - 线程生命周期 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/022-%E7%BA%BF%E7%A8%8B%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.md)
        - [ ] 新建状态（ new ）
        - [ ] 就绪状态 ( Runnable ）
        - [ ] 运行状态（ Running ）
        - [ ] 阻塞状态（ Blocked ）
        - [ ] 线程死亡（ Dead )
    - 线程的优先级 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/021-%E8%AE%BE%E7%BD%AE%E7%BA%BF%E7%A8%8B%E4%BC%98%E5%85%88%E7%BA%A7.md)
        - [ ] getPriority() 读线程的优先级
        - [ ] setPriority() 修改线程优先级
    - 线程基本方法 [代码位置]()
        - [ ] wait()
        - [ ] notify()
        - [ ] notifyAll()
        - [ ] sleep()
        - [ ] join()
        - [ ] yield()
    - 加锁相关 
        - [ ] 为某个对象加锁 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/01-%E4%B8%BA%E6%9F%90%E4%B8%AA%E5%AF%B9%E8%B1%A1%E5%8A%A0%E9%94%81.md)
        - [ ] this 加锁 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/02-this%E5%8A%A0%E9%94%81.md)
        - [ ] 执行代码的时候锁定当前对象 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/03-%E6%89%A7%E8%A1%8C%E4%BB%A3%E7%A0%81%E7%9A%84%E6%97%B6%E5%80%99%E9%94%81%E5%AE%9A%E5%BD%93%E5%89%8D%E5%AF%B9%E8%B1%A1.md)
        - [ ] 锁定静态方法 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/04-%E9%94%81%E5%AE%9A%E9%9D%99%E6%80%81%E6%96%B9%E6%B3%95.md)
        - [ ] 线程重入的问题 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/05-%E7%BA%BF%E7%A8%8B%E9%87%8D%E5%85%A5%E7%9A%84%E9%97%AE%E9%A2%98.md)
        - [ ] 同步方法和非同步方法是否可以同时调用 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/06-%20%E5%90%8C%E6%AD%A5%E6%96%B9%E6%B3%95%E5%92%8C%E9%9D%9E%E5%90%8C%E6%AD%A5%E6%96%B9%E5%BC%8F%E6%98%AF%E5%90%A6%E5%8F%AF%E4%BB%A5%E5%90%8C%E6%97%B6%E8%B0%83%E7%94%A8.md)
        - [ ] 对业务方法加锁 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/07-%E5%AF%B9%E4%B8%9A%E5%8A%A1%E6%96%B9%E6%B3%95%E5%8A%A0%E9%94%81.md)
        - [ ] 子类调用父类的同步方法 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/09-%E5%AD%90%E7%B1%BB%E8%B0%83%E7%94%A8%E7%88%B6%E7%B1%BB%E7%9A%84%E5%90%8C%E6%AD%A5%E6%96%B9%E6%B3%95.md)
        - [ ] 一个同步方法是不是可以调用另一个同步方法.md [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/08-%20%E4%B8%80%E4%B8%AA%E5%90%8C%E6%AD%A5%E6%96%B9%E6%B3%95%E6%98%AF%E4%B8%8D%E6%98%AF%E5%8F%AF%E4%BB%A5%E8%B0%83%E7%94%A8%E5%8F%A6%E4%B8%80%E4%B8%AA%E5%90%8C%E6%AD%A5%E6%96%B9%E6%B3%95.md)
        - [ ] 出现异常时，锁释放 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/010-%E5%87%BA%E7%8E%B0%E5%BC%82%E5%B8%B8%E6%97%B6%EF%BC%8C%E9%94%81%E9%87%8A%E6%94%BE.md)
        - [ ] volatile [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/011-volatile.md)
        - [ ] 使用 synchronized 和 volatile 的区别 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/012-%E4%BD%BF%E7%94%A8synchronized%20%E5%92%8Cvolatile%E7%9A%84%E5%8C%BA%E5%88%AB.md)
        - [ ] 使用 synchronized 解决 上面的问题 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/013-%E4%BD%BF%E7%94%A8Synchronized%E8%A7%A3%E5%86%B3012%E7%9A%84%E9%97%AE%E9%A2%98.md)
        - [ ] 使用 AtomXXX 类 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/014-%E4%BD%BF%E7%94%A8AtomXXX%E7%B1%BB.md)
        - [ ] 避免将锁定对象改为另一个对象 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/016-%E9%81%BF%E5%85%8D%E5%B0%86%E9%94%81%E5%AE%9A%E5%AF%B9%E8%B1%A1%E6%94%B9%E4%B8%BA%E5%8F%A6%E4%B8%80%E4%B8%AA%E5%AF%B9%E8%B1%A1.md)
        - [ ] synchronized优化.md [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/015-synchronized%E4%BC%98%E5%8C%96.md)
        - [ ] 不要以字符串作为锁的对象 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/017-%E4%B8%8D%E8%A6%81%E4%BB%A5%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%BD%9C%E4%B8%BA%E9%94%81%E7%9A%84%E5%AF%B9%E8%B1%A1.md)
        - [ ] 曾经的面试题 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/018-%E6%9B%BE%E7%BB%8F%E7%9A%84%E9%9D%A2%E8%AF%95%E9%A2%98.md)
        - [ ] 使用 wait 和 notify [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/019-%E4%BD%BF%E7%94%A8wait%E5%92%8Cnotify.md)
        - [ ] 使用 await 和 countdown [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/020-%E4%BD%BF%E7%94%A8await%E5%92%8Ccountdown.md)
    - 其他
        - [ ] sleep() 与 wait() 区别 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/023-%E5%85%B6%E4%BB%96.md#sleep-%E4%B8%8E-wait-%E5%8C%BA%E5%88%AB)
        - [ ] start() 与 run() 区别 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/023-%E5%85%B6%E4%BB%96.md#start-%E4%B8%8E-run-%E5%8C%BA%E5%88%AB)
        - [ ] 为什么使用 Exextor 框架 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/023-%E5%85%B6%E4%BB%96.md#%E4%B8%BA%E4%BB%80%E4%B9%88%E4%BD%BF%E7%94%A8-exextor-%E6%A1%86%E6%9E%B6)
        - [ ] Executor 和 Executors 区别 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/023-%E5%85%B6%E4%BB%96.md#executor-%E5%92%8C-executors-%E5%8C%BA%E5%88%AB)
        
        
        
- Java 异常
    - [ ] 异常的抛出 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/6-%E5%BC%82%E5%B8%B8/00-%E5%BC%82%E5%B8%B8.md#%E5%BC%82%E5%B8%B8%E7%9A%84%E6%8A%9B%E5%87%BA)
    - [ ] 异常的分类 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/6-%E5%BC%82%E5%B8%B8/00-%E5%BC%82%E5%B8%B8.md#%E5%BC%82%E5%B8%B8%E7%9A%84%E5%88%86%E7%B1%BB)
    - [ ] Throw 和 throws 的区别 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/6-%E5%BC%82%E5%B8%B8/00-%E5%BC%82%E5%B8%B8.md#throw-%E5%92%8C-throws-%E7%9A%84%E5%8C%BA%E5%88%AB)
    - [ ] 自定义异常 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/6-%E5%BC%82%E5%B8%B8/00-%E5%BC%82%E5%B8%B8.md#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%BC%82%E5%B8%B8)
    - [ ] 异常的捕获和处理 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/6-%E5%BC%82%E5%B8%B8/00-%E5%BC%82%E5%B8%B8.md#%E5%BC%82%E5%B8%B8%E7%9A%84%E6%8D%95%E8%8E%B7%E5%92%8C%E5%A4%84%E7%90%86)
    - [ ] Error 和 Exception 的区别？[代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/6-%E5%BC%82%E5%B8%B8/00-%E5%BC%82%E5%B8%B8.md#error-%E5%92%8C-exception-%E7%9A%84%E5%8C%BA%E5%88%AB)
    - [ ] try{} 里有一个 return 语句，那么紧跟在这个 try 后的 finally{} 里的代码会不会被执行，什么时候被执行，在 return 前还是后？[代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/6-%E5%BC%82%E5%B8%B8/00-%E5%BC%82%E5%B8%B8.md#try-%E9%87%8C%E6%9C%89%E4%B8%80%E4%B8%AA-return-%E8%AF%AD%E5%8F%A5%E9%82%A3%E4%B9%88%E7%B4%A7%E8%B7%9F%E5%9C%A8%E8%BF%99%E4%B8%AA-try-%E5%90%8E%E7%9A%84-finally-%E9%87%8C%E7%9A%84%E4%BB%A3%E7%A0%81%E4%BC%9A%E4%B8%8D%E4%BC%9A%E8%A2%AB%E6%89%A7%E8%A1%8C%E4%BB%80%E4%B9%88%E6%97%B6%E5%80%99%E8%A2%AB%E6%89%A7%E8%A1%8C%E5%9C%A8-return-%E5%89%8D%E8%BF%98%E6%98%AF%E5%90%8E)

- Java IO
    - [ ] 获得目录下的所有文件 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/04-IO%E7%B1%BB.md)
    - [ ] 获得目录下的指定扩展名的文件 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/04-IO%E7%B1%BB.md#%E8%8E%B7%E5%BE%97%E7%9B%AE%E5%BD%95%E4%B8%8B%E7%9A%84%E6%8C%87%E5%AE%9A%E6%89%A9%E5%B1%95%E5%90%8D%E7%9A%84%E6%96%87%E4%BB%B6)
    - [ ] 输入流 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/04-IO%E7%B1%BB.md#%E8%BE%93%E5%85%A5%E6%B5%81)
    - [ ] 输出流 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/04-IO%E7%B1%BB.md#%E8%BE%93%E5%87%BA%E6%B5%81)
    - [ ] 缓冲流 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/04-IO%E7%B1%BB.md#%E7%BC%93%E5%86%B2%E6%B5%81)
    - [ ] StringBuffer常用方法 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/04-IO%E7%B1%BB.md#stringbuffer%E5%B8%B8%E7%94%A8%E6%96%B9%E6%B3%95%E7%94%B1%E4%BA%8Estringbuffer%E5%92%8Cstringbuilder%E5%9C%A8%E4%BD%BF%E7%94%A8%E4%B8%8A%E5%87%A0%E4%B9%8E%E4%B8%80%E6%A0%B7)
    - [ ] String 和 StringBuilder、StringBuffer 的区别 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/04-IO%E7%B1%BB.md#string-%E5%92%8C-stringbuilderstringbuffer-%E7%9A%84%E5%8C%BA%E5%88%AB)

- 时间 
    - [ ] 如何取得年月日、小时分钟秒 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/07.%E6%97%B6%E9%97%B4.md#%E5%A6%82%E4%BD%95%E5%8F%96%E5%BE%97%E5%B9%B4%E6%9C%88%E6%97%A5%E5%B0%8F%E6%97%B6%E5%88%86%E9%92%9F%E7%A7%92)  
    - [ ] 如何取得从1970年1月1日0时0分0秒到现在的毫秒数 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/07.%E6%97%B6%E9%97%B4.md#%E5%A6%82%E4%BD%95%E5%8F%96%E5%BE%97%E4%BB%8E1970%E5%B9%B41%E6%9C%881%E6%97%A50%E6%97%B60%E5%88%860%E7%A7%92%E5%88%B0%E7%8E%B0%E5%9C%A8%E7%9A%84%E6%AF%AB%E7%A7%92%E6%95%B0)
    - [ ] 如何取得某月的最后一天 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/07.%E6%97%B6%E9%97%B4.md#%E5%A6%82%E4%BD%95%E5%8F%96%E5%BE%97%E6%9F%90%E6%9C%88%E7%9A%84%E6%9C%80%E5%90%8E%E4%B8%80%E5%A4%A9)
    - [ ] 如何格式化日期 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/07.%E6%97%B6%E9%97%B4.md#%E5%A6%82%E4%BD%95%E6%A0%BC%E5%BC%8F%E5%8C%96%E6%97%A5%E6%9C%9F)
    - [ ] 打印昨天的当前时刻 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/07.%E6%97%B6%E9%97%B4.md#%E6%89%93%E5%8D%B0%E6%98%A8%E5%A4%A9%E7%9A%84%E5%BD%93%E5%89%8D%E6%97%B6%E5%88%BB)


- 其他
    - [ ] 浅拷贝和深拷贝 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/01-%E6%B5%85%E6%8B%B7%E8%B4%9D%E5%92%8C%E6%B7%B1%E6%8B%B7%E8%B4%9D.md)
    - [ ] awaitility [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/0-%E5%9F%BA%E7%A1%80/03-awaitility.md)

      
## 数据结构

- 数组
    - 数组是一种效率最高的存储和随机访问对象引用序列的方式
    - [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/015-%E6%95%B0%E7%BB%84.md)
        - [ ] 数组初始化
        - [ ] [ ] —— 访问数组中的元素
        - [ ] length  —— 访问数组的长度（注意是数组的大小，不是实际保存的元素个数）
        - [ ] Arrays.toString() —— 将数组转换为String
        - [ ] Arrays.fill() —— 给数组填充值
        - [ ] Arrays.equals() —— 比较两个数组是否相等；相等的条件是：元素个数必须相等，并且对应位置的元素也相等
        - [ ] Arrays.sort() —— 数组排序
        - [ ] Arrays.binarySearch() —— 在排好序的数组中查找元素
        - [ ] System.arraycopy() —— 复制数组；参数：源数组，从源数组什么位置开始复制，目标数组，从什么位置开始复制，需要复制的个数
        - [ ] Arrays.asList() —— 接收一个数组或是一个用逗号分隔的元素列表（使用可变参数），并将其转为一个List对象    

- 动态数组
    - 实现一个可自动调整大小的动态数组
    - [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/011-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AAArrayList.md)
        - [ ] size() —— 数组元素的个数
        - [ ] capacity() —— 可容纳元素的个数
        - [ ] is_empty()
        - [ ] at(index) —— 返回对应索引的元素，索引越界报错
        - [ ] push(item)
        - [ ] insert(index, item) —— 在指定索引中插入元素，并把后面的元素依次后移
        - [ ] prepend(item) —— 可以使用上面的 insert 函数，传参 index 为 0
        - [ ] pop() —— 删除在数组末端的元素，并返回其值
        - [ ] delete(index) —— 删除指定索引的元素，并把后面的元素依次前移
        - [ ] remove(item) —— 删除指定值的元素，并返回其索引（即使有多个元素）
        - [ ] find(item) —— 寻找指定值的元素并返回其中第一个出现的元素其索引，若未找到则返回 -1
        - [ ] resize(new_capacity) // 私有函数
            - 若数组的大小到达其容积，则变大一倍
            - 获取元素后，若数组大小为其容积的1/4，则缩小一半
- 栈 
    - [ ] 先进后出 
    - [ ] [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/08-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E6%A0%88.md)

- 队列
    - [ ] 先进先出 有序
    - [ ] 普通队列 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/012-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E9%98%9F%E5%88%97.md)     
        - enqueue(value) —— 在可容的情况下添加元素到尾部
        - dequeue() —— 删除最早添加的元素并返回其值
        - empty()
        - full()
    - [ ] 环形队列 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/012-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E9%98%9F%E5%88%97.md#%E5%AE%9E%E7%8E%B0%E7%8E%AF%E5%BD%A2%E9%98%9F%E5%88%97)
        

- 链表
    - 特点：新增和删除更加高效
    - 单向链表 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md) 
    - 统计单链表中有效节点的个数 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md#%E7%BB%9F%E8%AE%A1%E5%8D%95%E9%93%BE%E8%A1%A8%E4%B8%AD%E6%9C%89%E6%95%88%E8%8A%82%E7%82%B9%E7%9A%84%E4%B8%AA%E6%95%B0)
    - 查找单链表中的倒数第k个节点[代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md#%E6%9F%A5%E6%89%BE%E5%8D%95%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACk%E4%B8%AA%E8%8A%82%E7%82%B9sina)
    - 单链表的反转 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md#%E5%8D%95%E9%93%BE%E8%A1%A8%E7%9A%84%E5%8F%8D%E8%BD%ACtencent)
    - 从尾到头打印单链表 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md#%E4%BB%8E%E5%B0%BE%E5%88%B0%E5%A4%B4%E6%89%93%E5%8D%B0%E5%8D%95%E9%93%BE%E8%A1%A8baidu)
    - 双向链表 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/010-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8F%8C%E5%90%91%E9%93%BE%E8%A1%A8.md)

- 哈希表
    - [ ] 创建 HashMap 对象 `HashMap<String,Integer> hashMap = new HashMap<>();`
    - [ ] 添加键值对 `hashMap.put("a",1);` 
    - [ ] 删除键值对 `hashMap.remove("a",5);`
    - [ ] 获取key 的 value `hashMap.get("cc");`
    - [ ] 判断 key 是否存在 `hashMap.containsKey("bb")'
    - [ ] 获得 key 的集合 `hashMap.keySet()`
    - [ ] 获得 key-value 的集合 `hashMap.entrySet();`
    - [ ] 替换 key 的 value `hashMap.replace("ff".5);`
    - [ ] 元素遍历 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/015-Map.md)


## 排序

- 实现各种排序 & 知道每种排序的最坏、最好和平均的复杂度分别是什么场景:
- 不要用冒泡排序 
    - [ ] 选择排序 [代码位置]()
    - [ ] 冒泡排序 [代码位置]()
    - [ ] 插入排序 [代码位置]()
    - [ ] 希尔排序 [代码位置]()
    - [ ] 归并排序 [代码位置]()
    - [ ] 快排 [代码位置]()
    
    
## 其他知识

- 递归（Recursion）
    - [ ] 计算阶乘 [代码位置]()
    - [ ] 斐波拉契数列 [代码位置]()
    - [ ] 爬楼梯 [代码位置]()  
            
- TCP / IP
    - [ ] 模型：访问层、网络层、传输层、应用层
    - [ ] 三次握手
    - [ ] 四次挥手
    
- HTTP
    - [ ] HTTP 是无状态的协议，无状态是指客户端与服务器之间不需要建立持久的连接。意味着客户端发起请求，服务器处理请求并响应，连接就关闭了
    - [ ] 传输过程
    
- HTTPS
    - [ ] 在 HTTP 上增加了 SSL 层，端口号是443
      
    
## Spring 

- 常用注解
    - [ ] @Controller 标注控制层组件 分发处理器将会扫描使用了这个注解的类里的方法，并检测方法是否使用了@RequestMapping注解
    - [ ] @RestController @Controller 和 @responseBody 组合
    - [ ] @Component 通用组件，表示这个类被 Spring 管理
    - [ ] @Repository  注解 dao 层
    - [ ] @Service 标注业务服务层组件
    - [ ] @responseBody  将@Controller 方法返回的对象，通过 HttpMessageConverter 转换为指定格式，写入到 Response 对象的 body 数据区，一般类型为 json 或  xml 等
    - [ ] @RequestMapping 用于类和方法，用于类时表示所有请求的父路径
    - [ ] @Autowired 自动装配注入某个类
    - [ ] @PathVariable  从路径中获得参数
    - [ ] @requestParam 定义参数
    - [ ] @RequestHeader 获得请求头
    - [ ] @SessionAttributes 将值写到 session 作用域中
    - [ ] @Valid 实体数据校验，可以结合 hibernate validator 一起使用
    - [ ] @CookieValue 用来获取Cookie中的值

    
## MyBatis 

- 知识点
    - [ ] `#{}` 和 `${}` 的区别是什么？ 
    - [ ] 实体类中的属性名和表中字段名不一样
    - [ ] 模糊查询 like 语句该怎么写
    - [ ] Mapper 接口的工作原理
    - [ ] Mapper 接口的方法参数不同时方法是否能重载
    - [ ] Mybatis 是如何将 sql 执行结果封装为目标对象并返回的？都有哪些映射方式？
    - [ ] 如何执行批量插入
    - [ ] 如何获取自动生成的主键值
    - [ ] 在 mapper 中如何传递多个参数
    - [ ] Mybatis 动态 sql 有什么用？执行原理？有哪些动态 sql
    - [ ] xml 映射文件中，除了常见的slect | insert | update | delete 标签之外，还有哪些标签？
    - [ ] Mybatis 的 xml 映射文件中，不同的 xml 映射文件，id 是否可以重复？
    - [ ] 一对一、一对多的关联查询？
    - [ ] MyBatis 实现一对一有几种方式？具体怎么操作？
    - [ ] Mybatis 实现一对多有几种方式，怎么操作的？
    - [ ] Mybatis 接口绑定？有哪些实现方式？
    - [ ] 使用 MyBatis 的 mapper 接口调用时有哪些要求？
    - [ ] Mapper 接口绑定方式？
        
## 测试相关的知识

- 测试包含点
    - [通过举例说明（文章）](https://github.com/xingyuexingyue/xingyue/blob/master/%E6%B5%8B%E8%AF%95%E7%9F%A5%E8%AF%86%E5%9F%BA%E7%A1%80/%E6%B5%8B%E8%AF%95%E5%AE%9E%E4%BE%8B.md#%E5%8A%9F%E8%83%BD%E6%80%A7%E6%B5%8B%E8%AF%95)
    - [ ] 界面测试 
    - [ ] 用户易用性测试
    - [ ] 功能性测试
    - [ ] 兼容测试率
    - [ ] 压力测试
    - [ ] 性能测试
    - [ ] APP新老版本兼容
- 测试流程有哪些
    - [ ] 1.需求评审
    - [ ] 2.需求评审后集中有问题的地方与产品私下后交流
    - [ ] 3.用例编写
        - 功能测试用例（由测试人员编写及执行，区分不同的优先级，执行的时候优先高优先级）
        - 冒烟测试（由开发人员编写及执行，在提测前执行） 
        - 接口测试用例（编写代码，由测试人员编写及执行，在功能测试前执行）
    - [ ] 4.提测后
        - 首轮用例执行（提交bug，并处理修改后的bug）
        - 二轮测试（针对重要的功能、重要的业务流程、及有bug的地方、一轮因为有bug没有执行的用例再次执行）
        - 三轮测试 (回归老的功能、兼容性测试、针对新功能的重要的功能、流程，整体重要的业务流程)
    - [ ] 5.上线前checklist
    - [ ] 6.上线
        - 通知开发上线，先上预环境（先上后端再上前端）（上线后对新老功能进行回归）
        - 通知开发上正式线上（上线后对新老功能回归、最好有回归的checklist，需要用外网）
- 如何开展一个性能测试
    - [ ] [JMeter实现多用户并发功能测试(文章)](https://github.com/xingyuexingyue/xingyue/blob/master/%E5%B7%A5%E5%85%B7/Jmeter.md)

- 一些工具
    - charles 
        - [ ] [charles(文章)](https://github.com/xingyuexingyue/xingyue/blob/master/%E5%B7%A5%E5%85%B7/Charles.md)
        - 常用到的用法
            - [ ] BreakPoints修改请求参数和响应数据
            - [ ] 映射远程地址 Map Remote
            - [ ] Throttle Setting修改网络连接
            - [ ] SSL Proxying 抓包HTTPS
            - [ ] Edit 修改请求内容
            - [ ] Map Local 接口重定向
            - [ ] 是将某个网络请求重定向到另一个网络请求
    - [ ] fiddler
    - [ ] postman 接口测试工具
    - [ ] swagger 接口管理工具，集成swagger扫描所有controller的url，方便直接通过url测试，返回json
    - [ ] sonar 代码静态扫描工具
    - [ ] Jmeter 性能测试工具
    - [ ] Monkey app随机自动点工具，用来暴力测试，稳定性测试
    - [ ] jenkins 实现持续集成化，可应用到接口，定时执行接口用例，或每次更新代码触发执行

- 接口测试
    - 接口测试的常用方法
    - 测试中会用到一些jar包
        - Java
            - [ ] testng
            - [ ] junnit
            - [ ] springtest
            - [ ] httpClient
        - python
            - [ ] unniest
- 消息队列测试
    - [ ] 被测应用为生产者
    - [ ] 被测应用消费者
    - [ ] 异常场景
            
- 测试中常用到的一些脚本
    - [ ] 快速生成测试数据及管理
    - [ ] 处理文本
    - [ ] 处理excel
    
- 微服务下的测试
    - [ ] mock 
    - [ ] 使用dubbo mock请求方的响应数据  
    
- 练习
    - [ ] 一个完整的CURD项目 [](https://github.com/xingyuexingyue/SSM-CURD)
        - spring+springmvc+mybaits+bootstrap+mysql
       

## 相关课程视频资源

- [ ] [Dubbo ](https://www.bilibili.com/video/av62353311/?pikaqiu)

- [ ] [Spring ](https://www.bilibili.com/video/av59570922/?pikaqiu)

- [ ] [SpringMVC ](https://www.bilibili.com/video/av59567541/?pikaqiu)

- [ ] [SpringBoot ](https://www.bilibili.com/video/av59572480/?pikaqiu)

- [ ] [MyBatis ](https://www.bilibili.com/video/av59564271/?pikaqiu)

- [ ] [rocketmq](https://www.bilibili.com/video/av11074519)

- [ ] [RabbitMQ](https://www.imooc.com/learn/1042)

- [ ] [消息队列 Kafka ]()

- [ ] [Redis入门](https://www.imooc.com/learn/839)

- [ ] [MySQL](https://www.bilibili.com/video/av59623481/?pikaqiu)

- [ ] [Elasticsearch](https://www.bilibili.com/video/av59628430/?pikaqiu)

- [ ] [Git](https://www.bilibili.com/video/av59634634/?pikaqiu)

- [ ] [Nginx](https://www.bilibili.com/video/av59639498/?pikaqiu)

- [ ] [单链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=16) 

- [ ] [双向链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=24)

- [ ] [环形链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=27)
    
- [ ] [使用数组实现队列（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=10)

- [ ] [使用数组实现栈（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=30)   
- [ ] [使用数组实现环形队列](https://www.bilibili.com/video/BV16t411g7wa?p=10)     