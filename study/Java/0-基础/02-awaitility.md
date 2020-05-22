## 1.背景
在编写自动化测试用例过程中，往往会遇见被测代码有异步或者队列处理的中间过程；如果需要校验这部分结果，必须等待异步操作结束或队列消费完，而这个中间等待的时间是不确定的，常常是根据经验值设定，通过Thread.sleep(经验值)，而这个时间通常会设置成最长的那次时间，但是可能99%次这个异步操作都低于这个最长的时间，这就造成了每次执行这个测试用例都花费了异步任务最长的那次时间。

现介绍一款开源工具 awaitility: [地址](https://github.com/awaitility/awaitility)，该工具提供轮询的方式，判断操作是否完成，以最短的时间获取异步任务结果。

## 2.入门

awaitility 支持 Java、Scala、Groovy，本文以 Java 介绍。

maven 工程在 pom.xml 添加 awaitility 依赖：

```
<dependency>
    <groupId>org.awaitility</groupId>
    <artifactId>awaitility</artifactId>
    <version>2.0.0</version>
    <scope>test</scope>
</dependency>
```

其他方式，请参考：

https://github.com/awaitility/awaitility/wiki/Getting_started

## 3.实例

构造一个异步任务

```java
import java.util.concurrent.Callable;
import static java.util.concurrent.TimeUnit.*;

import static org.awaitility.Awaitility.*;
import static org.awaitility.Duration.*;
import static org.awaitility.pollinterval.FibonacciPollInterval.*;
interface CounterService extends Runnable {
    int getCount();
}
// 每隔1s, count累加1
class CounterServiceImpl implements CounterService {
    private volatile int count = 0;
    public void run() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    for(int index = 0; index < 5; index++) {
                        Thread.sleep(1000);
                        count += 1;
                    }
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                }
            }
        }).start();
    }
    public int getCount() {
        return count;
    }
}   
```

#### 3.1 默认等待时间

await().until(Callable conditionEvaluator) 最多等待10s直到 conditionEvaluator 满足条件，否则 ConditionTimeoutException。

```java
public class MyTest {

    /**
     * 测试方法
     */
    @Test
    public void testAsynchronousNormal() {
        final CounterService service = new CounterServiceImpl();
        service.run(); // 调用一个异步方法，这个方法并没有回调方法
        try {
            // 默认10s, 如果在这时间段内,条件依然不满足,将抛出ConditionTimeoutException
            await().until(new Callable<Boolean>() {
                @Override
                public Boolean call() throws Exception {
                    return service.getCount() == 5;
                }
            });
            System.out.println("成功");
        } catch (Exception e) {
            Assert.fail("测试代码运行异常：" + e.getMessage() + "，代码位置：" + e.getStackTrace()[0].toString());
        }
    }
}
```

默认超时时间为10s, 可通过 setDefaultTimeout() 自定义默认超时时间


#### 3.2 最多等待

await().atMost() 设置最多等待时间，如果在这时间内条件还不满足，将抛出 ConditionTimeoutException

```java
public class MyTest {

    /**
     * 测试方法
     */
    @Test
    public void testAsynchronousAtMost(){
        final CounterService service = new CounterServiceImpl();
        service.run();
        try{
            // 指定超时时间3s, 如果在这时间段内,条件依然不满足,将抛出ConditionTimeoutException
            await().atMost(3, SECONDS).until(new Callable<Boolean>() {
                @Override
                public Boolean call() throws Exception {
                    return service.getCount() == 5;
                }
            });
        } catch (Exception e) {
            Assert.fail("测试代码运行异常：" + e.getMessage() + "，代码位置：" + e.getStackTrace()[0].toString());
        }
    }
}
```

#### 3.3 至少等待

await().atLeast() 设置至少等待时间；多个条件时候用 and() 连接

```java
public class MyTest {

    /**
     * 测试方法
     */
    @Test
    public void testAsynchronousAtLeast(){

        final CounterService service = new CounterServiceImpl();
        service.run();

        try{
            // 指定至少1s, 最多3s, 如果在这时间段内,条件依然不满足,将抛出ConditionTimeoutException
            await().atLeast(1, SECONDS).and().atMost(3, SECONDS).until(new Callable<Boolean>() {
                @Override
                public Boolean call() throws Exception {
                    return service.getCount() == 2;
                }
            });

        } catch (Exception e) {
            Assert.fail("测试代码运行异常：" + e.getMessage() + "，代码位置：" + e.getStackTrace()[0].toString());

        }
    }
}
```

#### 3.4 forever等待

forever 等待，不推荐使用，可能导致死循环

```java
public class MyTest {

    /**
     * 测试方法
     */
    @Test
    public void testAsynchronousAtLeast(){

        final CounterService service = new CounterServiceImpl();
        service.run();

        await().forever().until(new Callable<Boolean>() {
            @Override
            public Boolean call() throws Exception {
                return service.getCount() == 6;
            }
        });
    }
}
```

#### 3.5 轮询

with().pollInterval(ONE_HUNDRED_MILLISECONDS).and().with().pollDelay(50, MILLISECONDS) that is conditions are checked after 50ms then 50ms+100ms

```java
public class MyTest {

    /**
     * 测试方法
     */
    @Test
    public void testAsynchronousPoll(){
        final CounterService service = new CounterServiceImpl();
        service.run();
        try{
            // 轮询查询,pollInterval每隔多少时间段轮询, pollDelay每次轮询间隔时间
            with().pollInterval(ONE_HUNDRED_MILLISECONDS).and().with().pollDelay(50, MILLISECONDS).await("count is greater 3").until(
                    new Callable<Boolean>() {
                        @Override
                        public Boolean call() throws Exception {
                            return service.getCount() == 4;
                        }
                    });
        } catch (Exception e) {
            Assert.fail("测试代码运行异常：" + e.getMessage() + "，代码位置：" + e.getStackTrace()[0].toString());
        }
    }
}
```

#### 3.6 Fibonacci轮询

with().pollInterval(fibonacci(SECONDS)) 非线性轮询，按照 fibonacci 数轮询

```java
public class MyTest {

    /**
     * 测试方法
     */
   @Test
   public void testAsynchronousFibonacciPoll(){
       final CounterService service = new CounterServiceImpl();
       service.run();
       try{
           // 使用fibonacci数作为间隔数1,1,2,3,5,8,..., 默认单位milliseconds         with().pollInterval(fibonacci(SECONDS)).await("count is greater 3").until(
                   new Callable<Boolean>() {
                       @Override
                       public Boolean call() throws Exception {
                           return service.getCount() == 4;
                       }
                   };
       } catch (Exception e) {
           Assert.fail("测试代码运行异常：" + e.getMessage() + "，代码位置：" + e.getStackTrace()[0].toString());
       }
   }
}
```