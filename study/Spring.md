## 目录 

[一、idea创建spring项目(mac)]()

[二、在Spring的IOC容器里配置Bean]()

[三、ApplicationContext]()

[四、Spring支持3种依赖注入的方式]()

[五、引用其他的bean]()

[六、null值和级联属性]()

[七、集合属性]()

[八、properties]()

[九、使用utility scheme定义集合]()

[十、使用p命名空间]()

[十一、bean自动装配]()

[十二、bean之间的关系：继承和依赖]()

[十三、抽象Bean]()

[十四、依赖Bean]()

[十五、bean作用域]()

[十六、使用外部属性文件]()

[十七、通过调用静态工厂方法创建Bean]()

[十八、通过调用实例工厂方法创建Bean]()

[十九、通过注解配置Bean]()

[二十、泛型依赖注入]()

## 一、idea创建spring项目(mac)

## 二、在Spring的IOC容器里配置Bean

**配置形式：**基于XML文件的方式、基于注解的方式

**IOC：**其思想是**反转资源获取的方向**。传统的资源查找方式要求组件向容器发起请求查找资源作为回应，容器适时的返回资源。而应用了IOC之后，则是**容器主动地将资源推动给所管理的组件，组件所要做的仅是选择一种合适的方式来接受资源**，这种行为也称为查找的被动形式

**1. 在xml文件中通过bean节点来配置bean**

举个例子：

```
// 1. 创建HelloWorld类，提供setName()和hello()方法
public class HelloWorld {
    private String name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public void hello(){
        System.out.println("Hello: " + name);
    }
}
```

```
// 在src下创建applicationContext.xml，并配置bean
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    <context:component-scan base-package="com.sangyu"/>
    <!-- 配置bean-->
    <!-- id：bean的名称，且在IOC容器中必须是唯一的，若id没有指定，Spring自动类名作为bean的名字-->
    <bean id="helloWorld" class="com.sangyu.test.HelloWorld"> <!-- class：全类名，通过反射在IOC容器中创建bean，所以要求Bean中必须有无参数的构造器-->
        <!-- name:  对应HelloWorld类中setter方法；value对属性的赋值-->
        <property name="name" value="Spring"></property>
    </bean>
</beans>
```
```
// 创建Main类，通过容器调用HelloWorld类中的hello()方法
public class Main {
    public static void main(String[] args) {
        // 1. 创建IOC容器，加载文件applicationContext.xml
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml"); // ApplicationContext 代表IOC容器
       // 2. 从IOC容器中获取Bean实例
       // 利用id:helloWorld定位到IOC中bean
       // getBean()方法两种获取实例方式
       // 第一种：从IOC容器中获取Bean
        HelloWorld helloWorld = (HelloWorld) ctx.getBean("helloWorld"); 
        // 第二种：利用类型返回IOC容器中的Bean，但要求IOC容器中必须只能有一个该类型的Bean
        //HelloWorld helloWorld = ctx.getBean(HelloWorld.class);
      // 3. 调用HelloWorld类中的hello()方法
        helloWorld.hello();
    }
}
```

**Spring容器**

在SpringIOC容器读取Bean配置创建Bean实例之前，必须对容器进行实例化。只有在容器实例化后，才可以从IOC容器里获取Bean实例并使用

**Spring提供的两种IOC容器实现**

1. **BeanFactory：**IOC容器的基本实现，是Spring框架的基本设施，面向Spring本身

2. **ApplicationContext：**提供了更多的高级特性，是BeanFactory的子接口。面向使用Spring框架的开发者

## 三、ApplicationContext

**ApplicationContext的主要实现类**

ApplicationContext 在初始化上下文时就实例化所有单例的Bean

WebApplicationContext 继承了ApplicationContext接口，是ApplicationContext的扩展，是专门为WEB应用而准备的，它允许从相对于WEB根目录的路径中完成初始化工作

1. ClassPathXMLApplicationContext: 从类路
径下加载配置文件
    

2. FileSystemXmlApplicationContext: 从文件系统中加载配置文件


**ConfigurableApplicationContext**

扩展于ApplicationContext，新增加两个主要方法：refresh()和close()，让ApplicationContext
具有启动、刷新和关闭上下文的能力


## 四、Spring支持3种依赖注入的方式

1. 属性注入：通过setter方法注入Bean的属性值或依赖的对象

    属性注入使用<property>元素，使用name属性指定Bean的属性名称，Value属性或<value>子节点指定属性值

![](https://upload-images.jianshu.io/upload_images/2765653-e9370f66fb9feb5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-34a203bbdc6576a8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 构造方法注入：通过构造方法注入Bean的属性值或依赖的对象，它保证了Bean实例在实例化后就可以使用

      构造器注入在<construcotr-arg>元素里声明属性，<construcotr-arg>中没有name属性

```
<!-- 通过构造方法来配置bean的属性 - 按照构造器参数的顺序-->
    <bean id = "car" class="com.sangyu.test.Car">
        <constructor-arg  value="Audi"/>
        <constructor-arg  value="shanghai"/>
        <constructor-arg  value="300000"/>
    </bean>
```
```
<!-- 通过构造方法来配置bean的属性 - 通过index标记顺序-->
    <bean id = "car" class="com.sangyu.test.Car">
        <constructor-arg index="0" value="Audi"/>
        <constructor-arg index="1" value="shanghai"/>
        <constructor-arg index="2" value="300000"/>
    </bean>
```

```
    <!-- 多个构造器并且参数不同，通过参数列表类型区分-->
    <bean id="car" class="com.sangyu.test.Car">
        <constructor-arg index="0" type="java.lang.String" value="Audi"/>
        <constructor-arg index="1" type="java.lang.String" value="shanghai"/>
        <constructor-arg index="2" type="double" value="300000"/>
    </bean>

    <bean id="car2" class="com.sangyu.test.Car">
        <constructor-arg index="0" type="java.lang.String" value="Audi02"/>
        <constructor-arg index="1" type="java.lang.String" value="shanghai"/>
        <constructor-arg index="2" type="int" value="600000"/>
    </bean>
```

3. 字面值注入

    字面值：可用字符串表示的值，可以通过<value>元素标签或value属性进行注入；基本数据类型及其分装类，String类等类型都可以采取字面值注入的方式

```
 <bean id="car2" class="com.sangyu.test.Car">
        <constructor-arg index="0" type="java.lang.String" value="Audi02"/>
        <!-- 如果字面值包含特殊字符可以使用<![CDATA[]]> 包裹起来-->
        <constructor-arg index="1" type="java.lang.String">
            <value><![CDATA[Shanghai^]]></value>
        </constructor-arg>
        <constructor-arg index="2" type="int">
            <value>600000</value>
        </constructor-arg>
    </bean>
```

## 五、引用其他的bean

1. 在bean的配置文件中，通过```<ref>```元素或ref属性为Bean的属性或构造器参数指定对其他bean的引用

```
// 第一种写法
<bean id="person" class="com.sangyu.test.Person">
        <property name="name" value="Tom"></property>
        <property name="age" value="24"></property>
        <property name="car" ref="car2"></property>
    </bean>
```

```
// 第二种写法
 <bean id="person" class="com.sangyu.test.Person">
        <property name="name" value="Tom"></property>
        <property name="age" value="24"></property>
        <property name="car">
            <ref bean="car2"></ref>
        </property>
    </bean>
```
2. 也可以在属性或构造器里包含bean的声明，这样的bean称为内部bean，但要注意的是：内部bean不能被外部引用，只能在内部使用，所以不需要声明id

```
// 第三种写法
<bean id="person" class="com.sangyu.test.Person">
        <property name="name" value="Tom"></property>
        <property name="age" value="24"></property>
        <property name="car">
            <bean class="com.sangyu.test.Car">
                <constructor-arg index="0" type="java.lang.String" value="Ford"/>
                <constructor-arg index="1" type="java.lang.String" value="Changan"/>
                <constructor-arg index="2" type="double" value="200000"/>
            </bean>
        </property>
    </bean>
```

六、null值和级联属性

1. 可以使用专用的<null/>元素标签为Bean的字符串或其他对象类型的属性注入null值

```
<bean id="person" class="com.sangyu.test.Person">
        <constructor-arg index="0" value="Jerry"/>
        <constructor-arg index="1" value="25"/>
        <constructor-arg ><null/></constructor-arg>
</bean>
```

2. Spring支持级联属性的配置

```
<bean id="person" class="com.sangyu.test.Person">
    <constructor-arg value="Jerry"></constructor-arg>
    <constructor-arg value="25"></constructor-arg>
    <constructor-arg ref="car"></constructor-arg>
    <property name="car.price" value = "250"></property>
</bean>
```

## 七、集合属性

Spring中可以通过一组内置的xml标签(例如：<list>，<set>，<map> 来配置集合属性)

```
// 配置java.util.List类型的属性，需要指定<list>标签，
// 配置java.util.Set类型的属性，需要指定<set>标签，其他和<list>一样
// 通过<ref>指定对其他Bean的引用
<bean id="person" class="com.sangyu.test.Person">
        <constructor-arg index="0" value="Mike"/>
        <constructor-arg index="1" value="27"/>
        <constructor-arg index="2">
            <list>
                <ref bean="car"></ref>
            </list>
        </constructor-arg>
</bean>

// 通过<value>指定简单的常量值
    <bean id="person" class="com.sangyu.test.Person">
        <constructor-arg index="0" value="Mike"/>
        <constructor-arg index="1" value="27"/>
        <constructor-arg index="2">
            <list>
                <value name="car"></ref>
            </list>
        </constructor-arg>
    </bean>
```


```
// Java.util.Map通过<map>标签定义，<map>使用多个<entry> 作为子标签，每个条目包含一个键和一个值
// 必须在<key>标签里定义键
<bean id="newPerson" class="com.sangyu.test.NewPerson">
        <constructor-arg index="0" value="Rose"/>
        <constructor-arg index="1" value="28"/>
        <constructor-arg index="2">
            <map>
                <entry key="AA" value-ref="car"/>
            </map>
        </constructor-arg>
</bean>
```

## 八、properties

```
// 使用<props>定义java.util.Properties，该标签使用多个<prop>作为子标签，每个<prop>标签必须定义key属性
<bean id="dataSource" class="com.sangyu.test.DataSource">
        <property name="properties">
            <props>
                <prop key="user">root</prop>
                <prop key="password">1234</prop>
                <prop key="jdbcUrl">jdbc:mysql:///test</prop>
                <prop key="driverClass">com.mysql.jdbc.Driver</prop>
            </props>
        </property>
    </bean>
```
## 九、使用utility scheme定义集合

使用基本的集合标签定义集合时，不能将集合作为独立的Bean定义，导致其他Bean无法引用该集合，所以无法在不同Bean之间共享集合

可以使用util scheme里的集合标签定义独立的集合Bean，需要注意的是，必须在<beans>根元素里添加util schema定义

```
<!-- 配置单例的集合bean，以供多个bean进行引用，需要导入util命名空间-->
<util:list id="cars">
    <ref bean="car"></ref>
    <ref bean="car2"></ref>
</util:list>
    
<bean id="person4" class="com.sangyu.test.Person">
    <constructor-arg index="0" value="Jack"/>
    <constructor-arg index="1" value="29"/>
    <constructor-arg index="2" ref="cars"/>
</bean>
```

## 十、使用p命名空间
```
<!-- 配置p命名空间为bean的属性赋值，需要先导入p命名空间-->
<!-- 这里需要注意的是，使用p空间要有无参构造器-->
    <bean id="person5" class="com.sangyu.test.Person" p:age="30" p:name="Queen" p:car-ref="cars"></bean>
```

## 十一、bean自动装配

**XML配置里的Bean自动装配**

Spring IOC容器可以自动装配Bean，**通过<bean>的autowire属性里指定自动装配的模式**

1）byName: 根据名字自动装配

2）byType: 根据类型自动装配

```
// person 
public class Person {
    private String name;
    private Car car;
    private Address address;
    public void setName(String name) {
        this.name = name;
    }
    public void setCar(Car car) {
        this.car = car;
    }
    public void setAddress(Address address) {
        this.address = address;
    }
    public String getName(){
        return name;
    }
    public Car getCar() {
        return car;
    }
    public Address getAddress() {
        return address;
    }
    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", car=" + car +
                ", address=" + address +
                '}';
    }
}
```

```
// Address
public class Address {
    private String city;
    private String street;
    public void setCity(String city) {
        this.city = city;
    }
    public void setStreet(String street){
        this.street = street;
    }
    public String getCity() {
        return city;
    }
    public String getStreet() {
        return street;
    }
    @Override
    public String toString() {
        return "Address{" +
                "city='" + city + '\'' +
                ", street='" + street + '\'' +
                '}';
    }
}
```

```
// Car
public class Car {
    private String brand;
    private double price;
    public String getBrand(){
        return brand;
    }
    public double getPrice() {
        return price;
    }
    public void setPrice(double price) {
        this.price = price;
    }
    public void setBrand(String brand) {
        this.brand = brand;
    }
    @Override
    public String toString() {
        return "Car{" +
                "brand='" + brand + '\'' +
                ", price=" + price +
                '}';
    }
}
```

```
// 使用autowire属性指定自动装配的方式
// 1.byName根据bean的名字和当前bean的sette风格的属性名进行自动装配，若有装配的，则进行自动装配，若没有匹配的，则不装配
<bean id="address" class="com.sangyu.test01.Address" p:city="beijing" p:street="hh"></bean>

<bean id="car" class="com.sangyu.test01.Car"  p:brand="Audi" p:price="300000"></bean>

<bean id="person" class="com.sangyu.test01.Person" p:name="Tom" autowire="byName"></bean>

// 根据bean的类型和当前bean的属性的类型进行自动匹配
<bean id="address" class="com.sangyu.test01.Address" p:city="beijing" p:street="hh"></bean>
<bean id="car" class="com.sangyu.test01.Car"  p:brand="Audi" p:price="300000"></bean>
<bean id="person" class="com.sangyu.test01.Person" p:name="Tom" autowire="byType"></bean>

// 按照类型匹配要求类型必须是唯一，如果有两个相同类型类型会有异常
<bean id="address" class="com.sangyu.test01.Address" p:city="beijing" p:street="hh"></bean>
//<bean id="address2" class="com.sangyu.test01.Address"  p:city="beijing" p:street="hh"></bean> //如果有两个相同类型类型会有异常
<bean id="car" class="com.sangyu.test01.Car"  p:brand="Audi" p:price="300000"></bean>
<bean id="person" class="com.sangyu.test01.Person" p:name="Tom" autowire="byType"></bean>
```

```
// Main
public class Main {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        Person Person = (Person)ctx.getBean("person");
        System.out.println(Person);
    }
}
```

自动装配的缺点

1）在Bean配置文件里设置autowire属性进行自动装配将会配置Bean的所有属性。然后，若只希望装配个别属性时，autowire属性就不够灵活了

2）要么根据类型自动匹配，要么根据名称自动装配，不能两者都有

## 十二、bean之间的关系：继承和依赖

1）Spring允许继承bean的配置，被继承的bean称为父bean，继承的Bean称为子Bean，

2）子Bean继承父Bean中的配置，包括Bean的属性配置

3）子Bean可以覆盖从父Bean继承过来的配置

4）父Bean可以作为配置模版，也可以作为Bean实例，若只想把父Bean作为模版，可以设置<bean>的abstact属性为true，这样spring将不会实例化这个Bean

5）并不是<bean>元素里的所有都会被继承，如：autowire，abstract等

6）可以忽略父Bean的class属性，让子Bean指定自己的类，而共享相同的属性配置，但此时abstract必须设为true

```
// 继承
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="wudaokou"></bean>
<bean id="address2" parent="address"></bean>

// 覆盖
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="wudaokou"></bean>
<bean id="address2" p:city="Shanghai" p:street="Dazhongsi" parent="address"></bean>
```
## 十三、抽象Bean

```
// bean设置为抽象，抽象的bean只能继承不能实例化
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="WuDaoKou" abstract="true"></bean>
<bean id="address2" class="com.sangyu.test01.Address" p:street="DaZhongSi" parent="address"></bean>
```

## 十四、依赖Bean

1. Spring管理的bean都是单例模式(singleton)

2. 实例化对象应该顺序化的，比如A依赖B,B依赖C,C依赖D...

3. 一个bean可以依赖多个bean，可以通过逗号(",")或者分号(";")来定义多个依赖对象：

```
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="1111"></bean>
<bean id="person" class="com.sangyu.test01.Person" p:name="111" p:address-ref="address" depends-on="address"></bean>
```

## 十五、bean作用域
 
1. 通过scope属性设置Bean的作用域

2. 默认情况下，Spring管理的bean都是单例模式

| 属性值| 说明|
|-----| -----|
|singleton|单例的方式|
|prototype|每次调用getBean()都会返回一个新的实例|
|request|每次HTTP请求都会创建一个新的Bean，该作用域仅适用于WebApplicationContext环境|
|session|同一个HTTP Session共享一个Bean，不同的HTTP Session使用不同的Bean。该作用域仅适用于WebApplicationContext环境|


```
// 设置为singleton 模式
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="1111" scope="singleton"></bean>

// 设置为prototype 模式
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="1111" scope="prototype"></bean> 
```

## 十六、使用外部属性文件

```PropertyPlaceholderConfigurer``` 会从指定的location属性文件里加载属性，并使用这些属性来替换变量```${var}```
```
<context:property-placeholder location="classpath*:db.properties"></context:property-placeholder>
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
    <property name="user" value="${user}"></property>
    <property name="password" value="${password}"></property>
    <property name="driverClass" value="${driverClass}"></property>
    <property name="jdbcUrl" value="${jdbcUrl}"></property>
</bean>
```

```
// db.properties
user = root
password = 1230
driverClass = com.mysql.jdbc.Driver
jdbcUrl = jdbc:mysql:///test`
```

## 十七、通过调用静态工厂方法创建Bean

调用静态工厂方法创建Bean是将对象创建的过程封装到静态方法中，当客户端需要对象时，只需要简单地调用静态方法，而不同关心创建对象的细节

要声明通过静态方法创建Bean，需要在Bean的class属性里指定拥有该工厂的方法的类，同时在factory-method属性里指定工厂方法的名称，最后，使用<constrctor-arg>元素为该方法传递方法参数

```
// Car
public class Car {
    private String brand;
    private double price;
    public Car(String brand, double price){
        this.brand = brand;
        this.price = price;
    }
    public void setBrand(String brand) {
        this.brand = brand;
    }
    public void setPrice(double price) {
        this.price = price;
    }
    public double getPrice() {
        return price;
    }
    public String getBrand() {
        return brand;
    }
    @Override
    public String toString() {
        return "Car{" +
                "brand='" + brand + '\'' +
                ", price=" + price +
                '}';
    }
    public Car(){
        System.out.println("car's constructor");
    }
}

// Main
public class Main {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        Car car =(Car) ctx.getBean("car");
        System.out.println(car);
    }
}
// StaticCarFactory
public class StaticCarFactory {
    private static Map<String,Car> cars = new HashMap<String,Car>();
    static {
        cars.put("audi",new Car("audi",300000));
        cars.put("ford",new Car("ford",400000));
    }
    public static Car getCar(String name){
        return cars.get(name);
    }
}
// XML
<!-- 通过静态工厂方法来配置bean。注意不是配置静态工厂方法实例，而是配置bean实例-->
<!-- class 属性：指向静态工厂方法的全类名-->
<!-- factory-method：指向静态工厂方法的名字 -->
<!-- constructor-arg：如果工厂方法需要传入参数，则使用constructor-arg来配置参数 -->
<bean id="car" class="com.sangyu.test04.StaticCarFactory" factory-method="getCar">
    <constructor-arg value="audi"></constructor-arg>
</bean>
```

## 十八、通过调用实例工厂方法创建Bean

实例工厂方法：将对象的创建过程封装到另外一个对象实例的方法里，当客户端需要请求对象时，只需要简单的调用该实例方法而不需要关心对象创建细节

```
// StaticCarFactory
public class StaticCarFactory {
    private static Map<String,Car> cars = new HashMap<String,Car>();
    static {
        cars.put("audi",new Car("audi",300000));
        cars.put("ford",new Car("ford",400000));
    }
    public static Car getCar(String name){
        return cars.get(name);
    }
}
// XML
<bean id="carFactory" class="com.sangyu.test04.InstanceCarFactory"></bean>
<bean id="car" factory-bean="carFactory" factory-method="getCar">
      <constructor-arg value="ford"></constructor-arg>
</bean>
```




## 十九、 FactoryBean配置Bean

```
// 自定义的FactoryBean 需要实现FactoryBean接口
public class CarFactoryBean implements FactoryBean<Car> {
    @Override
    public Car getObject() throws Exception {
        return new Car("BMW",500000);
    }
    // 返回的bean的类型
    @Override
    public Class<?> getObjectType() {
        return Car.class;
    }
    @Override
    public boolean isSingleton() {
        return true;
    }
    private String brand;
    public void setBrand(String brand){
        this.brand = brand;
    }
}
// XML
 <!-- 通过FactoryBean来配置Bean的实例
        class：指向FactoryBean的全类名
        property：配置FactoryBean的属性
        但实际返回的实例确实FactoryBean的getObject()方法来返回的实例
-->
<bean id="car" class="com.sangyu.test04.CarFactoryBean">
      <property name="brand" value="BMW"></property>
</bean>
```

## 十九、通过注解配置Bean

**扫描组件**

Spring能够从classpath下自动扫描，侦测和实例化具有特定注解的组件。

特定组件包括：
```Component：```基本注解，标识了一个受Spring管理的组件
```Respository：```标识持久层组件
```Service：``` 标识服务层(业务层)组件
```Controller：```标识表现层组件

对于扫描到组件，Spring有默认的命名策略：使用非限定类名，第一个字母小写；

注解中通过value属性值标识组件的名称

使用注解后，还需要在Spring的配置文件中声明```<context:component-scar>：```
```base-package ```属性指定一个需要扫描的基类包，Spring容器将会扫描这个基类包里及其子包中的所有的类；当需要扫描多个包时，可以使用逗号隔开
```resource-pattern ``` 扫描特定的类而非基包下的所有类

目录结构

![](https://upload-images.jianshu.io/upload_images/2765653-6b6506dfa27e5813.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```
// UserRepository
public interface UserRepository {
    void save();
}
```
```
// UserRepositoryImpl
@Repository("userRepository")
public class UserRepositoryImpl implements UserRepository {
    @Override
    public void save() {
        System.out.println("UserRepository Save...");
    }
}
```
```
// UserController
@Controller
public class UserController {

    public void execute(){
        System.out.println("UserController execute... ");
    }
}
```

```
// UserService
@Service
public class UserService {
    public void add(){
        System.out.println("UserService add......");
    }
}
```

```
// TestObject
@Component
public class TestObject {
}
```

```
// Main
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        TestObject to = (TestObject)ctx.getBean("testObject");
        System.out.println(to);
        UserController tuserController = (UserController)ctx.getBean("userController");
        System.out.println(tuserController);
        UserService userService = (UserService)ctx.getBean("userService");
        System.out.println(userService);
        UserRepository userRepository = (UserRepository)ctx.getBean("userRepository");
        System.out.println(userRepository);
    }
}
```
```
// xml
<!--指定Spring IOC容器扫描的包 -->
<context:component-scan base-package="com.sangyu.test05.annotation"/>
// resource-pattern 指定扫描的资源
<context:component-scan base-package="com.sangyu.test05.annotation" resource-pattern="repository/*.class"/>
```

```<context:include-filter>：``` 子节点表示要包含的目标类
```<context:exclude-filter>：``` 子节点表示要排除在外的目标类
```<context:component-scar>：``` 下可以拥有若干个
```<context:include-filter>``` 和```<context:exclude-filter>```子节点
| 类别| 示例| 说明|
|-------|-------|-------|
| annotation  |  com.test.XxxAnntation  |  所有标注了XxxAnnotation的类。该类型采用目标类是否标注了某个注解进行过滤  |
| assinable  |  com.test.XxxService  | 所有继承或扩展XxxService的类，该类型采用目标类是否继承或扩展某个特定类进行过滤   |

```
<!--type="annotation" 该类型采用目标类是否标注了某个注解进行过滤-->
<!--context:exclude-filter 子节点指定排除哪些指定表达式的组件-->
<context:component-scan base-package="com.sangyu.test05.annotation">
        <context:exclude-filter expression="org.springframework.stereotype.Repository" type="annotation"/>
</context:component-scan>

<!--context:include-filter 子节点指定包含哪些表达式的组件，该子节点需要use-default-filters配合使用-->
<context:component-scan
        base-package="com.sangyu.test05.annotation"
        use-default-filters="false">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Repository"/>
</context:component-scan>

<!--type="assignable" 所有继承或扩展XxxService的类，该类型采用目标类是否继承或扩展某个特定类进行过滤 -->
<context:component-scan base-package="com.sangyu.test05.annotation">
    <context:exclude-filter type="assignable" expression="com.sangyu.test05.annotation.repository.UserRepository"/>
</context:component-scan>

<context:component-scan base-package="com.sangyu.test05.annotation" use-default-filters="false">
    <context:include-filter type="assignable" expression="com.sangyu.test05.annotation.repository.UserRepository"/>
</context:component-scan>
```

**使用@Autowired自动装配Bean**

构造器，普通字段（即使是非public）一切具有参数的方法都可以应用```@Autowired```注解

默认情况下，所有使用```@Autowired```注解的属性都需要被设置，当Spring找不到匹配的Bean装配属性时，会抛出异常

```
// UserService
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;
    public void add() {
        System.out.println("UserService add......");
        userRepository.save();
    }
}
// 另一种方式
@Service
public class UserService {
    private UserRepository userRepository;
    @Autowired
    public void setUserRepository(UserRepository userRepository){
        this.userRepository = userRepository;
    }
    public void add() {
        System.out.println("UserService add......");
        userRepository.save();
    }
}
```

```
// UserController
@Controller
public class UserController {
    @Autowired
    private UserService userService;
    public void execute() {
        System.out.println("UserController execute... ");
        userService.add();
    }
}
```

```
// Main
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserController userController = (UserController) ctx.getBean("userController");
        System.out.println(userController);
        userController.execute();
    }
}
```

若某一属性允许不被设置，可以设置```@Autowired```注解的required属性为false

```
// Main
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserRepository userRepository = (UserRepository)ctx.getBean("userRepository");
        System.out.println(userRepository);
    }
}
```

```
// TestObject
//@Component 注释掉
public class TestObject { }
```

```
// 实现类
@Repository("userRepository")
public class UserRepositoryImpl implements UserRepository {
    @Autowired(required = false)
    private TestObject testObject;
    @Override
    public void save() {
        System.out.println("UserRepository Save...");
        System.out.println(testObject);
    }
}
// 接口
public interface UserRepository {
    void save();
}
```

两个类实现一个接口的情况

```
// 接口
public interface UserRepository {
    void save();
}

// 实现类1
@Repository("userRepository") // 两个类实现一个接口 ，默认会按照设置的名字去查找实现类
public class UserRepositoryImpl implements UserRepository {
    @Autowired(required = false)
    private TestObject testObject;
    @Override
    public void save() {
        System.out.println("UserRepository Save...");
        System.out.println(testObject);
    }
}

// 实现类2
@Repository
public class UserJdbcRepository implements UserRepository {
    @Override
    public void save() {
        System.out.println("UserJdbcRepository save....");
    }
}
// Main
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserService userService = (UserService)ctx.getBean("userService");
        System.out.println(userService);
        userService.add();
    }
}
```

```
// 另一种方式：使用@Qualifier
@Service
public class UserService {
    @Autowired
    @Qualifier("userJdbcRepository")
    private UserRepository userRepository;
    public void add() {
        System.out.println("UserService add......");
        userRepository.save();
    }
}
```

## 二十、泛型依赖注入

spring 4.x 中可以为子类注入子类对应的泛型类型的成员变量的引用

```
@Service
public class UserService extends BaseService<User> {}
```
```
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserService userService = (UserService) ctx.getBean("userService");
        System.out.println(userService);
        userService.add();
    }
}
```
```
public class BaseService<T> {
    @Autowired
    protected BaseRepository<T> repository;

    public void add(){
        System.out.println("add...");
        System.out.println(repository);
    }
}
```

```
public class BaseRepository<T> { }
```

```
@Repository
public class UserRepository extends BaseRepository<User> {
    @Override
    public String toString() {
        System.out.println("UserRepository");
        return super.toString();
    }
}
```

```
public class User { }
```
