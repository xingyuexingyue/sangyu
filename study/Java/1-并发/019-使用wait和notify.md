在上面的面试题中，给lists添加volatile之后，t2能够接到通知，但是，t2线程的死循环浪费了cpu，如果不用死循环，该怎么做呢？

这里使用wait和notify，wait会释放锁，而notify不会释放锁。（sleep也不会）
需要注意的是，运用这种方法，必须要保证t2先执行，也就是首先让t2监听才可以

```java
package com.sangyu.test.test23;

import java.util.ArrayList;
import java.util.List;

/**
 * User: pengyapan
 * Date: 2020/3/26
 * Time: 下午10:01
 */
public class Test20 {
    volatile List lists = new ArrayList();
    public void add(Object o){
        lists.add(o);
    }

    public int size(){
        return lists.size();
    }

    public static void main(String[] args) {
        Test20 test20 = new Test20();
        final Object lock = new Object();

        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("t2 启动");
                if(test20.size() != 5){
                    try {
                        lock.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                System.out.println("t2 结束");
            }
        }).start();

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("t1 启动");
                synchronized (lock){
                    for(int i =0; i<10;i++){
                        test20.add(new Object());
                        System.out.println("add " + i);
                    }

                    if(test20.size() == 5){
                        lock.notify();
                    }

                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        }).start();
    }
}
```

分析：面试题中我们是volatile来解决通知所有线程变量发生变化，但是volatile会产生不精确的问题（指的是很有可能在多几个线程出来，给容器继续add，这个时候打印出来的可能就不是5了），所以我们通过加锁lock来解决这个问题

使用wait和notify必须用synchronized锁定lock，然后调用被锁定对象的wait方法和notify方法。。

假使现在有一个对象被锁定，有两个线程要访问这个对象。在第一个线程访问的过程中，条件还没有满足，我想让这个线程暂停等着，首先锁定这个对象，这个时候调用这个对象的wait方法，当前线程就进入等待状态，同时释放锁，其他线程就可以访问这个对象。什么时候这个线程可以再次启动呢，只有在调用这个对象的notify或notifyall方法，notify方法会启动一个正在这个对象等待的某一个线程，或者调用notifyall方法叫醒在这个对象上等待的所有线程（是其他线程调用，并不是正在等待的线程调用），所以一定要先启动t2线程，再启动t1线程，t2线程在wait过程中，t1满足线程后叫醒t1线程

这里还需要考虑一个问题，我们在判断中使用了if而不是while。这是因为用if是因为叫醒一次就可以执行一次关闭，

还要一个问题，为什么只有t2执行完了t1才会执行这是因为notify不释放锁（sleep也不释放锁）notify不需要指定锁由线程调度器会帮你指定一个线程运行

我们还可以在t1线程中，在增加一个wait方法，因为wait方面可以释放锁。但是我们在执行完t2后，还得使用notify通知t1，让t1继续执行直到结束，这个过程比较繁琐

![](https://upload-images.jianshu.io/upload_images/2765653-ad0f969254d1a729.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)