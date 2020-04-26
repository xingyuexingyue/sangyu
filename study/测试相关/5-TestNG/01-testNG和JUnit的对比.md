关于选择JUnit还是选testNG，这几篇文章，建议读一读：

API参考文档：

Junit API文档：http://junit.org/junit4/javadoc/latest/index.html

testng 6.11：http://www.javadoc.io/doc/org.testng/testng/6.11

testng documentation：http://testng.org/doc/documentation-main.html

 

两个框架的对比：

JUnit 4 与 TestNG 的对比：https://www.ibm.com/developerworks/cn/java/j-cq08296/index.html

JUnit vs TestNG: Which Testing Framework Should You Choose?：http://blog.takipi.com/junit-vs-testng-which-testing-framework-should-you-choose/

Java测试框架比较：TestNG VS JUnit 4：http://blog.csdn.net/jmyue/article/details/9041357
JUnit 4 与 TestNG 对比：http://www.importnew.com/16270.html

 

.....................

TestNG和JUnit是针对Java语言的两个比较常用的测试框架。JUnit出现的比较早，但是早期的JUnit 3对测试代码有非常多的限制，使用起来很不方便，后来的JUnit 4得到很大的改进。TestNG的出现介于JUnit 3和JUnit 4，但是TestNG在很多方面还要优于JUnit 4。下面从整体上对TestNG和JUnit 4进行比较全面的比较。

TestNG与JUnit的相同点：

       1. 使用annotation，且大部分annotation相同。

       2. 都可以进行单元测试（Unit test）。

       3. 都是针对Java测试的工具。

TestNG与JUnit的不同点：

      1. JUnit只能进行单元测试，TestNG可以进行单元测试，功能测试，端到端测试，集成测试等。

      2. TestNG需要一个额外的xml配置文件，配置测试的class、method甚至package。

      3. TestNG的运行方式更加灵活：命令行、ant和IDE，JUnit只能使用IDE。

      4. TestNG的annotation更加丰富，比如@ExpectedExceptions、@DataProvider等。

      5. 测试套件运行失败，JUnit 4会重新运行整个测试套件。TestNG运行失败时，会创建一个XML文件说明失败的测试，利用这个文件执行程序，就不会重复运行已经成功的测试。

TestNG比JUnit 4灵活性的体现：

      1. JUnit 4中必须把@BeforeClass修饰的方法声明为public static，这就限制了该方法中使用的变量必须是static。而TestNG中@BeforeClass修饰的方法可以跟普通函数完全一样。

      2. JUnit 4测试的依赖性非常强，测试用例间有严格的先后顺序。前一个测试不成功，后续所有的依赖测试都会失败。TestNG 利用@Test 的dependsOnMethods属性来应对测试依赖性问题。某方法依赖的方法失败，它将被跳过，而不是标记为失败。

      3. 对于n个不同参数组合的测试，JUnit 4要写n个测试用例。每个测试用例完成的任务基本是相同的，只是受测方法的参数有所改变。TestNG的参数化测试只需要一个测试用例，然后把所需要的参数加到TestNG的xml配置文件中。这样的好处是参数与测试代码分离，非程序员也可以修改参数，同时修改无需重新编译测试代码。

      4. 为了测试无法用String或原语值表示的复杂参数化类型，TestNG提供的@DataProvider使它们映射到某个测试方法。

      5. JUnit 4的测试结果通过Green/Red bar体现，TestNG的结果除了Green/Red bar，还有Console窗口和test-output文件夹，对测试结果的描述更加详细，方便定位错误。
      
Junit 4 和 TestNG 在注解方面的实现非常相似。

|特性|	JUnit 4|	TestNG|
|-----|---------|----------|
|测试注解	|@Test	|@Test|
|测试套件在执行之前需要执行的	|–|	@BeforeSuite|
|测试套件在执行之后需要执行的|	–	|@AfterSuite|
|在测试之前需要执行的|	–	|@BeforeTest|
|在测试之后需要执行的|	–	|@AfterTest|
|在一个测试方法所属于的任意一个组的第一个方法被调用之前执行|	–	|@BeforeGroups|
|在一个测试方法所属于的任意一个组的最后一个方法被调用之后执行	|–	|@AfterGroups|
|在当前类的第一个测试方法调用之前执行	|@BeforeClass|	@BeforeClass|
|在当前类的最后一个测试方法调用之后执行	|@AfterClass|	@AfterClass|
|每个测试方法之前需要执行|	@Before	|@BeforeMethod|
|每个测试方法之后需要执行	|@After|	@AfterMethod|
|忽略	|@ignore	|@Test(enbale=false)|
|预期异常|	@Test(expected = ArithmeticException.class)|	@Test(expectedExceptions = ArithmeticException.class)|
|超时|	@Test(timeout = 1000)	|@Test(timeout = 1000)|