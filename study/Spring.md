## 目录 

[一、idea创建spring项目(mac)](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E4%B8%80idea%E5%88%9B%E5%BB%BAspring%E9%A1%B9%E7%9B%AEmac)

[二、Bean属性注入](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E4%BA%8Cbean%E5%B1%9E%E6%80%A7%E6%B3%A8%E5%85%A5)

[三、Bean 注入参数的类型](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E4%B8%89bean-%E6%B3%A8%E5%85%A5%E5%8F%82%E6%95%B0%E7%9A%84%E7%B1%BB%E5%9E%8B)

[四、引用其他的bean](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%9B%9Bbean%E8%87%AA%E5%8A%A8%E8%A3%85%E9%85%8D)

[五、bean自动装配](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E4%BA%94bean%E4%B9%8B%E9%97%B4%E7%9A%84%E5%85%B3%E7%B3%BB%E7%BB%A7%E6%89%BF%E5%92%8C%E4%BE%9D%E8%B5%96)

[六、bean之间的关系：继承和依赖](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%85%AD%E6%8A%BD%E8%B1%A1bean)

[七、抽象Bean](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E4%B8%83%E4%BE%9D%E8%B5%96bean)

[八、依赖Bean](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%85%ABbean%E4%BD%9C%E7%94%A8%E5%9F%9F)

[九、bean作用域](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E4%B9%9D%E4%BD%BF%E7%94%A8%E5%A4%96%E9%83%A8%E5%B1%9E%E6%80%A7%E6%96%87%E4%BB%B6)

[十、使用外部属性文件](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E9%80%9A%E8%BF%87%E8%B0%83%E7%94%A8%E9%9D%99%E6%80%81%E5%B7%A5%E5%8E%82%E6%96%B9%E6%B3%95%E5%88%9B%E5%BB%BAbean)

[十一、通过调用静态工厂方法创建Bean](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E4%B8%80%E9%80%9A%E8%BF%87%E8%B0%83%E7%94%A8%E5%AE%9E%E4%BE%8B%E5%B7%A5%E5%8E%82%E6%96%B9%E6%B3%95%E5%88%9B%E5%BB%BAbean)

[十二、通过调用实例工厂方法创建Bean](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E4%BA%8C-factorybean%E9%85%8D%E7%BD%AEbean)

[十三、通过注解配置Bean](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E4%B8%89%E9%80%9A%E8%BF%87%E6%B3%A8%E8%A7%A3%E9%85%8D%E7%BD%AEbean)

[十四、泛型依赖注入](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E5%9B%9B%E6%B3%9B%E5%9E%8B%E4%BE%9D%E8%B5%96%E6%B3%A8%E5%85%A5)

[十五、AOP](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E4%BA%94aop)

[十六、Spring对JDBC的支持](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E5%85%ADspring%E5%AF%B9jdbc%E7%9A%84%E6%94%AF%E6%8C%81)

[十七、使用NamedParameterJdbcTemplate](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E4%B8%83%E4%BD%BF%E7%94%A8namedparameterjdbctemplate)

[十八、事务管理](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E5%85%AB%E4%BA%8B%E5%8A%A1%E7%AE%A1%E7%90%86)

[十九、spring - 生命周期](https://github.com/xingyuexingyue/sangyu/blob/master/study/Spring.md#%E5%8D%81%E4%B9%9Dspring---%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F)

## 一、idea创建spring项目(mac)

## 二、Bean属性注入

**IOC：**其思想是**反转资源获取的方向**。传统的资源查找方式要求组件向容器发起请求查找资源作为回应，容器适时的返回资源。而应用了IOC之后，则是**容器主动地将资源推动给所管理的组件，组件所要做的仅是选择一种合适的方式来接受资源**，这种行为也称为查找的被动形式

（此处通过XML方式创建Bean的方式）

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

        // ApplicationContext 代表IOC容器，在初始化上下文时就实例化所有单例的Bean
        // ClassPathXMLApplicationContext: 从类路
径下加载配置文件
        // WebApplicationContext 继承了ApplicationContext接口，是ApplicationContext的扩展，是专门为WEB应用而准备的，它允许从相对于WEB根目录的路径中完成初始化工作
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml"); 
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
#### 通过setter方法属性注入Bean

```
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
<bean id = "helloWorld" class="com.sangyu.test.bean.HelloWorld">
    <property name="name" value="Spring"></property>
</bean>
```

```
<bean id = "helloWorld" class="com.sangyu.test.bean.HelloWorld">
    <property name="name" >
       <value>Spring</value> <!--value字节点-->
    </property>
</bean> 
```

#### 通过构造方法注入Bean

```
public class HelloWorld {
    private String name;
    private String city;
    private int age;
    
    public HelloWorld(String name,String city,int age){
        this.name = name;
        this.city = city;
        this.age = age;
    }
}
```

```
<!-- 通过构造方法来配置bean的属性 - 按照构造器参数的顺序-->
    <bean id = "helloWorld" class="com.sangyu.test.bean.HelloWorld">
        <constructor-arg  value="Audi"/> <!-- 注意<construcotr-arg>中没有name属性-->
        <constructor-arg  value="shanghai"/>
        <constructor-arg  value="300000"/>
    </bean>
```
```
<!-- 通过构造方法来配置bean的属性 - 按照index标记顺序-->
    <bean id = "helloWorld" class="com.sangyu.test.bean.HelloWorld">
        <constructor-arg index="0" value="sangyu"/>
        <constructor-arg index="1" value="BJ"/>
        <constructor-arg index="2" value="11"/>
    </bean>
```

```
 <!--        通过构造方法来配置bean属性，按照参数列表类型 ,多个构造器并且参数不同，按照参数列表类型区分-->
<constructor-arg type="java.lang.String" value="sangyu"/>
<constructor-arg type="java.lang.String" value="BJ"/>
<constructor-arg type="int" value="1200"/>
```


## 三、Bean 注入参数的类型

在Spring 的配置文件中，用户可以通过Bean的property元素进行参数注入。使用property，不但可以将String、int等字面值注入到Bean中，还可以将集合、Map等类型的注入到Bean中，此外还可以注入配置文件中其他定义的Bean。

#### 1、字面值

一般是指可用字符串表示的值，这些值可以通过<value>元素标签进行注入。
在默认情况下，基本数据类型及其封装类，String等类型都可以采取字面值注入的方式：


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

#### 2、引用其他的bean

1. 在bean的配置文件中，通过```<ref>```元素或ref属性为Bean的属性或构造器参数指定对其他bean的引用

```
public class User {
    private String name;
    private String city;
    private int age;
    private Book book;

    public Book getBook() {return book; }
    public void setBook(Book book) {this.book = book;}
    public int getAge() {return age;}
    public String getCity() { return city;}
    public String getName() {return name;}
    public void setCity(String city) {this.city = city;}
    public void setAge(int age) {this.age = age;}
    public void setName(String name) {this.name = name;}

    @Override
    public String toString() {
        return "User{" +
                "name='" + name + '\'' +
                ", city='" + city + '\'' +
                ", age=" + age +
                ", book=" + book +
                '}';
    }
}
```

```
public class Book {
    private String bookName;
    private int id;
    private int price;

    public int getId() { return id;}
    public void setId(int id) { this.id = id;}
    public void setBookName(String bookName) {this.bookName = bookName;}
    public String getBookName() {return bookName;}
    public void setPrice(int price) {this.price = price;}
    public int getPrice() { return price;}

    @Override
    public String toString() {
        return "Book{" +
                "bookName='" + bookName + '\'' +
                ", id=" + id +
                ", price=" + price +
                '}';
    }
}
```

```
<bean id="book" class="com.sangyu.test.bean.Book">
    <property name="bookName" value="HaHaHa"/>
    <property name="id" value="1"/>
    <property name="price" value="1200"/> <!-- 以分为单位，避免产生精度问题-->
</bean>
<bean id="user" class="com.sangyu.test.bean.User">
    <property name="age" value="11"/>
    <property name="city" value="BJ"/>
    <property name="name" value="sangyu"/>
    <property name="book" ref="book"/> <!-- 通过ref属性-->
</bean>
```


```
// 也通过<ref>元素
<bean id="user" class="com.sangyu.test.bean.User">
    <property name="age" value="11"/>
    <property name="city" value="BJ"/>
    <property name="name" value="sangyu"/>
        <property name="book">
            <ref bean="book"></ref>
        </property>
</bean>
```

```
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx =
                new ClassPathXmlApplicationContext("applicationContext.xml");
        User user = (User) ctx.getBean("user");
        System.out.println(user);
    }
}
```
2. 也可以在属性或构造器里包含bean的声明，这样的bean称为内部bean，但要注意的是：内部bean不能被外部引用，只能在内部使用，所以不需要声明id

```
    <bean id="user1" class="com.sangyu.test.bean.User">
        <property name="name" value="sangyu01"/>
        <property name="age" value="11"/>
        <property name="city" value="BJ"/>
        <property name="book">
            <bean class="com.sangyu.test.bean.Book">
                <property name="price" value="1200"/>
                <property name="bookName" value="123"/>
                <property name="id" value="2"/>
            </bean>
        </property>
    </bean>
```

#### 3、集合属性

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

#### 4、properties

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
#### 5、使用utility scheme定义集合

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

#### 6、使用p命名空间**
```
<!-- 配置p命名空间为bean的属性赋值，需要先导入p命名空间-->
<!-- 这里需要注意的是，使用p空间要有无参构造器-->
    <bean id="person5" class="com.sangyu.test.Person" p:age="30" p:name="Queen" p:car-ref="cars"></bean>
```


## 四、bean自动装配

```
<!--    根据名字自动装配-->
    <bean id="user" class="com.sangyu.test.bean.User" autowire="byName">
        <property name="city" value="BJ"/>
        <property name="age" value="11"/>
        <property name="name" value="sangyu"/>
    </bean>
```

```$xslt
<!--    根据类型自动装配-->
    <bean id="user1" class="com.sangyu.test.bean.User" autowire="byType">
        <property name="city" value="BJ"/>
        <property name="age" value="11"/>
        <property name="name" value="sangyu"/>
    </bean>
```

## 五、bean之间的关系：继承和依赖

```
// 继承
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="wudaokou"></bean>
<bean id="address2" parent="address"></bean>

// 覆盖
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="wudaokou"></bean>
<bean id="address2" p:city="Shanghai" p:street="Dazhongsi" parent="address"></bean>
```
## 六、抽象Bean

```
// bean设置为抽象，抽象的bean只能继承不能实例化
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="WuDaoKou" abstract="true"></bean>
<bean id="address2" class="com.sangyu.test01.Address" p:street="DaZhongSi" parent="address"></bean>
```

## 七、依赖Bean


```
<bean id="address" class="com.sangyu.test01.Address" p:city="Beijing" p:street="1111"></bean>
<bean id="person" class="com.sangyu.test01.Person" p:name="111" p:address-ref="address" depends-on="address"></bean>
```

## 八、bean作用域
 
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

## 九、使用外部属性文件

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

## 十、通过调用静态工厂方法创建Bean

调用静态工厂方法创建Bean是将对象创建的过程封装到静态方法中，当客户端需要对象时，只需要简单地调用静态方法，而不同关心创建对象的细节

要声明通过静态方法创建Bean，需要在Bean的class属性里指定拥有该工厂的方法的类，同时在factory-method属性里指定工厂方法的名称，最后，使用<constrctor-arg>元素为该方法传递方法参数

Spring 将调用静态工厂方法（可能包含一组参数），来返回一个Bean实例，一旦获得了指定Bean实例，Spring后面的处理步骤与采用普通方法创建Bean实例则完全一样。需要注意的是，当使用静态工厂方法来创建Bean时，这个factory-method必须要是静态的。

```
// 定义一个接口，静态方法产生的时该类的实例
public interface Animal {
    public void sayHello();

    void setMsg(String msg);
}
```

```
// 接口的实现类
public class Cat implements Animal {
    private String msg;
    //依赖注入时必须的setter方法
    public void setMsg(String msg){
        this.msg = msg;
    }
    @Override
    public void sayHello(){
        System.out.println(msg + "，喵~喵~");
    }
}
```

```
// 接口的实现类
public class Dog implements Animal {
    private String msg;
    //依赖注入时必须的setter方法
    public void setMsg(String msg){
        this.msg = msg;
    }
    @Override
    public void sayHello(){
        System.out.println(msg + "，旺~旺~");
    }
}
```

```
// AnimalFactory工厂，包含getAnimal静态方法，该方法根据传入的参数决定创建哪个对象。这是典型的静态工厂设计模式
public clas AnimalFactory {
    public static Animal getAnimal(String type){
        if ("cat".equalsIgnoreCase(type)){
            return new Cat();
        } else {
            return new Dog();
        }
    }
}
```
Spring配置文件，指定Spring使用AnimalFactory来产生Animal对象

```
  <!-- 配置AnimalFactory的getAnimal方法，使之产生Cat -->
    <bean id = "cat" class="com.sangyu.test.bean.AnimalFactory" factory-method="getAnimal">
        <!-- 配置静态工厂方法的参数，getAnimal方法将产生Cat类型的对象 -->
        <constructor-arg value="cat"/>
        <!-- 通过setter注入的普通属性 -->
        <property name="msg" value="猫猫"/>
    </bean>

    <!-- 配置AnimalFactory的getAnimal方法，使之产生Dog -->
    <bean id="dog" class="com.sangyu.test.bean.AnimalFactory" factory-method="getAnimal">
        <!-- 配置静态工厂方法的参数，getAnimal方法将产生Dog类型的对象 -->
        <constructor-arg value="dog"/>
        <!-- 通过setter注入的普通属性 -->
        <property name="msg" value="狗狗"/>
    </bean>
```

```
// 主程序获取cat和dog两个Bean实例的方法，只需要调用spring容器的getBean()即可
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx =
                new ClassPathXmlApplicationContext("applicationContext.xml");

        Animal a1 = ctx.getBean("cat",Animal.class);
        a1.sayHello();

        Animal a2 = ctx.getBean("dog",Animal.class);
        a2.sayHello();
    }
}
```


## 十一、通过调用实例工厂方法创建Bean

实例工厂方法与静态工厂方法只有一点不同：调用静态工厂方法只需要使用工厂了即可，调用实例工厂方法则必须使用工厂实例。所以在Spring配置上也只有一点区别：配置静态工厂指定静态工厂类，配置实例工厂方法则指定工厂实例。

使用上面调用静态工厂方法例子修改为：


```
public class AnimalFactory {
    public Animal getAnimal(String type){ // 去掉static关键字
        if("cat".equalsIgnoreCase(type)){
            return new Cat();
        }else {
            return new Dog();
        }
    }
}
```

```$xslt
<!-- 配置工厂类-->
<bean id="animalFactory" class="com.sangyu.test.bean.AnimalFactory"/>

<!--这里使用factory-bean指定实例工厂类对象-->
<bean id="cat" factory-bean="animalFactory" factory-method="getAnimal">
    <!--同样指定factory-method的参数-->
    <constructor-arg value="cat"/>
    <property name="msg" value="猫咪"/>
</bean>

<bean id="dog" factory-bean="animalFactory" factory-method="getAnimal">
    <constructor-arg value="dog"/>
    <property name="msg" value="狗狗"/>
</bean>
```



## 十二、 FactoryBean配置Bean

```$xslt
public class Car {
    private int id;
    private String name;
    private int price;

    @Override
    public String toString() {
        return "Car [id=" + id + ", name=" + name + ", price=" + price + "]";
    }

    public Car(){

    }

    public Car(int id, String name, int price) {
        super();
        this.id = id;
        this.name = name;
        this.price = price;
    }
}
```

```
// 自定义的FactoryBean 需要实现FactoryBean接口
public class CarBeanFactory implements FactoryBean<Car>{

    private int id;
    private String brand;

    public void setId(int id) {
        this.id = id;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    @Override
    public Car getObject() throws Exception {
        return new Car(id, brand, 0);
    }

    @Override
    public Class<?> getObjectType() {
        return Car.class;
    }

    @Override
    public boolean isSingleton() {
        return true;
    }

}
```

```
 <!-- 通过FactoryBean来配置Bean的实例
        class：指向FactoryBean的全类名
        property：配置FactoryBean的属性
        但实际返回的实例确实FactoryBean的getObject()方法来返回的实例
-->
<bean id="car1" class="com.home.factoryBean.CarBeanFactory">
  <property name="id" value="1"></property>
  <property name="brand" value="Ford"></property>
</bean>
```

## 十三、通过注解配置Bean

Spring能够从classpath下自动扫描，实例化具有特定注解的组件。

特定组件包括：
```Component：```基本注解，标识了一个受Spring管理的组件 
```Respository：```标识持久层组件 主要是作用于DAO类上的，为了让spring能够扫描类路径的时候扫描并识别出@Repository，从而扫描到DAO。
```Service：``` 标识服务层(业务层)组件，为了让spring能够扫描类路径的时候识别业务层类。
```Controller：```标识表现层组件，可以让spring在扫描的时候扫描到控制层的各个类。

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



#### 使用@Autowired自动装配Bean

构造器，类成员变量（即使是非public）一切具有参数的方法都可以应用```@Autowired```注解，完成自动装配的工作

如果对成员变量使用了@Autowired注解，可以直接使用反射将标注的成员变量注入到Bean中，而省略getter和setter方法。如果作用在构造函数上，会自动将构造函数所需的参数Bean注入
 
默认情况下，所有使用```@Autowired```注解的属性都需要被设置，当Spring找不到匹配的Bean装配属性时，会抛出异常。要想避免这种异常，可以用@Autowired(required = false)，告诉spring，找不到Bean也无须报错。

```
// UserService
@Service
public class UserService {
    // 将@Autowired注解到类成员变量上
    @Autowired
    private UserRepository userRepository;
    public void add() {
        System.out.println("UserService add......");
        userRepository.save();
    }
}
// 或者将@Autowired注解到方法
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
// 接口
public interface UserRepository {
    void save();
}

// 实现类
@Repository("userRepository")
public class UserRepositoryImpl implements UserRepository {
    @Autowired(required = false)  // TestObject 自动装配的类已经从spring组件中移除
    private TestObject testObject;
    @Override
    public void save() {
        System.out.println("UserRepository Save...");
        System.out.println(testObject);
    }
}

```

```
// TestObject
//@Component 注释掉
public class TestObject {}
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

## 十四、泛型依赖注入

spring 4.x 中可以为子类注入子类对应的泛型类型的成员变量的引用


```
public class User { }
```

```
public class BaseRepository<T> { }
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
@Service
public class UserService extends BaseService<User> {}
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
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        UserService userService = (UserService) ctx.getBean("userService");
        System.out.println(userService);
        userService.add();
    }
}
```

## 十五、AOP

编写一个简单的需求：要求在程序执行期间追踪正在发生的活动

```
// 接口
public interface AtithmeticCalculator {
    int add(int i,int j);
    int sub(int i,int j);
    int mul(int i,int j);
    int div(int i,int j);
}
```
```
// 实现
public class AtithmeticCalculatorImpl implements AtithmeticCalculator {
    @Override
    public int add(int i, int j) {
        System.out.println("The method add begins with [" + i + "," + j + "]");
        int result = i + j;
        System.out.println("The method add ends with " + result);
        return result;
    }
    @Override
    public int sub(int i, int j) {
        System.out.println("The method add begins with [" + i + "," + j + "]");
        int result = i - j;
        System.out.println("The method add ends with " + result);
        return result;
    }
    @Override
    public int mul(int i, int j) {
        System.out.println("The method add begins with [" + i + "," + j + "]");
        int result = i * j;
        System.out.println("The method add ends with " + result);
        return result;
    }
    @Override
    public int div(int i, int j) {
        System.out.println("The method add begins with [" + i + "," + j + "]");
        int result = i / j;
        System.out.println("The method add ends with " + result);
        return result;
    }
}
```
```
// Main
public class Main {
    public static void main(String[] args) {
        AtithmeticCalculator atithmeticCalculator = new AtithmeticCalculatorImpl();
        int result = atithmeticCalculator.add(1,2);
        System.out.println(result);
        result = atithmeticCalculator.div(4,2);
        System.out.println(result);
    }
}
// Output
The method add begins with [1,2]
The method add ends with 3
3
The method add begins with [4,2]
The method add ends with 2
2
```

上面例子中的实现代码存在的问题：
1. 代码混乱：非业务需求(日志和验证等)加入后，原有的业务方法急剧膨胀，每个方法在处理核心逻辑的同时还必须兼顾其他多个关注点
2. 代码分散：以日志需求为例，只是为了满足这个单一的需求，就不得不在多个模块(方法)里多次重复相同的日志代码，如果日志需求发生变化，必须修改所有的模块

#### 使用动态代理解决上述问题
代理设计模式的原理：使用一个代理将对象包装起来，然后用该代理对象取代原始对象，任何对原始对象的调用都要通过代理，代理对象决定是否以及合适将方法调用转到原始对象上

```
// 接口
public interface ArithmeticCalculator {
    int add(int i, int j);
    int sub(int i, int j);
    int mul(int i, int j);
    int div(int i, int j);
}
```

```
// 实现类
public class ArithmeticCalculatorImpl implements ArithmeticCalculator {
    @Override
    public int add(int i, int j) {
        int result = i + j;
        return result;
    }
    @Override
    public int sub(int i, int j) {
        int result = i - j;
        return result;
    }
    @Override
    public int mul(int i, int j) {
        int result = i * j;
        return result;
    }
    @Override
    public int div(int i, int j) {
        int result = i / j;
        return result;
    }
}
```

```
// 代理
public class ArithmeticCalculatorLoggingProxy {
    // 要代理的对象
    private ArithmeticCalculator target;

    public ArithmeticCalculatorLoggingProxy(ArithmeticCalculator target){
        this.target = target;
    }
    public ArithmeticCalculator getLoggingProxy(){
        ArithmeticCalculator proxy = null;
        // 代理对象由哪一个类加载器负责加载
        ClassLoader loader = target.getClass().getClassLoader();
        // 代理对象的类型，即其中有哪些方法
        Class [] interfaces = new Class[]{ArithmeticCalculator.class};
        // 当调用代理对象其中的方法时，该执行的代码
        InvocationHandler h = new InvocationHandler() {
            /**
             *
             * @param proxy 正在返回的那个代理对象，一般情况下，在invoke方法中都不使用该对象
             * @param method 正在被调用的方法
             * @param args 调用方法时，传入的参数
             * @return
             * @throws Throwable
             */
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                String methodName = method.getName();
                // 日志
                System.out.println("The method" + methodName + "begins with " + Arrays.asList(args));
                // 执行方法
                Object result = method.invoke(target,args);
                // 日志
                System.out.println("The method" + methodName + "ends with " + result);
                return result;
            }
        };
        proxy = (ArithmeticCalculator) Proxy.newProxyInstance(loader,interfaces,h);
        return proxy;
    }
}
```

```
// Main
public class Main {
    public static void main(String[] args) {
        ArithmeticCalculator target = new ArithmeticCalculatorImpl();
        ArithmeticCalculator proty = new ArithmeticCalculatorLoggingProxy(target).getLoggingProxy();
        int result = proty.add(1,2);
        System.out.println(result);
        result = proty.div(8,2);
        System.out.println(result);
    }
}
```

#### AOP

AOP面向切面编程，是一种新的方法论，并对传统OOP(面向对象编程)的补充

在应用AOP编程时，仍然需求定义公共功能，但可以明确的定义这个功能在哪里，以什么方式应用，并且不必修改受影响的类，这样依赖横切关注点就被模块化到特殊的对象(切面)里

![](https://upload-images.jianshu.io/upload_images/2765653-02ad32a4e2c1e4c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


切面(Aspect)：横切关注点 (跨越应用程序多个模块的功能)被模块化的特殊对象

通知(Advice)：切面必须要完成的工作

目标(Target)：被通知的对象

代理(Proxy)：向目标对象应用通知之后创建的对象

连接点(Joinpoint)：程序执行的某个特定位置：如类某个方法调用前，调用后，方法抛出异常后等。

切点(pointcut)：每个类都拥有多个连接点。即连接点是程序类中客观存在的事务。AOP通过切点定位到特定的连接点


#### Spring中启用AspectJ注解支持

AspectJ：Java社区里最完整最流行的AOP框架

通知是标注有注解的简单的Java方法：

```@Before``` 前置通知，在方法执行之前执行

```@After``` 后置通知，在方法执行之后执行

```@AfterRunning``` 返回通知，在方法返回结果之后执行

```@AfterThrowing``` 异常通知，在方法抛出异常之后

```@Around```环绕通知，环绕着方法执行 
 
```
// maven注入依赖
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-aop</artifactId>
  <version>5.1.12.RELEASE</version>
</dependency>

<dependency>
  <groupId>org.aspectj</groupId>
  <artifactId>aspectjweaver</artifactId>
  <version>1.9.4</version>
</dependency>
```

```
// ArithmeticCalculator
public interface ArithmeticCalculator {
    int add(int i, int j);
    int sub(int i, int j);
    int mul(int i, int j);
    int div(int i, int j);
}
```

```
// ArithmeticCalculatorImpl
@Component
public class ArithmeticCalculatorImpl implements ArithmeticCalculator {
    @Override
    public int add(int i, int j) {
        int result = i + j;
        return result;
    }
    @Override
    public int sub(int i, int j) {
        int result = i - j;
        return result;
    }
    @Override
    public int mul(int i, int j) {
        int result = i * j;
        return result;
    }
    @Override
    public int div(int i, int j) {
        int result = i / j;
        return result;
    }
}
```
```
// ArithmeticCalculatorLoggingProxy
public class ArithmeticCalculatorLoggingProxy {
    // 要代理的对象
    private ArithmeticCalculator target;

    public ArithmeticCalculatorLoggingProxy(ArithmeticCalculator target){
        this.target = target;
    }
    public ArithmeticCalculator getLoggingProxy(){
        ArithmeticCalculator proxy = null;
        // 代理对象由哪一个类加载器负责加载
        ClassLoader loader = target.getClass().getClassLoader();
        // 代理对象的类型，即其中有哪些方法
        Class [] interfaces = new Class[]{ArithmeticCalculator.class};
        // 当调用代理对象其中的方法时，该执行的代码
        InvocationHandler h = new InvocationHandler() {
            /**
             * @param proxy 正在返回的那个代理对象，一般情况下，在invoke方法中都不使用该对象
             * @param method 正在被调用的方法
             * @param args 调用方法时，传入的参数
             * @return
             * @throws Throwable
             */
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                String methodName = method.getName();
                // 日志
                System.out.println("The method" + methodName + "begins with " + Arrays.asList(args));
                // 执行方法
                Object result = method.invoke(target,args);
                // 日志
                System.out.println("The method" + methodName + "ends with " + result);
                return result;
            }
        };
        proxy = (ArithmeticCalculator) Proxy.newProxyInstance(loader,interfaces,h);
        return proxy;
    }
}
```

```
// LoggingAspect
@Component
@Aspect
public class LoggingAspect {

    // 声明该方法是一个前置通知：在目标方法开始之前执行
    // @Before("execution(public int com.sangyu.test10.ArithmeticCalculator.add(int, int))") // 只针对add方法
    @Before("execution(public int com.sangyu.test10.ArithmeticCalculator.*(int, int))") // 所有方法：add、mul、div、sub
    public void beforeMethod(JoinPoint joinPoint){
        String methodName = joinPoint.getSignature().getName();
        List<Object> args = Arrays.asList(joinPoint.getArgs());
        System.out.println("The method " + methodName + " begins with" + args);
    }
}
```
```
// Main
public class Main {
    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        ArithmeticCalculator arithmeticCalculator = ctx.getBean(ArithmeticCalculator.class);
        int result = arithmeticCalculator.add(3,6);
        System.out.println("result: " + result);
        result = arithmeticCalculator.sub(2,1);
        System.out.println("result: " + result);
        result = arithmeticCalculator.mul(2,1);
        System.out.println("result: " + result);
        result = arithmeticCalculator.div(6,3);
        System.out.println("result: " + result);
    }
}
```

#### 前置通知

在方法执行之前执行的通知，使用@Before注解，并将切入点表达式的值作为注解值

![](https://upload-images.jianshu.io/upload_images/2765653-1932316387715761.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 编写AspectJ切入点表达式

通过方法的签名来匹配各种方法：
```execution * com.sangyu.test10.ArithmeticCalculator.*(...) ``` 匹配ArithmeticCalculator中声明的所有方法，第一个*代表任意修饰符及任意返回值，第二个* 代表任意方法，...表示匹配任意数量的参数(若目标类于接口与该切面在同一个包中，可以省略包名)

```execution public * com.sangyu.test10.ArithmeticCalculator.*(...) ```  匹配ArithmeticCalculator接口的所有共有方法

```execution public double com.sangyu.test10.ArithmeticCalculator.*(...) ``` 匹配ArithmeticCalculator中返回double类型数值的方法

```execution public double com.sangyu.test10.ArithmeticCalculator.*(double,...) ``` 匹配第一个参数为double类型的方法 ...匹配任意数量任意类型的参数

```execution public double com.sangyu.test10.ArithmeticCalculator.*(double,double) ``` 匹配参数类型为double,double类型的方法

```execution * *,*(...) ``` 执行任意类的任意方法

#### JoinPoint

通知方法中beforeMethod()中声明一个类型为JoinPoint的参数，可以访问链接细节，如方法名称和参数值

![](https://upload-images.jianshu.io/upload_images/2765653-1b55d53fd1ce42b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### 后置通知

在连接点完成之后执行的，即连接点返回结果或者抛出异常的时候，下面的后置通知记录了方法的终止，一个切面可以包括一个或者多个通知

```
@Component
@Aspect
public class LoggingAspect {
    // 声明该方法是一个前置通知：在目标方法开始之前执行
     @Before("execution(public int com.sangyu.test10.ArithmeticCalculator.add(int, int))") // 只针对add方法
//    @Before("execution(public int com.sangyu.test10.ArithmeticCalculator.*(int, int))") // 所有方法：add、mul、div、sub
    public void beforeMethod(JoinPoint joinPoint){
        String methodName = joinPoint.getSignature().getName();
        List<Object> args = Arrays.asList(joinPoint.getArgs());
        System.out.println("The method " + methodName + " begins with" + args);
    }
    // 后置通知：在目标方法执行后(无论是否发生异常)，执行的通知
    @Before("execution(public int com.sangyu.test10.ArithmeticCalculatorImpl.*(int, int))") // 所有方法：add、mul、div、sub
    public void afterMethod(JoinPoint joinPoint){
         String methodName = joinPoint.getSignature().getName();
        System.out.println("The method " + methodName + " end");
    }
}
```

## 十六、Spring对JDBC的支持

Spring在JDBC API上定义了一个抽象层，以此建立一个JDBC存取框架，

#### 获取数据库连接
```
// db.properties
jdbc.user = root
jdbc.password = 1230
jdbc.driverClass = com.mysql.cj.jdbc.Driver
jdbc.jdbcUrl = jdbc:mysql://localhost:3306/ssm_crud?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&failOverReadOnly=false&useSSL=false&serverTimezone=UTC

jdbc.initPoolSize=5
jdbc.maxPoolSize=10
```

```
// applicationContext.xml
 <!--导入资源文件-->
    <context:property-placeholder location="classpath:db.properties"/>

    <!--配置c3p0数据源-->
    <bean id="datasource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="User" value="${jdbc.user}"/>
        <property name="Password" value="${jdbc.password}"/>
        <property name="DriverClass" value="${jdbc.driverClass}"/>
        <property name="jdbcUrl" value="${jdbc.jdbcUrl}"/>

        <property name="InitialPoolSize" value="${jdbc.initPoolSize}"/>
        <property name="MaxPoolSize" value="${jdbc.maxPoolSize}"/>
    </bean>
```
```
// pom.xml 注入依赖 mysql-connector-java
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.15</version>
    </dependency>
```
```
// 获取连接
public class JDBCTest {
    private ApplicationContext ctx;
    {
        ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
    }
    @Test
    public void testDataSource() throws SQLException {
        DataSource dataSource = ctx.getBean(DataSource.class);
        System.out.println(dataSource.getConnection());
    }
}
```

#### 使用JdbcTemplate操作数据库
```
// applicationContext.xml
    <!--导入资源文件-->
    <context:property-placeholder location="classpath:db.properties"/>

    <!--配置c3p0数据源-->
    <bean id="datasource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="User" value="${jdbc.user}"/>
        <property name="Password" value="${jdbc.password}"/>
        <property name="DriverClass" value="${jdbc.driverClass}"/>
        <property name="jdbcUrl" value="${jdbc.jdbcUrl}"/>

        <property name="InitialPoolSize" value="${jdbc.initPoolSize}"/>
        <property name="MaxPoolSize" value="${jdbc.maxPoolSize}"/>
    </bean>

    <!--配置Spring的JdbcTempplate-->
    <bean id ="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="datasource"></property>
    </bean>
```
```
// pom.xml注入依赖spring-jdbc
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.2.2.RELEASE</version>
    </dependency>
```
```
// JDBCTest.java
public class JDBCTest {

    private ApplicationContext ctx;
    private JdbcTemplate jdbcTemplate;
    {
        ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        jdbcTemplate = (JdbcTemplate)ctx.getBean("jdbcTemplate");
    }

    /**
     * 执行UPDATE
     */
    @Test
    public void testUpdate(){
        String sql = "UPDATE tbl_dept SET dept_name = ? WHERE dept_id = ?";
        jdbcTemplate.update(sql,"test",7);
    }

    /**
     * 执行INSERT
     */
    @Test
    public void testInsert(){
        String sql = "INSERT INTO tbl_dept(dept_name) VALUES(?)";
        jdbcTemplate.update(sql,"test6");
    }

    /**
     * 执行DELETE
     */
    @Test
    public void testDelete(){
        String sql = "DELETE FROM tbl_dept WHERE dept_id = ?";
        jdbcTemplate.update(sql,6);
    }

    /**
     * 执行批量更新：INSERT
     */
    @Test
    public void testBatchInsert(){
        String sql = "INSERT INTO tbl_dept(dept_name) VALUES(?) ";
        List<Object[]> batchArgs = new ArrayList<>();

        batchArgs.add(new Object[]{"test1"});
        batchArgs.add(new Object[]{"test2"});
        batchArgs.add(new Object[]{"test3"});
        batchArgs.add(new Object[]{"test4"});
        batchArgs.add(new Object[]{"test5"});

        jdbcTemplate.batchUpdate(sql,batchArgs);
    }

    /**
     * 执行批量更新：UPDATE
     */
    @Test
    public void testBatchUpdate(){
        String sql = "UPDATE tbl_dept SET dept_name = ? WHERE dept_id = ?";
        List<Object[]> batchArgs = new ArrayList<>();

        batchArgs.add(new Object[]{"update-test1",8});
        batchArgs.add(new Object[]{"update-test2",9});
        batchArgs.add(new Object[]{"update-test3",10});
        batchArgs.add(new Object[]{"update-test4",11});
        batchArgs.add(new Object[]{"update-test5",12});

        jdbcTemplate.batchUpdate(sql,batchArgs);
    }

    /**
     * 执行批量更新：DELETE
     */
    @Test
    public void testBatchDelete(){
        String sql = "DELETE FROM tbl_dept WHERE dept_id = ?";
        List<Object[]> batchArgs = new ArrayList<>();

        batchArgs.add(new Object[]{8});
        batchArgs.add(new Object[]{9});
        batchArgs.add(new Object[]{10});
        batchArgs.add(new Object[]{11});
        batchArgs.add(new Object[]{12});

        jdbcTemplate.batchUpdate(sql,batchArgs);
    }

     /**
     * 从数据库中获得一条记录，实际得到对应的一个对象
     * 调用queryForObject(String sql,RowMapper<Employee> rowMapper,Object... args)
     * 1. RowMapper，指定如何去映射结果集的行，常用的实现类为BeanPropertyRowMapper
     * 2. 使用Sql中列的别名完成列名和类的属性名的映射，例如last_name lastName
     */
    @Test
    public void testQueryForObject(){
        String sql = "SELECT id,last_name lastName,email FROM employees WHERE id > ?";
        RowMapper<Emoloyee> rowMapper = new BeanPropertyRowMapper<>(Emoloyee.class);
        Emoloyee emoloyee = jdbcTemplate.queryForObject(sql,rowMapper,1);
        System.out.println(emoloyee);
    }
  
    /**
     * 查到实体类的集合
     */
    @Test
    public void testQueryForList(){
        String sql = "SELECT id,last_name lastName,email FROM employees WHERE id > ?";
        RowMapper<Emoloyee> rowMapper = new BeanPropertyRowMapper<>(Emoloyee.class);
        List<Emoloyee> emoloyees = jdbcTemplate.query(sql,rowMapper,0);
        System.out.println(emoloyees);
    }

    /**
     * 获取单个列的值，或统计查询
     */
    @Test
    public void testQueryForObject2(){
        String sql = "SELECT count(id) FROM employees";
        long count = jdbcTemplate.queryForObject(sql,Long.class);
        System.out.println(count);
    }
}
```

#### 简化JDBC模版查询

由于每次使用都创建一个JdbcTemplate的新实例，这样的做法效率低下，JdbcTemplate类被设计称为线程安全的，可以可以在IOC容器中声明它的单个实例，并将这个实例注入到所有的DAO实例中。

Spring JDBC框架还提供了一个JdbcDaoSupport类来简化DAO实现，该类声明了jdbcTemplate属性，它可以从IOC容器中注入，或者自动从数据源中创建。

```
// EmployeeDao.java
@Repository
public class EmployeeDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public Employee get(Integer id){
        String sql = "SELECT id,last_name lastName,email FROM employees WHERE id = ?";
        RowMapper<Employee> rowMapper = new BeanPropertyRowMapper<>(Employee.class);
        Employee employee = jdbcTemplate.queryForObject(sql,rowMapper,id);
        return employee;
    }
}
```

```
// JDBCTest.java
public class JDBCTest {

    private ApplicationContext ctx;
    private EmployeeDao employeeDao;
    {
        ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        employeeDao = ctx.getBean(EmployeeDao.class);
    }

    @Test
    public void testEmployeeDao(){
        System.out.println(employeeDao.get(1));
    }
}
```

```
// applicationContext.xml
    <context:component-scan base-package="com.sangyu.test11"/>
    <!--导入资源文件-->
    <context:property-placeholder location="classpath:db.properties"/>

    <!--配置c3p0数据源-->
    <bean id="datasource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="User" value="${jdbc.user}"/>
        <property name="Password" value="${jdbc.password}"/>
        <property name="DriverClass" value="${jdbc.driverClass}"/>
        <property name="jdbcUrl" value="${jdbc.jdbcUrl}"/>

        <property name="InitialPoolSize" value="${jdbc.initPoolSize}"/>
        <property name="MaxPoolSize" value="${jdbc.maxPoolSize}"/>
    </bean>

    <!--配置Spring的JdbcTempplate-->
    <bean id ="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="datasource"></property>
    </bean>
```

## 十七、使用NamedParameterJdbcTemplate

在经典的JDBC用法中，SQL参数是用占位符？表示，并且收到位置的限制，定位参数的问题在于，一旦参数的顺序发生变化，就必须改变参数绑定。

在SpringJDBC框架中，绑定SQL参数的另一种选择是使用具名参数(named parameter)，SQL按名称(以冒号开头)进行指定

```
    <!--导入资源文件-->
    <context:property-placeholder location="classpath:db.properties"/>

    <!--配置c3p0数据源-->
    <bean id="datasource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="User" value="${jdbc.user}"/>
        <property name="Password" value="${jdbc.password}"/>
        <property name="DriverClass" value="${jdbc.driverClass}"/>
        <property name="jdbcUrl" value="${jdbc.jdbcUrl}"/>

        <property name="InitialPoolSize" value="${jdbc.initPoolSize}"/>
        <property name="MaxPoolSize" value="${jdbc.maxPoolSize}"/>
    </bean>

    <!--配置NamedParameterJdbcTemplate,该对象可以使用具名参数，其没有无参数的构造器，所以必须为其构造器指定参数-->
    <bean id = "namedParameterJdbcTemplate" class="org.springframework.jdbc.core.namedparam.NamedParameterJdbcTemplate">
        <constructor-arg ref="datasource"></constructor-arg>
    </bean>
```

```
public class JDBCTest {

    private ApplicationContext ctx;
    private NamedParameterJdbcTemplate namedParameterJdbcTemplate;
    {
        ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        namedParameterJdbcTemplate = (NamedParameterJdbcTemplate)ctx.getBean("namedParameterJdbcTemplate");
    }

    /**
     * 可以为参数命名
     * 使用具名参数时，SQL语句中的参数名和类的属性一致
     */
    @Test
    public void testNamedParameterJdbcTemplate(){
        String sql = "INSERT INTO employees(last_name,email) VALUES(:ln,:email)";
        Map<String,Object> paramMap = new HashMap<>();
        paramMap.put("ln","cc");
        paramMap.put("email","cc@cc.com");
        namedParameterJdbcTemplate.update(sql,paramMap);
    }

```

## 十八、事务管理

事务管理用来确保数据的完整性和一致性。事务就是一系列的工作，它们被当做一个单独的工作单元，这些动作要么全部完成，要么全部不起作用。

####事务的四个关键属性（ACID）

- 原子性：事务是一个原子操作，由一系列动作组成，事务的原子性确保动作要么全部完成要么完全不起作用

- 一致性：事务的执行的结果必须是使数据库从一个一致性状态变到另一个一致性状态。因此当数据库只包含成功事务提交的结果时，就说数据库处于一致性状态。如果数据库系统运行时发生故障，有些事务尚未完成就被迫中断，这些未完成事务对数据库所做的修改有一部分已写入物理数据库，这时数据库就处于一种不正确的状态，或者说是不一致的状态

- 隔离性：一个事务的执行不能有其他事务干扰。即一个事务内部的操作及使用的数据对其它并发事务是隔离的，并发之执行的各个事务之间不能互相干扰。事务的隔离界别有4级。

- 持续性：也称永久性，指一个事务一旦提交，它对数据库中的数据的改变就应该是永久的，不能回滚。接下来的其它操作或故障不应该对其执行结果有任何影响

####Spring中的事务管理

Spring在不同的事务管理API之上定义了一个抽象层，Spring既支持编程式事务管理，也支持声明式的事务管理。

- 编程式事务管理：将事务管理代码潜入到业务方法中来控制事务的提交和回滚

- 声明式事务管理：将事务管理代码从业务方法中分离出来，以声明的方式来实现事务管理，Spring通过Spring AOP框架支持声明式事务管理

Spring的核心事务管理抽象是```org.springframework.transaction.PlatformTransactionManager``` ,这是一个接口，封装了一组独立于技术的方法，无论使用Spring的哪种事务管理策略，事务管理器都是必须的。

####事务管理器的不同实现：

- ```org.springframework.jdbc.datasource.DataSourceTransactionManager``` : 在应用程序中只需要处理一个数据源，而且通过JDBC存取

- ```org.springframework.transaction.jta.JtaTransactionManager ``` 在JavaEE应用服务器上用JTA（Java Transaction API）进行事务管理

事务管理器最终以普通的Bean形式声明在Spring IOC容器中

## 事务的传播行为

当事务方法被另一个事务方法调用时，必须指定事务应该如何传播。例如：方法可能继续在现有事务中运行，也可能开启一个新事务，并在自己的事务中运行

Spring支持的事务传播行为

|传播属性 | 描述|
|--------|------|
|REQURED |  如果有事务在运行，当前的方法就在这个事务内运行，否则，就启动一个新的事务，并在自己的事务内运行|
|REQUIRED_NEW| 当前的定义方法必须启动新事务，并在它自己的事务内运行，如果有事务正在运行，应该将它挂起|

#### 并发事务所导致的问题

并发事务（当同一个应用程序或不同应用程序中的多个事务在同一个数据集上并行执行时）可能导致的问题：

- 脏读：一个事务正在访问数据，并且对数据进行了修改，而这种修改还没有提交到数据库中，这时，另外一个事务也访问这个数据，然后使用了这个数据

![](https://upload-images.jianshu.io/upload_images/2765653-340f92b3414d381d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 不可重复读：一个事务内，多次读同一个数据。在这个事务还没有结束时，另外一个事务也访问该统一数据，在第一个事务中的两次读数据之间，由于第二个事务的修改，那么第一个事务两次读到的数据可能是不一样。

![](https://upload-images.jianshu.io/upload_images/2765653-1c5543c19c79f731.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 幻读：第一个事务对一个表中的数据进行了修改，这种修改涉及到表中的全部数据行，同时，第二个事务也修改这个表中的数据，这种修改是向表中插入一行新数据。第一个事务同样的操作读取两次，得到的记录数并不相同

![](https://upload-images.jianshu.io/upload_images/2765653-b8c37bd451b80424.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

|隔离级别|描述|
|---------|--------|
| READ_UNCOMMITED|允许事务读取未其他事务提交的变更，脏读，不可重复读和幻读的问题都会出现|
|READ_COMMITED | 一个事务只能看见已经提交事务所做的改变，可以避免脏读，但不可重复读和幻读的问题仍旧会出现，这是默认的隔离级别|
| REPEATABLE——READ| 确保事务可以多次从一个字段读取相同的值，在这个事务持续期间，禁止其他事务对这个字段进行更新，可以避免脏读和不可重复读，但幻读的问题仍然存在 |
|SERIALZABLE | 确保事务可以从一个表中读取相同的行，在这个事务持续期间，禁止其他事务执行插入，更新和删除操作，所有并发都可以避免，但性能十分低下|
注意：事务的隔离级别受到数据库的限制，不同的数据库支持的的隔离级别不一定相同

```
// BookShopDao.java
public interface BookShopDao {

    // 根据书号获取书的单价
    public  int findBookPriceByIsbn(String isbn);

    // 更新书的库存，使书号对应的库存 -1
    public void updateBookStock(String isbn);

    // 更新用户的账户余额：使username的balacne - price
    public void updateUserAccount(String username,int price);
}
```

```
// BookShopDaoImpl.java
@Repository("bookShopDao") // 可以不命名，默认使用类名首字母小写
public class BookShopDaoImpl implements BookShopDao {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public int findBookPriceByIsbn(String isbn) {
        String sql = "SELECT price FROM book WHERE id = ?";
        return jdbcTemplate.queryForObject(sql,Integer.class,isbn);
    }

    @Override
    public void updateBookStock(String isbn) {
        // 检查书的库存是否足够，若不够，则抛出异常
        String sql2 = "SELECT stock FROM book_stock WHERE book_id = ?";
        int stock = jdbcTemplate.queryForObject(sql2,Integer.class,isbn);
        if(stock == 0){
            throw new BookStockException("库存不足！");
        }
        String sql = "UPDATE book_stock SET stock = stock - 1 WHERE book_id = ?";
        jdbcTemplate.update(sql,isbn);
    }

    @Override
    public void updateUserAccount(String username, int price) {
        String sql2 = "SELECT balance FROM accout WHERE user = ?";
        int balance = jdbcTemplate.queryForObject(sql2,Integer.class,username);
        if(balance < price){
            throw new UserAccountException("余额不足！");
        }
        String sql = "UPDATE accout SET balance = balance - ? WHERE user = ?";
        jdbcTemplate.update(sql,price,username);
    }
}
```
```
// BookShopService.java
public interface BookShopService {
    public void purchase(String username,String isbn);
}
```

```
// BookShopServiceImpl.java
@Service("bookShopService")
public class BookShopServiceImpl implements BookShopService {

    @Autowired
    private BookShopDao bookShopDao;

    // -->添加事务注解
    // -->使用propagation 指定事务的传播行为，即当前的事务方法被另一个事务方法调用时
    // 如何使用事务，默认取值为 REQUIRED，即使用调用方法的事务
    // REQUIRED_NEW：事务自己的事务，调用的事务方法的事务被挂起
    // -->使用isolation 指定事务的隔离级别，最常用的取值为READ_COMMITTED
    // 默认情况下Spring的声明式事务对所有的运行时异常进行回滚，也可以通过对应的属性进行设置，通常情况下默认值即可
    // -->使用timeout指定强制回滚之前事务可以占用的时间
    // -->使用readOnly指定事务是否为只读。表示这个事务只读取事务但不更新数据
    @Transactional(propagation = Propagation.REQUIRED,isolation = Isolation.READ_COMMITTED,
                    noRollbackFor = {UserAccountException.class},
                    timeout = 3,readOnly = false)
    @Override
    public void purchase(String username, String isbn) {
        // 1. 获取书的单价
        int price = bookShopDao.findBookPriceByIsbn(isbn);

        // 2. 更新书的库存
        bookShopDao.updateBookStock(isbn);

        // 3. 更新用户余额
        bookShopDao.updateUserAccount(username,price);
    }
}
```

```
// BookStockException.java
public class BookStockException extends RuntimeException {

    private static final long sericlVersionUID = 1L;

    public BookStockException(){
        super();
    }

    public BookStockException(String message,Throwable cause,
                                   boolean enableSuppression,boolean writeableStackTrace){
        super(message,cause,enableSuppression,writeableStackTrace);
    }

    public BookStockException(String message,Throwable cause){
        super(message,cause);
    }

    public BookStockException(String message){
        super(message);
    }

    public BookStockException(Throwable cause){
        super(cause);
    }

}
```

```
// SpringTransactionTest.java
public class SpringTransactionTest {
    private ApplicationContext ctx = null;
    private BookShopDao bookShopDao = null;
    private BookShopService bookShopService = null;
    {
        ctx = new ClassPathXmlApplicationContext("applicationContext.xml");
        bookShopDao = ctx.getBean(BookShopDao.class);
        bookShopService = ctx.getBean(BookShopService.class);
    }

    @Test
    public void testBookShopDaoFindPriceByIsbn(){
        System.out.println(bookShopDao.findBookPriceByIsbn("2"));
    }

    @Test
    public void testBookShopDaoUpdateBookStock(){
        bookShopDao.updateBookStock("1");
    }

    @Test
    public void testUpdateUserAccount(){
        bookShopDao.updateUserAccount("ada",1);
    }

    @Test
    public void testBookShopService(){
        bookShopService.purchase("ada","1");
    }
}
```

```
// UserAccountException.java
public class UserAccountException extends RuntimeException {

    private static final long serialVersionUID = 1L;

    public UserAccountException(){
        super();
    }

    public UserAccountException(String message,Throwable cause,
                              boolean enableSuppression,boolean writeableStackTrace){
        super(message,cause,enableSuppression,writeableStackTrace);
    }

    public UserAccountException(String message,Throwable cause){
        super(message,cause);
    }

    public UserAccountException(String message){
        super(message);
    }

    public UserAccountException(Throwable cause){
        super(cause);
    }
}
```


```
// applicationContext.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.0.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd">

    <context:component-scan base-package="com.sangyu.test12"/>
    <!--导入资源文件-->
    <context:property-placeholder location="classpath:db.properties"/>

    <!--配置c3p0数据源-->
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="User" value="${jdbc.user}"/>
        <property name="Password" value="${jdbc.password}"/>
        <property name="DriverClass" value="${jdbc.driverClass}"/>
        <property name="jdbcUrl" value="${jdbc.jdbcUrl}"/>

        <property name="InitialPoolSize" value="${jdbc.initPoolSize}"/>
        <property name="MaxPoolSize" value="${jdbc.maxPoolSize}"/>
    </bean>

    <!-- 配置 Spirng 的 JdbcTemplate -->
    <bean id="jdbcTemplate"
          class="org.springframework.jdbc.core.JdbcTemplate">
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <!--配置NamedParameterJdbcTemplate,该对象可以使用具名参数，其没有无参数的构造器，所以必须为其构造器指定参数-->
    <bean id="namedParameterJdbcTemplate" class="org.springframework.jdbc.core.namedparam.NamedParameterJdbcTemplate">
        <constructor-arg ref="dataSource"></constructor-arg>
    </bean>

    <!--配置bean-->
    <bean class="com.sangyu.test12.BookShopDao" abstract="true"></bean>
    <bean class="com.sangyu.test12.BookShopService" abstract="true"></bean>


    <!-- 配置事务管理器 -->
    <bean id="transactionManager"
          class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"></property>
    </bean>

    <!-- 启用事务注解 -->
    <tx:annotation-driven transaction-manager="transactionManager"/>
</beans>
```

## 十九、spring - 生命周期

Spring  IOC容器对Bean的生命周期进行管理的过程：

1）通过构造器或工厂方法创建Bean实例
2）为Bean的属性设置值和对其他Bean的引用
3）调用Bean的初始化方法
4）Bean可以使用了
5）当容器关闭时，调用Bean的销毁方法

可以在Bean的声明里设置init-method 和destory-method属性，为Bean指定初始化和销毁方法

 
#### 创建bean后置处理器

Bean后置处理器允许在调用初始化方法前后对Bean进行额外的处理。对IOC容器里所有的Bean实例逐一处理，而非单一实例，典型的应用是：检查Bean属性的正确性或根据特定的标准更改Bean的属性

对Bean后置处理器而言，需要实现```org.springframework.beans.factory.config.BeanPostProcessor```接口，在初始化方法被调用前后，Spring将把每个Bean实例分别传递给上述接口的两个方法:

```
public interface BeanPostProcessor {
    @Nullable
    default Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        return bean;
    }

    @Nullable
    default Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        return bean;
    }
}
```

#### 添加Bean后置处理器后Bean的生命周期

1）通过构造器或工厂方法创建Bean实例
2）为Bean的属性设置值和对其他Bean的引用
3）将Bean实例传递给Bean后置处理器的postProcessBeforeInitialization 方法
4）调用Bean的初始化方法
5）将Bean实例传递给Bean后置处理器的postProcessAfterInitialization方法
6）Bean可以使用了
7）当容器关闭时，调用Bean的销毁方法

```
//applicationContext.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id = "car" class="com.sangyu.test13.Car" init-method="init" destroy-method="destory">
        <property name="brand" value="Audi"></property>
    </bean>

    <!--
            实现BeanPostProcessor接口，并提供具体实现
            postProcessBeforeInitialization，postProcessAfterInitialization
            bean:bean实例本身
            beanName：IOC容器配置的bean的名字
            返回值：是实际上返回给用户的那个bean，可以返回一个新的bean

     -->
    <!-- 配置bean的后置处理器 -->
    <bean class="com.sangyu.test13.MyBeanPostProcessor"></bean>
</beans>
```

```
// Car.java
public class Car {

    public Car(){
        System.out.println("Car's Constructor...");
    }

    private String brand;

    public void setBrand(String brand){
        System.out.println("setBrand...");
        this.brand = brand;
    }

    public void init(){
        System.out.println("init...");
    }

    public void destory(){
        System.out.println("destory");
    }

    @Override
    public String toString() {
        return "Car{" +
                "brand='" + brand + '\'' +
                '}';
    }
}
```

```
// Main.java
public class Main {
    public static void main(String[] args) {
        ClassPathXmlApplicationContext ctx = new ClassPathXmlApplicationContext("applicationContext.xml");

        Car car = (Car) ctx.getBean("car");
        System.out.println(car);
        // 关闭IOC容器
        ctx.close();
    }
}
```

```
// MyBeanPostProcessor.java
public class MyBeanPostProcessor implements BeanPostProcessor {

    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("postProcessBeforeInitialization: " + beanName + ", " + beanName );
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("postProcessAfterInitialization: " + beanName + ", " + beanName);
        Car car = new Car();
        car.setBrand("Ford");
        return car;
    }
}
```


