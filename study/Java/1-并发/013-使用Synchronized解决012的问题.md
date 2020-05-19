对比上一个程序，可以用synchronized解决，synchronized可以保证可见性和原子性，volatile只能保证可见性

```java
package com.sangyu.test.test23;

import java.util.ArrayList;
import java.util.List;

/**
 * User: pengyapan
 * Date: 2020/3/26
 * Time: 下午8:28
 */
public class Test14 {
    int count = 0;

    synchronized void m() {
        for (int i = 0; i < 10000; i++) {
            count++;
        }
    }

    public static void main(String[] args) {
        Test14 test14 = new Test14();
        List<Thread> threads = new ArrayList<>();
        for (int i = 0; i < 10; i++) {
            threads.add(new Thread(new Runnable() {
                @Override
                public void run() {
                    test14.m();
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
        System.out.println(test14.count);
    }
}
```
