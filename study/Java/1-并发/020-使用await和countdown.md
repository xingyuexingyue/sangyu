给lists增加volatile之后，t2能够接到通知，但是，t2的死循环很浪费CPU，如果不用死循环

可以使用wait和notify做到，wait会释放锁，而notify不会释放锁
需要注意的是，运用这种方法，必须先保证t2先执行（就是要监听的线程），也就是首先让t2监听才可以。

当我们使用wait和notify后，t2会执行使用wait通知t1，t1执行后使用notify通知t1，但是t1不会立刻执行，因为notify并不会释放锁，所以t1会等到t2结束后才执。

还可以使用Latch(门闩)替代wait和notify来进行通知，好处是通信方式简单，同时也可以指定等待时间。

CountDownLatch不涉及锁定，当CountDownLatch的值为零时锁释放当前线程继续运行，调用countdownm修改

CountDownLatch和 wait/notify比较，当不涉及同步，只是线程通信的时候，用synchronized + wait、notify就显得太重了，这时应该考虑CountDownLatch/cyclicabarrier/semaphore

通知门栓打开后不需要锁定对象，还可以继续往下运行


```java
package com.sangyu.test.test23;

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.CountDownLatch;
import java.util.concurrent.TimeUnit;

/**
 * User: pengyapan
 * Date: 2020/3/26
 * Time: 下午10:28
 */
public class Test21 {
    volatile List lists = new ArrayList();

    public void add(Object o) {
        lists.add(o);
    }

    public int size() {
        return lists.size();
    }

    public static void main(String[] args) {
        Test21 test21 = new Test21();
        CountDownLatch latch = new CountDownLatch(1);

        new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("t2 启动");
                if(test21.size() != 5){
                    try {
                        latch.wait(); // 门闩等待不需要锁定对象
                        // 也可以指定等待时间
                        // latch.await(5000, TimeUnit.MILLISECONDS);
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
                for(int i = 0; i < 10;i++){
                    test21.add(new Object());
                }

                if(test21.size() == 5){
                    latch.countDown(); // 打开门闩，让t2执行 ，通知门闩打开后不需要锁定对象，还可以继续执行
                }
            }
        }).start();
    }

}
```

