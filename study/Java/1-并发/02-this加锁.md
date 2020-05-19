```java
package com.sangyu.test.test23;

/**
 * User: pyp
 * Date: 2020/3/26
 * Time: 下午4:16
 */
public class Test04 {
    private int count = 10;
    public void m(){
        synchronized (this){ // 任何线程在要执行下面的代码时，必须要先拿到this的锁
            count--;
            System.out.println(Thread.currentThread().getName() + " count = " + count);
        }
    }
}
```