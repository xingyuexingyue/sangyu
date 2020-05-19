解决同样的问题的更高效的方法，使用AtomXXX类

AtomXXX 类本身方法都是原子性的，但不能保证多个方法连续调用是原子性的

```java
package com.sangyu.test.test23;

import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.atomic.AtomicInteger;

/**
 * User: pengyapan
 * Date: 2020/3/26
 * Time: 下午8:31
 */
public class Test15 {

    AtomicInteger count = new AtomicInteger(0);
    void m(){
        for(int i = 0;i<10000;i++){
            // if count.get() < 1000 // 如果用到两个AtomicInteger的方法，不加锁的还是会被其他线程打断，产生这个问题的原因是：在两个方法执行中间会可能会被其他线程打断
            count.incrementAndGet(); // count++不具备原子性，但是incrementAndGet方法具有原子性，在执行结束前其他线程不能打断它
        }
    }

    public static void main(String[] args) {
        Test15 test15 = new Test15();
        List<Thread> threads = new ArrayList<>();

        for(int i = 0; i < 10; i++){
            threads.add(new Thread(new Runnable() {
                @Override
                public void run() {
                    test15.m();
                }
            }));
        }
        for (Thread thread : threads) {
            thread.start();
        }

        for (Thread thread : threads) {
            try {
                thread.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println(test15.count);
    }
}
```
