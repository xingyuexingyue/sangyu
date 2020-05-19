volatile关键字，使一个变量在多个线程间可见。

A B线程都用到一个变量，java默认是A线程中保留一份copy，这样如果B线程修改了该变量，则A线程未必知道

使用volatile关键字，会让所有线程都会读到变量的修改值

在下面的代码中，running是存在于堆内存的t对象中
当线程t1开始运行的时候，会把running值从内存值从内存中读到t1线程的工作区，在运行过程中直接使用这个copy，并不会每次都去读堆内存，这样，当主线程修改running的值之后，t1线程感知不到，所以不会停止

使用volatile关键字之后，将会强制所有线程都去堆内存中读取running的值

volatile并不能保证多个线程共同修改running变量时所带来的不一致问题，也就是说volatile不能替代synchronized

```java
package com.sangyu.test.test23;

/**
 * User: pengyapan
 * Date: 2020/3/26
 * Time: 下午7:26
 */
public class Test12 {
    volatile boolean running = true; // 对比有无volatile的情况下，整个程序运行结果的区别
    void m(){
        System.out.println("m start");
        while (running){

        }
        System.out.println("m end!");
    }

    public static void main(String[] args) {
        Test12 test12 = new Test12();
        new Thread(new Runnable() {
            @Override
            public void run() {
                test12.m();
            }
        }).start();

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        test12.running = false;
    }
}
```

JMM中主内存，每个线程有自己的内存（线程存放自己变量的内存还有CPU的缓冲），如果线程，就会有多个缓冲区，每个线程会把主内存里的东西读取来到自己的缓冲区，CPU在处理的时候就不去主内存里读这个内存了。这个时候其他线程在修改后，更新到主内存，但是的第一个线程并没有去主内存里取读

加了volatile后，增加线程间的可见性，主内存的发生改变的后，会通知其他线程所有缓冲区，你们内存的内容过期了，需要去主内容重新读取更新。

没有volatile ，在run中增加sleep，上面的问题会没有了

![](https://upload-images.jianshu.io/upload_images/2765653-61466e389741098e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

产生的原因是，在run中增加语句后，CPU改变原来一直执行的状态，此时产生了空闲，有可能去主线程刷新下内容。所以会访问到。

但是为了保证线程间的可见性，需要使用volatile。需要对两个线程共同访问的变量增加volatile。 不用volatile也可以使用synchronized语法，volatile比synchronized效率要高。用volatile的是时候就不要加锁

synchronized 即保证了可见性有保证了原子性