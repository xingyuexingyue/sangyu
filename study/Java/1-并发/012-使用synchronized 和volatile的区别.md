volatile并不能保证多个线程共同修改running变量时所带来的不一致的问题，也就是说volatile不能替代synchronized

```java
package com.sangyu.test.test23;

import java.util.ArrayList;
import java.util.List;

/**
 * User: pengyapan
 * Date: 2020/3/26
 * Time: 下午8:16
 */
public class Test13 {
    volatile int count = 0;
    void m(){
        for(int i = 0;i<10000;i++){
            count++;
        }
    }

    public static void main(String[] args) {
        Test13 test13 = new Test13();
        List<Thread> threads = new ArrayList<>();

        for(int i = 0; i < 10;i++){
            threads.add(new Thread(new Runnable() {
                @Override
                public void run() {
                    test13.m();
                }
            }));
        }

        for (Thread thread:threads){
            thread.start();
        }

        for (Thread thread:threads){
            try {
                thread.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println(test13.count);
    }
}
// 执行结果
// 74659
// 产生这样的结果是，每个线程修改数据后会更新到主内存，主内存更新会通知其他线程重新读取主线程的数据，在这个过程，写回来的数据并不能保证是最新。只是单纯写回来
```
