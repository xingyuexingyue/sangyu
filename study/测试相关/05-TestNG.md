## 一. TestNG的HelloWorld
1. 创建一个maven项目
2. pom.xml中注入TestNG的依赖
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.sangyu</groupId>
    <artifactId>my-testng</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <!-- https://mvnrepository.com/artifact/org.testng/testng -->
        <dependency>
            <groupId>org.testng</groupId>
            <artifactId>testng</artifactId>
            <version>7.1.0</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>
```
3. 此时项目的目录结构

![](https://upload-images.jianshu.io/upload_images/2765653-4bacdb0db6d8876d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. 在java下创建包并在包下创建一个测试类

![](https://upload-images.jianshu.io/upload_images/2765653-748405aa91615225.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. 在TestAnnotation类下新建一个测试方法，代码如下：

```
package com.sangyu.test;

import org.testng.annotations.Test;

/**
 * User: pengyapan
 * Date: 2020/4/10
 * Time: 下午9:32
 */
public class TestAnnotation {
    @Test // 这里使用到了一个注解，用来标识这是一个测试用例
    public void testCase1(){
        System.out.println("case01");
    }
}
```
6. 运行测试用例

![](https://upload-images.jianshu.io/upload_images/2765653-2dfb6ba46dfc82fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 二. TestNG支持的注释列表

| 注解| 描述|
|--|--|
| @BeforeSuite|  注解的方法只运行一次，运行当前套件所有测试前 |
|@AfterSuite  | 注解的方法只运行一次，运行当前套件所有测试之后 |
| @BeforeClass| 注解的方法只运行一次，在调用当前类的第一个测试方法之前运行 |
| @AfterClass| 注解的方法只运行一次，在调用当前类的第一个测试方法之后 |
| @BeforeTest|在所有测试方法之前运行 |
|@AfterTest | 在所有测试方法之后运行 |
|@BeforeGroups |配置方法将在运行组列表之前运行 |
| @AfterGroups|配置方法将在运行组列表之前运行 |
| @BeforeMethod| 注释方法将在每个测试方法之前运行|
| @AfterMethod| 注释方法将在每个测试方法之后运行|
| @DataProvider| 标记一种方法来提供测试方法的数据，被注释的方法将返回一个Object[][]|
|@Factory | 将一个方法标记为工厂，返回TestNG将被用作测试类的对象。 该方法必须返回Object []|
| @Listeners| 定义测试类上的侦听器|
| @Parameters|描述如何将参数传递给方法
| @Test| 将类或方法标记为测试的一部分|

## 三. @BeforeSuite和@AfterSuite的用法

- **@BeforeSuite** 在test suite中的所有test运行之前运行，只运行一次；
- **@AfterSuite** 在test suite中的所有test运行之后运行，只运行一次。

**应用场景：**将通用的功能抽取并封装起来，在方法中使用注解@BeforeSuite和@AfterSuite，在测试类中继承这个类，测试类在运行前会先运行@BeforeSuite注解的方法，测试类在运行后会运行@AfterSuite注解的方法

**testng.xml**

```
<!--管理测试类-->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<!-- allow-return-values 默认值为FALSE,表示返回值将被忽略 -->
<suite name="framework_testng" allow-return-values="true">
    <test verbose="2" name="TestMethods">
        <classes>
            <class name="com.sangyu.suitetest.TestNGClass1"></class>
            <class name="com.sangyu.suitetest.TestNGClass2"></class>
        </classes>
    </test>
</suite>
```
**BaseTestSuite.java**
```
package com.sangyu.suitetest;

import org.testng.annotations.AfterClass;
import org.testng.annotations.AfterSuite;
import org.testng.annotations.BeforeClass;
import org.testng.annotations.BeforeSuite;

/**
 * User: pengyapan
 * Date: 2020/4/12
 * Time: 上午10:39
 */

public class BaseTestSuite {
    @BeforeSuite
    public void beforeSuite(){
        System.out.println("*BaseTestSuite类：@beforeSuite");
    }
    @AfterSuite
    public void afterSuite(){
        System.out.println("*BaseTestSuite类：@afterSuite");
    }
    @BeforeClass
    public void beforeClass(){
        System.out.println("*BaseTestSuite类：@BeforeClass");
    }
    @AfterClass
    public void afterClass(){
        System.out.println("*BaseTestSuite类：@AfterClass");
    }
}
```

**TestNGClass1.java**
```
package com.sangyu.suitetest;

import org.testng.annotations.*;

/**
 * User: pengyapan
 * Date: 2020/4/12
 * Time: 上午10:40
 */
public class TestNGClass1 extends BaseTestSuite{
    @BeforeClass
    public void setUp(){
        System.out.println("#TestNGClass1类：@BeforeClass");
    }
    @AfterClass
    public void tearDown(){
        System.out.println("#TestNGClass1类：@AfterClass");
    }
    @BeforeMethod
    public void beforeMethod() {
        System.out.println("#TestNGClass1类： @BeforeMethod");
    }
    @AfterMethod
    public void afterMethod() {
        System.out.println("#TestNGClass1类：@AfterMethod");
    }
    @Test
    public void testAdd(){
        System.out.println("#TestNGClass1类：@Test11111");
    }
    @Test
    public void testMethod(){
        System.out.println("#TestNGClass1类：@Test22222");
    }
}
```
**TestNGClass2.java**
```
package com.sangyu.suitetest;

import org.testng.annotations.*;

/**
 * User: pengyapan
 * Date: 2020/4/12
 * Time: 上午10:40
 */

public class TestNGClass2 extends BaseTestSuite{
    @BeforeClass
    public void setUp(){
        System.out.println("#TestNGClass2类：@BeforeClass");
    }
    @AfterClass
    public void tearDown(){
        System.out.println("#TestNGClass2类：@AfterClass");
    }
    @BeforeMethod
    public void beforeMethod() {
        System.out.println("#TestNGClass2类： @BeforeMethod");
    }
    @AfterMethod
    public void afterMethod() {
        System.out.println("#TestNGClass2类：@AfterMethod");
    }
    @Test
    public void testAdd(){
        System.out.println("#TestNGClass2类：@Test11111");
    }
    @Test
    public void testMethod(){
        System.out.println("#TestNGClass2类：@Test22222");
    }
}
```

## 四. @Factory的用法

- **@Factory** 采用工厂的方法来创建测试数据并配合完成测试

**应用场景：** @Test注解的方法，需要输入多个测试数据进行测试，并且这些测试数据可以是有一定关系(可以通过代码控制)，使用@Factory注解的方法中对要测试的类调用，这时TestNG会自动调用测试类中带有@Test注解的方法

**TestngFactory.java**
```
package com.sangyu.test;

import org.testng.annotations.Factory;

/**
 * User: pengyapan
 * Date: 2020/4/10
 * Time: 下午10:11
 */
public class TestngFactory {
    @Factory
    public Object[] createInstances() {
        Object[] result = new Object[10];
        for (int i = 0; i < 10; i++) {
            result[i] = new TestngFactoryTest(i*10);
        }
        return result;
    }
}
```

**TestngFactoryTest.java**

```
package com.sangyu.test;

import org.testng.annotations.Test;

/**
 * User: pengyapan
 * Date: 2020/4/10
 * Time: 下午10:13
 */
public class TestngFactoryTest {
    private int m_numberOfTimes;

    public TestngFactoryTest(int i) {
        this.m_numberOfTimes = i;
    }

    private static int num;

    @Test
    public void testServer() {
        num++;
        System.out.println("num  " + num + " m_numberOfTimes : " + m_numberOfTimes);
    }
}
```

## 五. @Listeners的用法

TestNG监听器就是预定义的 Java 接口。用户创建这些接口的实现类，并把它们加入到 TestNG 中，TestNG 便会在测试运行的不同时刻调用这些类中的接口方法。TestNG有多种类型的监听器，@Listeners就是其中的一种

**ITestListener** 接口中定义的方法，可以在实现类中实现， 下面例子重写了onTestStart,onTestSuccess(), onTestFailure()三个方法，其他方法先不管。

```
package org.testng;

public interface ITestListener extends ITestNGListener {
    default void onTestStart(ITestResult result) {
    }

    default void onTestSuccess(ITestResult result) {
    }

    default void onTestFailure(ITestResult result) {
    }

    default void onTestSkipped(ITestResult result) {
    }

    default void onTestFailedButWithinSuccessPercentage(ITestResult result) {
    }

    default void onTestFailedWithTimeout(ITestResult result) {
        this.onTestFailure(result);
    }

    default void onStart(ITestContext context) {
    }

    default void onFinish(ITestContext context) {
    }
}
```

**ListenerDemo.java**

```
package com.sangyu.listenertest;

import org.testng.ITestListener;
import org.testng.ITestResult;

/**
 * User: pengyapan
 * Date: 2020/4/12
 * Time: 上午10:17
 */
public class ListenerDemo implements ITestListener {

    @Override
    public void onTestStart(ITestResult iTestResult) {
        System.out.println("用例启动。" + iTestResult.toString());
    }

    @Override
    public void onTestSuccess(ITestResult iTestResult) {
        System.out.println("用例执行成功，" + iTestResult.toString());
    }

    @Override
    public void onTestFailure(ITestResult iTestResult) {
        System.out.println("用例运行失败，启动截图。");
    }
}
```
**MyTest.java**
```
package com.sangyu.listenertest;

import org.testng.Assert;
import org.testng.annotations.Listeners;
import org.testng.annotations.Test;

/**
 * User: pengyapan
 * Date: 2020/4/12
 * Time: 上午10:25
 */
@Listeners(ListenerDemo.class)
public class MyTest {
    @Test
    public void testListener() {
        System.out.println("run test");
    }

    @Test
    public void testListener1() {
        System.out.println("runnnnnnn test");
    }

    @Test
    public void listenerExampletest() {
        Assert.assertTrue(11 == 10);
    }
}
```

## 六. @Parameters注解的用法

- **@Parameters** 给测试方法传入参数，通过xml方式

**testng.xml**

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<!-- allow-return-values 默认值为FALSE,表示返回值将被忽略 -->
<suite name="framework_testng" allow-return-values="true">
    <test verbose="2" name="TestMethods">
        <classes>
            <class name="com.sangyu.parametertest.ParameterTest"></class>
            <parameter name="name" value="Lily"></parameter>
            <parameter name="age" value="11"></parameter>
        </classes>
    </test>
</suite>
```
**ParameterTest.java**
```
package com.sangyu.parametertest;

import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

/**
 * User: pengyapan
 * Date: 2020/4/12
 * Time: 下午2:07
 */
public class ParameterTest {

    @Test
    @Parameters({"name","age"})
    public void test01(String name,int age){
        System.out.println("name = " + name +"; age= " + age);
    }
}
```

## 七. @DataProvider注解的用法

- **@DataProvider** 给测试方法传入参数

```
package com.sangyu.parametertest;

import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

/**
 * User: pengyapan
 * Date: 2020/4/12
 * Time: 下午2:12
 */
public class DataProviderTest {

    @Test(dataProvider = "data")
    public void testDataProvider(String name,int age){
        System.out.println("name = " + name + "; age = " + age);
    }

    @DataProvider(name="data")
    public Object[][] providerData(){
        Object[][] o = new Object[][]{
                {"abc",22},
                {"bdc",11},
                {"dce",33}
        };
        return o;
    }
}
```

**通过不同的方法传递不同的参数**

```
package com.sangyu.parametertest;

import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

import java.lang.reflect.Method;

/**
 * User: pengyapan
 * Date: 2020/4/12
 * Time: 下午2:12
 */
public class DataProviderTest {
    @Test(dataProvider = "anotherData")
    public void test01(String name, int age) {
        System.out.println(" test01 name = " + name + "; age = " + age);
    }

    @Test(dataProvider = "anotherData")
    public void test02(String name, int age) {
        System.out.println(" test02 name = " + name + "; age = " + age);
    }
    @DataProvider(name = "anotherData")
    public Object[][] anotherDataTest(Method method) {

        Object[][] o = null;
        if (method.getName().equals("test01")) {
            o = new Object[][]{
                    {"abc", 22},
                    {"bdc", 11},
                    {"dce", 33}

            };
        } else if (method.getName().equals("test02")) {

            o = new Object[][]{
                    {"xyz", 22},
                    {"hhhhh", 11},
            };
        }
        return o;
    }
}
```

## 八. @Test注解的属性列表

| 属性名| 功能  |
|--|--|
|  timeout  | 超时测试，单位为毫秒  |
| dependsOnMethods | 依赖测试，本个测试方法执行的时候依赖于其它方法   |
| expectedExceptions | 异常测试，结果为某一个异常   |
| enabled=false | 忽略测试，本次测试执行中不想要执行的测试方法，默认true  |

#### 8.1 timeout 属性的用法

下面的例子中，test07要在3000毫秒内给予响应，否则抛出异常。使用sleep使当前线程休眠2000ms后执行。
```
    @Test(timeOut = 3000)
    public void test07() throws InterruptedException {
        Thread.sleep(2000);
        System.out.println("test07");
    }
```
#### 8.2 dependsOnMethods 属性的用法

下面例子中，test06方法的执行要依赖test05先执行后才能运行，如果test05失败，test06不再执行
```
public class MyTest {

    @Test
    public void test05(){
        System.out.println("test05");
        throw new RuntimeException(); // 如果此方法抛出异常，则依赖这个test05的方法将不会在执行
    }

    @Test(dependsOnMethods = {"test05"})
    public void test06(){
        System.out.println("test06");
    }

}
```
#### 8.3 expectedExceptions 属性的用法

在下面例子中test03的运行结果将会是一个异常

```
public class MyTest {
    @Test(expectedExceptions = RuntimeException.class)
    public void test03() {
        System.out.println("test03");
    }

    @Test(expectedExceptions = RuntimeException.class)
    public void test04() {
        System.out.println("test04");
        throw new RuntimeException();
    }
}
```
#### 8.4 enabled 属性的用法

在下面例子中的两个方法test01不会执行，test02会执行

```
public class MyTest {

    @Test(enabled = false)
    public void test01(){
        System.out.println("test01");
    }

    @Test(enabled = true) 
    public void test02(){
        System.out.println("test02");
    }
}
```

## 九. 套件测试

通过创建一个xml文件，比如testng.xml管理要执行的测试类。

suite标签管理一个测试套件，test标签管理一个测试组，classes标签管理多个测试类，class标签标示每一个测试类。每个测试套件suite下可以包含多个test，每个test下有一个classes，每个classes下可以有多个class。然后再去执行这个xml文件就可以了

**BaseTestSuite.java**
```
public class BaseTestSuite {
    @BeforeSuite
    public void beforeSuite(){
        System.out.println("*BaseTestSuite类：@beforeSuite");
    }
    @AfterSuite
    public void afterSuite(){
        System.out.println("*BaseTestSuite类：@afterSuite");
    }
    @BeforeClass
    public void beforeClass(){
        System.out.println("*BaseTestSuite类：@BeforeClass");
    }
    @AfterClass
    public void afterClass(){
        System.out.println("*BaseTestSuite类：@AfterClass");
    }
}
```
**LoginTest.java**

```
public class LoginTest extends BaseTestSuite {
    @Test
    public void login(){
        System.out.println("login success");
    }
}
```
**PayTest.java**
```
public class PayTest extends BaseTestSuite {

    @Test
    public void paySuccess(){
        System.out.println("pay success");
    }
}
```
**testng.xml**
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
<!-- allow-return-values 默认值为FALSE,表示返回值将被忽略 -->
<suite name="framework_testng" allow-return-values="true">
    <test name="login">
        <classes>
            <class name="com.sangyu.suitetest.LoginTest"></class>
        </classes>
    </test>

    <test name="pay">
        <classes>
            <class name="com.sangyu.suitetest.PayTest"></class>
        </classes>
    </test>
</suite>
```











