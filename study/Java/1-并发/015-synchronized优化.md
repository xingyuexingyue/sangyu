同步代码块中的语句越少越好，比较下列代码中的m1和m2

```java
package com.sangyu.test.test23;

/**
 * User: pengyapan
 * Date: 2020/3/26
 * Time: 下午8:40
 */
public class Test16 {
    int count = 0;
    synchronized void m1(){
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 业务逻辑中只有下面这句需要sync，这时不应该给整个方法上锁
        count++;
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    
    synchronized void m2(){
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 业务逻辑中只有下面这句需要sync，这时不应该给整个方法上锁
        // 采用细粒度的锁，可以使线程争用时间变短，从而提高效率
        synchronized (this){
            count++;
        }
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }   
    }
}
```
