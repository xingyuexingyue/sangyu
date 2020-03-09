## 目录

[一、SpringBoot 项目创建](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E4%B8%80springboot---helloworld)

[二、使用向导快速创建SpringBoot项目](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E4%BA%8C%E4%BD%BF%E7%94%A8%E5%90%91%E5%AF%BC%E5%BF%AB%E9%80%9F%E5%88%9B%E5%BB%BAspringboot%E9%A1%B9%E7%9B%AE)

[三、YAML](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E4%B8%89yaml)

[四、@Value和@CongigurationProperties比较](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%9B%9Bvalue%E5%92%8Ccongigurationproperties%E6%AF%94%E8%BE%83)

[五、@Propertysource和@ImportResource比较](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E4%BA%94propertysource-importresource%E6%AF%94%E8%BE%83)

[六、配置文件占位符](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%85%AD%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%8D%A0%E4%BD%8D%E7%AC%A6)

[七、profile 多环境支持](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E4%B8%83profile-%E5%A4%9A%E7%8E%AF%E5%A2%83%E6%94%AF%E6%8C%81)

[八、配置文件加载位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%85%AB%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%8A%A0%E8%BD%BD%E4%BD%8D%E7%BD%AE)

[九、springboot日志默认配置](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E4%B9%9Dspringboot%E6%97%A5%E5%BF%97%E9%BB%98%E8%AE%A4%E9%85%8D%E7%BD%AE)

[十、指定日志配置文件和日志profile功能](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%8D%81%E6%8C%87%E5%AE%9A%E6%97%A5%E5%BF%97%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E5%92%8C%E6%97%A5%E5%BF%97profile%E5%8A%9F%E8%83%BD)

[十一、webjars&静态资源映射规则](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%8D%81%E4%B8%80webjars%E9%9D%99%E6%80%81%E8%B5%84%E6%BA%90%E6%98%A0%E5%B0%84%E8%A7%84%E5%88%99)

[十二、引入模板引擎thymeleaf](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%8D%81%E4%BA%8C%E5%BC%95%E5%85%A5%E6%A8%A1%E6%9D%BF%E5%BC%95%E6%93%8Ethymeleaf)

[十三、springboot 2.0 + Redis](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%8D%81%E4%B8%89springboot-20--redis)

[十四、springboot + 消息队列](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%8D%81%E5%9B%9Bspringboot--%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97)

[十五、springboot 整合 ElasticSearch](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%8D%81%E4%BA%94springboot-%E6%95%B4%E5%90%88-elasticsearch)

[十六、springboot-任务](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringBoot.md#%E5%8D%81%E5%85%ADspringboot-%E4%BB%BB%E5%8A%A1)

## 一、SpringBoot - HelloWorld

1、 创建新的project

![](https://upload-images.jianshu.io/upload_images/2765653-a91ba6bc2b7808a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

选择Maven工程

![](https://upload-images.jianshu.io/upload_images/2765653-60073622a6b358f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

对项目命名

![](https://upload-images.jianshu.io/upload_images/2765653-d0a9df5a228ab8ee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

选择自动下载maven中的jar包

![](https://upload-images.jianshu.io/upload_images/2765653-52958ef0d13d2e88.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2、pom.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.test</groupId>
    <artifactId>MySpringBoot</artifactId>
    <version>1.0-SNAPSHOT</version>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.5.9.RELEASE</version>
    </parent>

<!--
    spring-boot-starter：spring-boot场景启动器，帮我们导入了web模块正常运行所依赖的组件
    SpringBoot将所有功能场景都抽取出来，做成了一各个的starters（启动器），只需要在项目里面引入这些starter相关场景的所有依赖都会导入出来，要用什么功能就导入什么场景的启动器
 -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

</project>
```

我这里pom.xml抛出了一个异常

![](https://upload-images.jianshu.io/upload_images/2765653-573cd90f6c28c998.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

解决办法：1、打开配置 2、把自己本地的Maven仓库settings.xml加进去后，选择apply后，ok就好了

![](https://upload-images.jianshu.io/upload_images/2765653-6b43d6d690788766.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/2765653-d3028c0cf134776a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3、编写代码，将java文件配置成Sources Root，选中java文件右键点击Make Directory as，打开后选择Sources Root即可，这个时候java前面的灰色图标会变成蓝色的。之后在java文件下创建包和java文件，按照下图目录

![](https://upload-images.jianshu.io/upload_images/2765653-7d85436e07f5a01d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication // 标注一个主程序类，说明这是一个SpringBoot应用
public class HelloWorldMainApplication {
    public static void main(String[] args) {
        SpringApplication.run(HelloWorldMainApplication.class,args); // Spring应用启动起来
    }
}
```

```
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @ResponseBody
    @RequestMapping("/hello")
    public String hello(){
        return "Hello World!";
    }
}
```

7、运行项目，直接在main方法运行即可。

![](https://upload-images.jianshu.io/upload_images/2765653-4e1561511d827c13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

执行结果

![](https://upload-images.jianshu.io/upload_images/2765653-34ee37d8a39fa98c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8、其他：将应用打包成一个可执行的jar包

在pom.xml中增加配置

```
<build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
```

![](https://upload-images.jianshu.io/upload_images/2765653-f0031b386f6fdd46.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-ff1044a910dc26c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

jar 包可以直接在命令行运行 

```
java -jar  /Users/xxx/spring-test01/MySpringBoot/target/MySpringBoot-1.0-SNAPSHOT.jar
```
![](https://upload-images.jianshu.io/upload_images/2765653-b50252d648fc8b23.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 二、使用向导快速创建SpringBoot项目

1、使用Spring Initialize向导创建项目

![](https://upload-images.jianshu.io/upload_images/2765653-a91ba6bc2b7808a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-1d288ea8d3ff6602.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-59854ed87cbaa9b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-bf4b67ca8d233500.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-23f279bded2ab434.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2、创建成功后springboot相关的在pom.xml中配置已经注入成功了

3、创建HelloController.java文件

![](https://upload-images.jianshu.io/upload_images/2765653-edec3d0dcb2e9809.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

// 这个类的所有方法返回的数据直接写给浏览器，如果是对象转为json数据
//@Controller
//@ResponseBody
@RestController  // 相当于 @Controller @ResponseBody
public class HelloController {
    @RequestMapping("/hello")
    public String hello(){
        return "Hello World!";
    }
}
```

4、resources下的目录文件

![](https://upload-images.jianshu.io/upload_images/2765653-b1a7e7ed2f06201e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- static：保存所有的静态资源：js、css、images
- templates：保存所有的模板页面；（SpringBoot默认jar包使用嵌入式的Tomcat，默认不支持JSP页面）；可以使用模板引擎（freemarker、thymeleaf）
- application.properties：SpringBoot应用的配置文件；可以修改一些默认设置，比如修改端口号将默认的端口号8080修改为8081

![](https://upload-images.jianshu.io/upload_images/2765653-cc7b7950394d4baf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 三、YAML

SpringBoot支持使用一个全局的配置配置文件，目录在```src/main/resources或者类路径/config```，全局配置文件可以对一些默认配置值进行修改，配置文件名是固定的：application.properties或application.yml


yaml是YAML语言的文件，以数据为中心，比json、xml等更适合做配置文件 [参考官方语法规范](https://yaml.org/)

1、YAML语法

- k:(空格)v：表示一对键值对切中间的空格必须有，不能省略
- 使用缩进表示层级关系,只要是左对齐的一列数据，都是同一个层级
 ```
server:
  port: 8082
  path: /hello
```
- 属性和值大小写敏感

2、值的写法

- 字面量：普通的值（数字、字符串、布尔）
k: v  字面直接写，字符串默认不用加上单引号或双引号，如果包含" ",表示不会转义字符串内包含的特殊字符，如果包含' '，表示会转义字符串内的特殊字符，特殊字符最终只是一个普通的字符串数据
- 对象、Map(属性和值)（键值对）
k: v   在下一行写对象的属性和值的关系；
```
friends:
    lastName: aa
    age: 20
// 行内写法
friends: {lastName:aa,age:20}
```
- 数组（List，Set）

```
// 用- 表示数组中的一个元素
pets:
    - cat
    - dog
    - pig
// 行内写法
pets: [cat,dog,pig]
```


```
public class Dog {
    private String name;
    private Integer age;
    @Override
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
    public void setName(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
    public void setAge(Integer age) {
        this.age = age;
    }
    public Integer getAge() {
        return age;
    }
}
```

```
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

import java.util.Date;
import java.util.List;
import java.util.Map;

/**
 * 将配置文件中配置的每一个属性的值，映射到这个组件中
 * @ConfigurationProperties(prefix = "person") 告诉SpringBoot将本类中的所有属性和配置文件中相关的配置进行绑定
 * (prefix = "person") 配置文件文件中哪个下面的所有属性进行一一映射
 */
@Component
@ConfigurationProperties(prefix = "person")
public class Person {
    private String lastName;
    private Integer age;
    private Boolean boss;
    private Date birth;

    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public void setBoss(Boolean boss) {
        this.boss = boss;
    }

    public void setBirth(Date birth) {
        this.birth = birth;
    }

    public void setMaps(Map<String, Object> maps) {
        this.maps = maps;
    }

    public void setDog(Dog dog) {
        this.dog = dog;
    }

    public void setLists(List<Object> lists) {
        this.lists = lists;
    }

    public Integer getAge() {
        return age;
    }

    public Date getBirth() {
        return birth;
    }

    public String getLastName() {
        return lastName;
    }

    public Boolean getBoss() {
        return boss;
    }

    public Dog getDog() {
        return dog;
    }

    public List<Object> getLists() {
        return lists;
    }

    public Map<String, Object> getMaps() {
        return maps;
    }

    @Override
    public String toString() {
        return "Person{" +
                "lastName='" + lastName + '\'' +
                ", age=" + age +
                ", boss=" + boss +
                ", birth=" + birth +
                ", maps=" + maps +
                ", lists=" + lists +
                ", dog=" + dog +
                '}';
    }
}
```

```
server:
  port: 8082
person:
  last-name: hello
  age: 18
  boss: false
  birth: 2017/12/12
  maps: {k1: v1,k2: 12}
  lists:
    - lisi
    - zhaoliu
  dog:
    name: 狗狗
    age: 12
```

```
import com.sangyu.springboot.bean.Person;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

/**
 * Spring 单元测试
 * 可以在测试期间很方便类似编码一样进行自动注入容器等
 */
@RunWith(SpringRunner.class)
@SpringBootTest
public class MySpringBoot01ApplicationTests {

	@Autowired
	Person person;
	@Test
	public void contextLoads() {
		System.out.println(person);
	}
}
```
可能会提示一个异常

![](https://upload-images.jianshu.io/upload_images/2765653-4e5edf2c9e309ddf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如何解决：在pom.xml中注入

```
<!--导入配置文件处理器，配置文件进行绑定就会有提示-->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-configuration-processor</artifactId>
      <optional>true</optional>
</dependency>
```

## 四、@Value和@CongigurationProperties比较


|属性|	@CongigurationProperties| @Value|
|---|--|--|
|功能|批量注入配置文件中的属性|一个个指定 |
|松散绑定(松散语法)|支持|不支持 |
|spEL|不支持|支持 |
|JSP303数据校验|支持|不支持 |

```
@Component
//@ConfigurationProperties(prefix = "person")
public class Person {

    @Value("${person.last-name}") // 从配置文件获取
    private String lastName;
    @Value("#{11*2}") // 直接计算 spEL表达式
    private Integer age;
    @Value("true") // 字面量
    private Boolean boss;
    private Date birth;
    private Map<String,Object> maps;
    private List<Object> lists;
    private Dog dog;
```

```
#application.properties
#server.port = 8081
#配置person的值
person.last-name=张三
person.age=16
#person.age=#{11*2}  //不支持spEL（表达式语言）
person.birth=2017/12/15
person.boss=false
person.maps.k1 = v1
person.maps.k2 = 14
person.lists=a,b,c
```

**如何选择@Value和@CongigurationProperties**

配置文件yml还是properties他们都能获取到值；如果只是在某个业务逻辑中需要获取配置文件中的某项值，使用@Value；如果专门编写一个javaBean来和配置文件进行映射，就直接使用@CongigurationProperties

```
@RestController  // 相当于 @Controller @ResponseBody
public class HelloController {

    @Value("${person.last-name}") // 从配置文件获取
    private String name;

    @RequestMapping("/hello")
    public String hello() {
        return "Hello World!" + name;
    }
}
```

**@ConfigurationProperties校验通过添加JSR-303 javax.validation约束注解**

```
@Component
@ConfigurationProperties(prefix = "person")
@Validated // 添加JSR-303 javax.validation约束注解
public class Person {
    @Email // lastName必须是邮箱格式
    private String lastName;
    @Value("#{11*2}") // 直接计算 spEL表达式
    private Integer age;
    @Value("true") // 字面量
    private Boolean boss;
    private Date birth;

    private Map<String, Object> maps;
    private List<Object> lists;
    private Dog dog;
}
```

## 五、@Propertysource和@ImportResource比较

@CongigurationProperties与@Propertysource结合读取指定配置文件（只能用于properties文件）

```
@PropertySource(value = {"classpath:person.properties"})
@Component
@ConfigurationProperties(prefix = "person")
@Validated // 添加JSR-303 javax.validation约束注解
public class Person {

    //    @Value("${person.last-name}") // 从配置文件获取
    @Email // lastName必须是邮箱格式
    private String lastName;
    @Value("#{11*2}") // 直接计算 spEL表达式
    private Integer age;
    @Value("true") // 字面量
    private Boolean boss;
    private Date birth;

    private Map<String, Object> maps;
    private List<Object> lists;
    private Dog dog;
}
```

@ImportResource 导入Spring的配置文件，让配置文件里面的内容生效
SpringBoot里面没有Spring的配置文件，我们自己编写的配置文件，也不能自动识别；通过将@ImportResource标注在一个配置类上，让Spring的配置文件生效

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean id="helloService" class="com.sangyu.springboot.service.HelloService"></bean>
</beans>
```

```
@ImportResource(locations = {"classpath:beans.xml"})
@SpringBootApplication
class MySpringBoot01Application {

	public static void main(String[] args) {
		SpringApplication.run(MySpringBoot01Application.class, args);
	}
}
```
```
public class HelloService {
}
```

```
/**
 * Spring 单元测试
 * 可以在测试期间很方便类似编码一样进行自动注入容器等
 */
@RunWith(SpringRunner.class)
@SpringBootTest
public class MySpringBoot01ApplicationTests {
	@Autowired
	Person person;
	@Autowired
	ApplicationContext ioc;
	@Test
	public void contextLoads() {
		System.out.println(person);
	}
	@Test
	public void testHelloService(){
		boolean b = ioc.containsBean("helloService");
		System.out.println("====");

		System.out.println(b);
	}
}
```

## 六、配置文件占位符

1、随机数
```
${random.value}、${random.int}、${random.long}
${random.int(10)}、${random.int[1024,65536]}
```
2、占位符获取之前配置的值，如果没有可以用：指定默认值
```
person.lastName=张三${random.uuid}
person.age=${random.int(10)}
person.birth=2017/12/15
person.boss=false
person.maps.k1=v1
person.maps.k2=14
person.lists=a,b,c
person.dog.name=${person.hello:hello}_dog
person.dog.age=15
```

## 七、profile 多环境支持

1、多Profile文件

在写主配置文件时，文件名可以是 application-{profile}.properties/yml
默认使用application.properties的配置

```
# application.properties
server.port=8081
spring.profiles.active=dev //  在application.properties配置文件中指定激活Profile，此时application.properties是主配置文件
```

```
# application-dev.properties
server.port=8082
```

```
# application-prod.properties
server.port=8083
```

2、使用yml配置多文档块方式

```
server:
  port: 8081
spring:
  profiles:
    active: dev // 激活profile ，如果不激活默认是8081

---
server:
  port: 8083
spring:
  profiles: dev

---

server:
  port: 8084
spring:
  profiles: prod
```

3、命令行方式：支持properties和yml文件

```
--spring.profiles.active=prod
```

![](https://upload-images.jianshu.io/upload_images/2765653-688311f55074f1b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


4、命令行直接运行jar包的时，增加命令行参数

```
java -jar /Users/aaa/spring-test01/my-springboot-demo02/target/my-springboot-demo02-0.0.1-SNAPSHOT.jar --spring.profiles.active=dev
```

![](https://upload-images.jianshu.io/upload_images/2765653-ebf7f2bc2cc45ec5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 八、配置文件加载位置

spring boot 启动会扫描以下位置的application.properties或者appliation.yml文件作为Spring Boot的默认配置文件，并且优先级按照从高到低的顺序，所有位置的文件都会被加载，高优先级配置内容会覆盖低优先级配置内容：

-file:./config/
-file:./
-classpath:/config
-classpath:/


![](https://upload-images.jianshu.io/upload_images/2765653-34fb2e7a81ca4e63.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

配置项目的访问路径

```
server.port=8081

# 配置项目的访问路径
server.servlet.context-path=/boot02
```

```
@RestController
public class HelloController {

    @RequestMapping("/hello")
    public String hello(){
        return "hello";
    }
}
```

![](https://upload-images.jianshu.io/upload_images/2765653-a36073fbb84e2cd9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 九、springboot日志默认配置

```
# application.properties 中修改日志的输出级别
# 对某个包某个类调整日志的输出级别
logging.level.com.sangyu=trace
```

```
import org.junit.Test;
import org.junit.runner.RunWith;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.context.junit4.SpringRunner;

@RunWith(SpringRunner.class)
@SpringBootTest
public class MySpringbootDemo03ApplicationTests {

	// 记录器
	Logger logger = LoggerFactory.getLogger(getClass()); // 注意使用slf4j包

	/**
	 * 日志的级别
	 * 由低到高：trace<debug<info<warn<error
	 * 可以调整输出的日志级别，日志就只会在这个级别以后的高级别生效
	 */
	@Test
	public void contextLoads() {
		logger.trace("这是trace日志...");
		logger.debug("这是debug日志...");
		// SpringBoot默认给我们使用的是info级别的，没有指定级别的就用SpringBoot默认规定的级别：root级别
		logger.info("这是info日志...");
		logger.warn("这是warn日志...");
		logger.error("这是error日志...");
	}
}
```

```
2020-02-20 11:27:25.936 TRACE 7840 --- [           main] c.s.s.MySpringbootDemo03ApplicationTests : 这是trace日志...
2020-02-20 11:27:25.936 DEBUG 7840 --- [           main] c.s.s.MySpringbootDemo03ApplicationTests : 这是debug日志...
2020-02-20 11:27:25.936  INFO 7840 --- [           main] c.s.s.MySpringbootDemo03ApplicationTests : 这是info日志...
2020-02-20 11:27:25.937  WARN 7840 --- [           main] c.s.s.MySpringbootDemo03ApplicationTests : 这是warn日志...
2020-02-20 11:27:25.937 ERROR 7840 --- [           main] c.s.s.MySpringbootDemo03ApplicationTests : 这是error日志...
```

日志输出

|logging.file|logging.path|Example| Description|
|--|--|--| --|
|(none)  | (none)  |  | 只在控制台输出| 
|指定文件名 | (none)  | my.log | 输出日志到my.log文件| 
| (none) | 指定目录 | /var/log | 输出到指定目录的spring.log文件| 


```
# application.properties 
# 不指定路径在当前项目下生成springboot.log日志
logging.file=springboot.log
```

![](https://upload-images.jianshu.io/upload_images/2765653-23a74e6fa0e72093.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
# application.properties 
# 在当前磁盘的根路径下创建spring文件夹和里面的log文件夹，使用spring.log作为默认文件
logging.path=/Users/aaa/Documents/spring/log
```

![](https://upload-images.jianshu.io/upload_images/2765653-10d5e8ff94cf75c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

日志输出格式

```
%d 表示日期时间
%thread 表示线程名
%-Slevel 线程从左显示5个字符宽度
%logger{50} 表示logger名字最长50个字符，否则按照句点分隔
%msg 日志消息
%n 换行符
```
```
# application.properties 
# 在控制台输出的日志的格式
logging.pattern.console=%d{yyyy-MM-dd} [%thread] %-5level %logger{50} - %msg%n

# 指定文件中日志输出的格式
logging.pattern.file=%d{yyyy-MM-dd} === [%thread] === %-5level === %logger{50} ==== %msg%n
```

## 十、指定日志配置文件和日志profile功能

在类路径下放每个日志框架自己的配置文件；SpringBoot就不再使用默认配置文件了。但要注意的是：```logback.xml```直接就被日志框架识别了；```logback-spring.xml```日志框架就不直接加载日志但配置项，由SpringBoot解析日志配置，可以使用SpringBoot的高级Profile功能

![](https://upload-images.jianshu.io/upload_images/2765653-7a989d7b0b4614cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```
<?xml version="1.0" encoding="UTF-8"?>
<!--
scan：当此属性设置为true时，配置文件如果发生改变，将会被重新加载，默认值为true。
scanPeriod：设置监测配置文件是否有修改的时间间隔，如果没有给出时间单位，默认单位是毫秒当scan为true时，此属性生效。默认的时间间隔为1分钟。
debug：当此属性设置为true时，将打印出logback内部日志信息，实时查看logback运行状态。默认值为false。
-->
<configuration scan="false" scanPeriod="60 seconds" debug="false">
    <!-- 定义日志的根目录 -->
    <property name="LOG_HOME" value="/Users/pengyapan/Documents/spring/log" />
    <!-- 定义日志文件名称 -->
    <property name="appName" value="sangyu-springboot"></property>
    <!-- ch.qos.logback.core.ConsoleAppender 表示控制台输出 -->
    <appender name="stdout" class="ch.qos.logback.core.ConsoleAppender">
        <!--
        日志输出格式：
			%d表示日期时间，
			%thread表示线程名，
			%-5level：级别从左显示5个字符宽度
			%logger{50} 表示logger名字最长50个字符，否则按照句点分割。 
			%msg：日志消息，
			%n是换行符
        -->
<!--        指定某段配置只在某个环境下生效-->
        <layout class="ch.qos.logback.classic.PatternLayout">
            <springProfile name="dev">
                <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} ----> [%thread] ---> %-5level %logger{50} - %msg%n</pattern>
            </springProfile>
            <springProfile name="!dev">
                <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} ==== [%thread] ==== %-5level %logger{50} - %msg%n</pattern>
            </springProfile>
        </layout>
    </appender>

    <!-- 滚动记录文件，先将日志记录到指定文件，当符合某个条件时，将日志记录到其他文件 -->  
    <appender name="appLogAppender" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!-- 指定日志文件的名称 -->
        <file>${LOG_HOME}/${appName}.log</file>
        <!--
        当发生滚动时，决定 RollingFileAppender 的行为，涉及文件移动和重命名
        TimeBasedRollingPolicy： 最常用的滚动策略，它根据时间来制定滚动策略，既负责滚动也负责出发滚动。
        -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <!--
            滚动时产生的文件的存放位置及文件名称 %d{yyyy-MM-dd}：按天进行日志滚动 
            %i：当文件大小超过maxFileSize时，按照i进行文件滚动
            -->
            <fileNamePattern>${LOG_HOME}/${appName}-%d{yyyy-MM-dd}-%i.log</fileNamePattern>
            <!-- 
            可选节点，控制保留的归档文件的最大数量，超出数量就删除旧文件。假设设置每天滚动，
            且maxHistory是365，则只保存最近365天的文件，删除之前的旧文件。注意，删除旧文件是，
            那些为了归档而创建的目录也会被删除。
            -->
            <MaxHistory>365</MaxHistory>
            <!-- 
            当日志文件超过maxFileSize指定的大小是，根据上面提到的%i进行日志文件滚动 注意此处配置SizeBasedTriggeringPolicy是无法实现按文件大小进行滚动的，必须配置timeBasedFileNamingAndTriggeringPolicy
            -->
            <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
                <maxFileSize>100MB</maxFileSize>
            </timeBasedFileNamingAndTriggeringPolicy>
        </rollingPolicy>
        <!-- 日志输出格式： -->     
        <layout class="ch.qos.logback.classic.PatternLayout">
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [ %thread ] - [ %-5level ] [ %logger{50} : %line ] - %msg%n</pattern>
        </layout>
    </appender>

    <!-- 
		logger主要用于存放日志对象，也可以定义日志类型、级别
		name：表示匹配的logger类型前缀，也就是包的前半部分
		level：要记录的日志级别，包括 TRACE < DEBUG < INFO < WARN < ERROR
		additivity：作用在于children-logger是否使用 rootLogger配置的appender进行输出，
		false：表示只用当前logger的appender-ref，true：
		表示当前logger的appender-ref和rootLogger的appender-ref都有效
    -->
    <!-- hibernate logger -->
    <logger name="com.sangyu" level="debug" />
    <!-- Spring framework logger -->
    <logger name="org.springframework" level="debug" additivity="false"></logger>



    <!-- 
    root与logger是父子关系，没有特别定义则默认为root，任何一个类只会和一个logger对应，
    要么是定义的logger，要么是root，判断的关键在于找到这个logger，然后判断这个logger的appender和level。 
    -->
    <root level="info">
        <appender-ref ref="stdout" />
        <appender-ref ref="appLogAppender" />
    </root>
</configuration> 
```

```
#application.properties
server.port=8081

# 激活环境
spring.profiles.active=dev 
```

## 十一、webjars&静态资源映射规则

pom.xml 注入资源

```
<!--        引入jquery-webjar-->
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>jquery</artifactId>
            <version>3.3.1</version>
        </dependency>
```

1、webjars 是jar包的方式引入静态资源，所有/webjars/**，都去classpath:/META-INF/resources/webjars/资源

 [pom注入资源后启动应用可访问](http://localhost:8080/webjars/jquery/3.3.1/jquery.js)


![image.png](https://upload-images.jianshu.io/upload_images/2765653-8fd3d0047b79a268.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2、```/**```访问当前项目的任何资源，（静态资源的文件夹）

```
classpath:/META-INF/resources/
classpath:/resources/
classpath:/static/
classpath:/public/
/ 当前项目的根路径 
```


创建index.html

![](https://upload-images.jianshu.io/upload_images/2765653-ac79fda847c0a611.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3、欢迎页，静态资源文件下查找所有index.html页面；被"/**"映射， [访问index页面](http://localhost:8080/)

![](https://upload-images.jianshu.io/upload_images/2765653-424984f340898a90.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/2765653-c29e65ce59352c20.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/2765653-2877e4cbf7321aae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4）所有的**/favicon.ico都是在静态资源文件下查找

![](https://upload-images.jianshu.io/upload_images/2765653-4bdedc165e46f696.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 十二、引入模板引擎thymeleaf

1、pom.xml 注入模板引擎thymeleaf依赖，切换thymeleaf版本为3.0

```
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
    <java.version>1.8</java.version>
    <thymeleaf.version>3.0.2.RELEASE</thymeleaf.version>
<!--        布局功能的支持程序thymeleaf3主程序 layout2以上版本-->
<!--        thymeleaf2 layoout1-->
    <thymeleaf-layout-dialect.version>2.1.1</thymeleaf-layout-dialect.version>
</properties>
 <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```
2、thymeleaf语法

```
@Controller
public class HelloController {
    @ResponseBody
    @RequestMapping("/hello")
    public String hello(){
        return "Hello World";
    }
    @RequestMapping("/success")
    public String success(){
        // classpath:/templates/success.html
        return "success";
    }
}
```

![](https://upload-images.jianshu.io/upload_images/2765653-b8283571b8d72205.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-2d060d615caf97be.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


给sucess.html中设置内容
```
@Controller
public class HelloController {

    @ResponseBody
    @RequestMapping("/hello")
    public String hello(){
        return "Hello World";
    }

    @RequestMapping("/success")
    public String success(Map<String,Object> map){
        // classpath:/templates/success.html
        map.put("hello","你好");
        return "success";
    }
}
```

```
<!DOCTYPE html>
<!--导入thymeleaf语法提示-->
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<h1>success!!!!!!!</h1>
<!--th:text 改变当前元素里面的文本内容-->
<!--th:任意html属性；来替换原生属性的值-->
<div th:text="${hello}"></div>
</body>
</html>
```

![](https://upload-images.jianshu.io/upload_images/2765653-c653feadc563ad21.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3、th的语法

```
th:insert 片段包含
th:replace 片段包含
th:each 遍历
th:if 判断
th:unless 条件判断
th:switch 条件判断
th:case 条件判断
th:object 声明变量
th:with 声明变量
th:attr 任意属性修改支持prepend，append
th:attrprepend 任意属性修改支持prepend，append
th:attrappend 任意属性修改支持prepend，append
th:value 修改指定属性默认值
th:href 修改指定属性默认值
th:src 修改指定属性默认值
th:text 修改标签体内容，转义特殊字符
th.utext 修改标签体内容，不转义特殊字符
th:fragment 声明片段
th:remove 声明片段
```

## 十三、springboot 2.0 + Redis

Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件

1、使用docker安装redis

```
docker pull redis // 拉取镜像

docker ps // 列出所有的容器

docker run -d -p 6379:6379 --name myredis redis:latest // 使用docker镜像redis:latest以后台模式启动一个容器,并将容器命名为myredis，容器的 6379 端口映射到主机的 6379 端口

docker rmi <Image-Id> // 使用rmi 删除容器时提示错误
Error response from daemon: conflict: unable to delete <Image-ID> (must be forced) - image is being used by stopped container xxxxxxxxxxx
// 可强制删除
docker rmi -f <image_id>  
```
2、pom.xml 注入redis依赖

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

3、测试Redis

```
@RunWith(SpringRunner.class)
@SpringBootTest
public class MySpringBootRedisApplicationTests {
    @Autowired
    EmployeeMapper employeeMapper;

    @Autowired
    StringRedisTemplate stringRedisTemplate;  //操作k-v都是字符串的

    @Autowired
    RedisTemplate redisTemplate;  //k-v都是对象的

    /**
     * Redis常见的五大数据类型
     *  String（字符串）、List（列表）、Set（集合）、Hash（散列）、ZSet（有序集合）
     *  stringRedisTemplate.opsForValue()[String（字符串）]
     *  stringRedisTemplate.opsForList()[List（列表）]
     *  stringRedisTemplate.opsForSet()[Set（集合）]
     *  stringRedisTemplate.opsForHash()[Hash（散列）]
     *  stringRedisTemplate.opsForZSet()[ZSet（有序集合）]
     */
    @Test
    public void test01(){
        //给redis中保存数据
        //stringRedisTemplate.opsForValue().append("msg","hello");
		String msg = stringRedisTemplate.opsForValue().get("msg"); // 保存字符串
		System.out.println(msg);

		stringRedisTemplate.opsForList().leftPush("mylist","1"); // 保存列表
		stringRedisTemplate.opsForList().leftPush("mylist","2");
    }
   //测试保存对象
    @Test
    public void test02(){
        Employee empById = employeeMapper.getEmpById(1);
        //如果保存对象，默认使用jdk序列化机制，序列化后的数据保存到redis中
        redisTemplate.opsForValue().set("emp-01",empById); // Employee bean实现Serializable
    }
}
```

4、RedisConfig

```
@Configuration
public class MyRedisConfig {
    // 改变默认的序列化规则
    @Bean
    public RedisTemplate<Object, Employee> empRedisTemplate(
            RedisConnectionFactory redisConnectionFactory)
            throws UnknownHostException {
        RedisTemplate<Object, Employee> template = new RedisTemplate<Object, Employee>();
        template.setConnectionFactory(redisConnectionFactory);
        Jackson2JsonRedisSerializer<Employee> ser = new Jackson2JsonRedisSerializer<Employee>(Employee.class); // Jackson2JsonRedisSerializer redis的序列化器
        template.setDefaultSerializer(ser); // 切换到redis序列化器
        return template;
    }
}
```

测试
```
@RunWith(SpringRunner.class)
@SpringBootTest
public class MySpringBootRedisApplicationTests {
    @Autowired
    EmployeeMapper employeeMapper;

    @Autowired
    RedisTemplate<Object, Employee> empRedisTemplate;

   //测试保存对象
    @Test
    public void test02(){
        Employee empById = employeeMapper.getEmpById(1);
        //1、将数据以json的方式保存
        //(1)自己将对象转为json
        //(2)redisTemplate默认的序列化规则；可以转为json
        empRedisTemplate.opsForValue().set("emp-01",empById);
    }
}
```

5、CacheManager

```
@Configuration
public class MyRedisConfig {
    @Bean
    public CacheManager cacheManager(RedisConnectionFactory factory) {
        //初始化一个RedisCacheWriter
        RedisCacheWriter redisCacheWriter = RedisCacheWriter.nonLockingRedisCacheWriter(factory);
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);

        //重写objectMapper
        MyObjectMapper objectMapper = new MyObjectMapper();
        objectMapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);

        //设置序列化器
        RedisSerializationContext.SerializationPair<Object> pair = RedisSerializationContext.SerializationPair.fromSerializer(jackson2JsonRedisSerializer);
        RedisCacheConfiguration defaultCacheConfig = RedisCacheConfiguration.defaultCacheConfig().serializeValuesWith(pair);
        return new RedisCacheManager(redisCacheWriter, defaultCacheConfig);
    }

    public class MyObjectMapper extends ObjectMapper {
        private static final long serialVersionUID = 1L;

        public MyObjectMapper() {
            super();
            // 去掉各种@JsonSerialize注解的解析
            this.configure(MapperFeature.USE_ANNOTATIONS, false);
            // 只针对非空的值进行序列化
            this.setSerializationInclusion(JsonInclude.Include.NON_NULL);
            // 对于找不到匹配属性的时候忽略报错
            this.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
            // 不包含任何属性的bean也不报错
            this.configure(SerializationFeature.FAIL_ON_EMPTY_BEANS, false);
        }
    }
}

```

```
public class Department  {
	
	private Integer id;
	private String departmentName;
	
	public Department() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Department(Integer id, String departmentName) {
		super();
		this.id = id;
		this.departmentName = departmentName;
	}
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getDepartmentName() {
		return departmentName;
	}
	public void setDepartmentName(String departmentName) {
		this.departmentName = departmentName;
	}
	@Override
	public String toString() {
		return "Department [id=" + id + ", departmentName=" + departmentName + "]";
	}
}
```

```
@Mapper
public interface DepartmentMapper {
    @Select("SELECT * FROM department WHERE id = #{id}")
    Department getDeptById(Integer id);
}
```

```
@RestController
public class DeptController {

    @Autowired
    DeptService deptService;

    @GetMapping("/dept/{id}")
    public Department getDept(@PathVariable("id") Integer id){
        return deptService.getDeptById(id);
    }
}
```

```
// 缓存：缓存中存在从缓存返回，缓存中没有查DB返回并更新缓存
// 使用缓存，方式一，使用注解
@Service
public class DeptService {
    @Autowired
    DepartmentMapper departmentMapper;
    // 使用缓存管理器得到缓存，进行api调用
    @Cacheable(cacheNames = {"dept"},key = "#id")
    public Department getDeptById(Integer id) {
        Department department = departmentMapper.getDeptById(id);
        return department;
    }
}

// 使用缓存，方式二，编码
@Service
public class DeptService {
    @Autowired
    DepartmentMapper departmentMapper;
    @Autowired
    CacheManager cacheManager;
    public Department getDeptById(Integer id) {
        //获取某个缓存
        Cache dept = cacheManager.getCache("dept");
        if (dept != null) {
            Department department1 = dept.get(id, Department.class);
            if (department1 != null) {
                return department1;
            }
        }
        Department department = departmentMapper.getDeptById(id);
        dept.put(id, department);
        return department;
    }
}
```

## 十四、springboot + 消息队列

消息服务中间件可以提升系统异步通信、扩展解耦能力。

举个例子：传统注册流程和使用消息队列比较

第一种：用户注册信息写入数据库后在按照顺序先后发送注册邮件和短信，走完这三步后用户才完成注册

![传统注册流程](https://upload-images.jianshu.io/upload_images/2765653-6b873176e68febfe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

第二种：用户注册消息写入数据后通过开启线程池的方式，同时发送邮件和注册短信，两个线程完成后返回，用户注册完成

![采用多线程方式](https://upload-images.jianshu.io/upload_images/2765653-44595675b7b462de.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

第三步：用户注册消息写入数据后将消息写入到消息队列，此时发送邮件和发送短信通过异步读取消息队列执行具体的操作，但在写入消息队列之前已经返回给用户，用户注册完成，而发送短信和邮件是异步操作

![消息队列](https://upload-images.jianshu.io/upload_images/2765653-139cabe10b432502.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

应用解耦

传统方式下单后调用库存系统更新商品的剩余库存。采用消息队列方式，可达到应用解耦，下单后订单系统调用mq将消息写入到消息队列，由库存系统订阅消息队列并按照业务逻辑处理对应消息

![传统方式](https://upload-images.jianshu.io/upload_images/2765653-22b87ba5c1aa9615.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![采用消息队列方式](https://upload-images.jianshu.io/upload_images/2765653-88f873a102018d4f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


流量削峰

比如我们有100W用户同时抢100台手机，服务层并发请求压力至少为100W。

既然服务层知道库存只有100台手机，那完全没有必要把100W个请求都传递到数据库啊，那么可以先把这些请求都写到消息队列缓存一下，数据库层订阅消息减库存，减库存成功的请求返回秒杀成功，失败的返回秒杀结束。

![](https://upload-images.jianshu.io/upload_images/2765653-31bc636c311a2552.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


当消息发送者发送消息以后，将由消息代理接管，消息代理保证消息传递到指定目的地。

消息队列主要有两种形式的目的地：

- 队列（queue）：点对点消息通信

消息发送者发送消息，消息代理将其放入一个队列中，消息接收者从队列中获取消息内容，消息读取后被移除队列，此时消息只有唯一的发送者和接收者，但并不是只能有一个接收者，这种情况下可以存在多个接收者，但一个接收者接收后，其他的就不再处理

- 主题（topic）：发布（public）/订阅（subscribe）消息通信

订阅式：发送者（发布者）发送消息到主题，多个接收者（订阅者）监听（订阅）这个主题，那么就会在消息到达时同时收到消息

再说下JMS和AMOP，JAMS（Java Messge Service） JAVA消息服务是给予JVM消息代理的规范。ActiveMQ、HornetMQ是JMS实现；
AMQP是高级消息队列协议，也是一个消息代理的规范，兼容JMS，RabbitMQ是AMQP的实现，AMQP提供了五种消息模型：direct exchage、fanout exchange、topic change、headers exchange、system exchange；

#### RabbitMQ


- Message
消息，消息是不具名的，它由消息头和消息体组成。消息题是不透明的，而消息头则由一系列的可选属性组成，这些属性包括routing-key（路由键）、priority（相对于其他消息的优先权）、delivery-mode（指出该消息可能需要持久性存储）等

- Publisher
消息的生产者，也是一个向交换器发布消息的客户端应用程序

- Exchange
交换器，用来接收生产者发送的消息并将这些消息路由给服务器中的队列
Exchange有4中类型：direct（默认）、fanout、topic和headers，不同类型的Exchange转发消息的策略有所区别，direct指的是点对点，fanout、topic和headers指的是订阅

- Queue
消息队列，用来保存消息直到发送给消费者，它是消息的容器，也是消息的终点。一个消息可投入一个或多个队列。消息一直在队列里面，等待消费者连接到这个队列将其取走

- Binding
绑定，用于消息队列和交换器之间的关联。一个关联就是基于路由键将交换器和消息队列连接起来的路由规则，所以可以将交换器理解成一个由绑定构成的路由表。Exchange和Queue的绑定可以是多对多的关系

- Connection
网络连接，比如一个TCP连接

- Channel
信道，多路复用连接中的一条独立的双向数据流通道。信道是建立在真实的TCP连接内的虚拟连接，AMQP命令都是通过信道发出去的，不管是发布消息、订阅队列还是接收消息，这些动作都是信道完成。因为对于操作系统来说建立和销毁TCP都是非常昂贵的开销，所以引入了信道的概念，以复用一条TCP连接

- Consumer
消息的消费者，表示一个从消息队列中取得消息的客户端应用程序

- Virtual Host
虚拟主机，表示一批交换器、消息队列和相关对象。虚拟主机是共享相同的身份认证和加密环境的独立服务器域。每个vhost本质上就是一个mini版的RabbitMQ服务器，拥有自己的队列、交换器、绑定和权限机制。vhost是AMOP概念的基础，必须在连接时指定，RabbitMQ默认的vhost是/

- Broker
表示消息队列服务器实体

![](https://upload-images.jianshu.io/upload_images/2765653-5185b52910306d9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

RabbitMQ 运行机制

- Exchange

AMQP中消息的路由过程和Java开发者熟悉的JMS存在一些差别，AMQP中增加了Exchange和Binding的角色。生产者把消息发布到Exchange上，消息最终到达队列并被消费者接收，而Binding决定交换器的消息应该发送到哪个队列上。

![](https://upload-images.jianshu.io/upload_images/2765653-47a135ed46e30333.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-  Exchange

Exchange分发消息时类型不同分发策略不同，目前有四种类型：direct、fanout、topic、headers。headers匹配AMQP消息的header而不是路由键，headers交换器和direct交换器完全一致，但性能相差很多，目前几乎用不到了，所以直接看另外三种类型：

- Direct

![Direct Exchange](https://upload-images.jianshu.io/upload_images/2765653-9591bc418fe83edd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

消息中的路由键如果和Binding中的binding key一致，交换器就将消息发到对应的队列中。路由键与队列名完全匹配，如果一个队列绑定到交换机要求路由键为 “dog”，则交换器只转发“dog”的消息到此消息队列。不会转发“dog.puppy”,也不会转发“dog.guard”等等。direct是完全匹配、单播的模式。

- Fanout

![Fanout Exchange](https://upload-images.jianshu.io/upload_images/2765653-13363fd86236639e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

每个发到Fanout类型交换器的消息都会分到所有绑定的队列上去。fanout交换器不处理路由键，只是简单的将队列交换器上，每个发送到交换器的消息都会被转发到与该交换器绑定的所有队列上。很像子网广播，每个子网内的主机都获得了一份复制的消息。fanout类型转发消息是最快的

- topic

![Topic Exchange](https://upload-images.jianshu.io/upload_images/2765653-f681086a9c560ba6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

topic交换器通过模式匹配分配消息的路由键属性，将路由键和某个模式进行匹配，此时队列需要绑定到一个模式上。它将路由键和绑定键的字符串切分为单词，这些单词之间用点个靠。它同样也会识别两个匹配符：符号# 和 符号* *，#匹配0个或多个单词，*匹配一个单词


1、docker 安装 RabbitMQ

```
$ docker ps // docker查看运行的容器
$ docker pull rabbitmq:management // 拉取镜像,加上management，表明是带web管理界面的，便于管理
Using default tag: latest
latest: Pulling from library/rabbitmq
423ae2b273f4: Pull complete 
de83a2304fa1: Pull complete 
f9a83bce3af0: Pull complete 
b6b53be908de: Pull complete 
834aeb8bfce6: Pull complete 
3407dc115970: Pull complete 
a003ac596878: Pull complete 
5664c847e128: Pull complete 
d392687f8224: Pull complete 
8b6336946e55: Pull complete 
Digest: sha256:fb0023bda1d2237418417557b212ca027180dcdf6da883891c08b78591cc8c15
Status: Downloaded newer image for rabbitmq:latest
docker.io/library/rabbitmq:latest

$ docker images // 查看当前镜像
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
rabbitmq            latest              4c8cb17c3ab5        31 hours ago        151MB

$ docker run -d -p 5672:5672 -p 15672:15672 --name myrabbitmq 4c8cb17c3ab5 // 运行镜像 ,默认的端口为：5672，web管理的端口为:15672，
328854acf29841bb7bd1dee54b6d0c4c4b5077284e301fe97bcdbdd0494ddf17
```

[浏览器直接访问服务器地址](http://localhost:15672) ，默认用户和密码为：guest

![](https://upload-images.jianshu.io/upload_images/2765653-fec881c6f1d3f1fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/2765653-75cb5e7c671041a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2、添加交换器

![添加交换器的步骤，选择Durable持久化的原因是，关闭服务器后交换器还在](https://upload-images.jianshu.io/upload_images/2765653-f542a0de120b9cf3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

分别添加direct、fanout、topic

![添加direct](https://upload-images.jianshu.io/upload_images/2765653-4dc1f10b8f93eb0b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![添加fanout](https://upload-images.jianshu.io/upload_images/2765653-7493ef4b15e26550.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![添加 topic](https://upload-images.jianshu.io/upload_images/2765653-01ef22bce23e53a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![添加的交换器在列表展示](https://upload-images.jianshu.io/upload_images/2765653-db0c450a09bde6ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3、添加消息队列 

![添加消息队列的步骤](https://upload-images.jianshu.io/upload_images/2765653-14933c52c284bf7c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![添加的消息队列在列表展示](https://upload-images.jianshu.io/upload_images/2765653-c954410326974efd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


4、交换器绑定Binding

![](https://upload-images.jianshu.io/upload_images/2765653-cd518f6c0a1277f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-966a494c9e2ce538.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![direct交换器 绑定消息队列](https://upload-images.jianshu.io/upload_images/2765653-d3de912803cf1187.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![fonout交换器 绑定消息队列](https://upload-images.jianshu.io/upload_images/2765653-0da5f3a56b2bf0a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![topic交换器 绑定消息队列](https://upload-images.jianshu.io/upload_images/2765653-e4e4b18dc54c090d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


5、发送消息到交换器

发送到direct交换器，根据绑定时路由键（Routing key）发送到消息队列

![](https://upload-images.jianshu.io/upload_images/2765653-b9534876d9e20d67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![发送消息的步骤](https://upload-images.jianshu.io/upload_images/2765653-0173d0f0cbeba65a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-b2e776a0540b7f29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![查看发送消息结果](https://upload-images.jianshu.io/upload_images/2765653-667cbfb72697ec80.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

消息队列中get message

![](https://upload-images.jianshu.io/upload_images/2765653-eecb7e28debb72ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-7df01683040702d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

发送到fonout交换器，fonout绑定了所有队列 不管什么路由键是什么都可以接收消息

![](https://upload-images.jianshu.io/upload_images/2765653-d9dd2edb2e405a7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![查看发送消息结果，四个队列都接收到了这条消息](https://upload-images.jianshu.io/upload_images/2765653-9d6aa1c23ed1501f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![任意查看一个队列](https://upload-images.jianshu.io/upload_images/2765653-4b9b18a25747a28d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


发送到topic交换器，按照路由规则接收消息

![](https://upload-images.jianshu.io/upload_images/2765653-457bb879c5aadc49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![4个消息队列都收到了](https://upload-images.jianshu.io/upload_images/2765653-d37872dd465a6ff1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![继续发送一个其他的消息测试](https://upload-images.jianshu.io/upload_images/2765653-d1ae06136b9cd4fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![这次只有两个收到了](https://upload-images.jianshu.io/upload_images/2765653-d43bb25e0ea1182c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### springboot 整合消息队列

使用idea 创建过程，可参考前几篇中的内容

![选择注入依赖的时候，选择web和rabbitmq](https://upload-images.jianshu.io/upload_images/2765653-747e9c14afccfdb3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
# application.properties
# 不写默认是localhost
spring.rabbitmq.host=127.0.0.1
spring.rabbitmq.username=guest
spring.rabbitmq.password=guest
spring.rabbitmq.port=5672
```

RabbitAutoConfiguration自动配置类提供了连接工厂ConnectionFactory，可以获得rabbitmq的连接，通过RabbitProperties获得user和password，给RabbitMQ发送和接收消息

发送点对点消息

```
@SpringBootTest
class SpringbootRabbitmqApplicationTests {

    @Autowired
    RabbitTemplate rabblitTemplete;

    /**
     * 单播（点对点）
     */
    @Test
    void contextLoads() {
//        rabblitTemplete.send(exchange,routeKey,message); // Message需要自己构造一个；自己构造的时候定义消息体内容和消息头。

//        rabblitTemplete.convertAndSend(exchange,routeKey,object); // object默认当成消息体，只需要传递要发送的对象，会自动序列化发送给rabbitmq
        Map<String,Object> map = new HashMap<>();
        map.put("msg","这是第一个消息");
        map.put("data", Arrays.asList("helloworld",123,true)); // 对象被默认序列化以后发送出去
//        rabblitTemplete.convertAndSend("exchange.direct","sangyu.news",map);
        rabblitTemplete.convertAndSend("exchange.direct","sangyu.news",new Book("AA","BB")); // 发送包含对象的信息

    }
```

接收消息

```
@SpringBootTest
class SpringbootRabbitmqApplicationTests {

    @Autowired
    RabbitTemplate rabblitTemplete;
    /**
     * 接收数据
     */
    @Test
    public void receive(){
        Object o = rabblitTemplete.receiveAndConvert("sangyu.news");
        System.out.println(o.getClass());
        System.out.println(o);
    }
 }
```

将数据自动地转为json发送出去，通过MessageConverter

```
@Configuration
public class MyAMQConfig {
    @Bean
    public MessageConverter messageConverter(){
        return new Jackson2JsonMessageConverter();
    }
}
```

发送广播消息

```
@SpringBootTest
class SpringbootRabbitmqApplicationTests {
    /**
     * 广播 fanout
     */
    @Test
    public void sendMsg(){
        rabblitTemplete.convertAndSend("exchange.fanout","",new Book("EE","FF"));
    }
}
```

通过AmqpAdmin ：创建和删除Queue、Exchange、Binging

```
@SpringBootTest
class SpringbootRabbitmqApplicationTests {
    @Autowired
    AmqpAdmin amqpAdmin;

    @Test
    public void createExchange(){
//        amqpAdmin.declareExchange(new DirectExchange("amqpadmin.exchange"));
//        System.out.println("ok");
        amqpAdmin.declareQueue(new Queue("amqpadmin.queue",true));
        amqpAdmin.declareBinding(new Binding("amqpadmin.queue", Binding.DestinationType.QUEUE,"amqpadmin.exchange","amqpadmin.haha",null));
    }
}
```

@EnableRabbit + @RabbitListener 监听消息队列的内容

```
@Service
public class BookService {
    @RabbitListener(queues = "sangyu.news") // 可以监听多个消息队列，只要这个消息队列有消息，receive这个方法就会被调用
    public void receive(Book book){ //通过监听mq来调用的
        System.out.println("收到消息： " + book);
    }
    @RabbitListener(queues = "sangyu")
    public void receive02(Message message){
        System.out.println(message.getBody()); // 获得消息的内容
        System.out.println(message.getMessageProperties()); // 获得消息体
    }
}
```

```
@EnableRabbit //开启基于注解的RabblitMQ注解
@SpringBootApplication
public class SpringbootRabbitmqApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringbootRabbitmqApplication.class, args);
    }
}
```

## 十五、springboot 整合 ElasticSearch

ElasticSearch是目前全文搜索引擎的首选，可以快速的存储、搜索和分析数据，并且ES是一个分布式搜索服务，提供Restful API，底层基于Lucene，采用多shard（分片）的方式保证数据安全，并且提供自动resharding的功能，github等大型的站点也是采用了ES作为其搜索服务

#### docker安装ES

```
$ docker pull elasticsearch // 拉取镜像
Using default tag: latest
latest: Pulling from library/elasticsearch
[DEPRECATION NOTICE] registry v2 schema1 support will be removed in an upcoming release. Please contact admins of the docker.io registry NOW to avoid future disruption.
05d1a5232b46: Pull complete 
5cee356eda6b: Pull complete 
89d3385f0fd3: Pull complete 
65dd87f6620b: Pull complete 
78a183a01190: Pull complete 
1a4499c85f97: Pull complete 
2c9d39b4bfc1: Pull complete 
1b1cec2222c9: Pull complete 
59ff4ce9df68: Pull complete 
1976bc3ee432: Pull complete 
5af49e8af381: Pull complete 
42c8b75ff7af: Pull complete 
7e6902915254: Pull complete 
99853874fa54: Pull complete 
596fbad6fcff: Pull complete 
Digest: sha256:6133081706cedbb5f486a510482c285d8cd54820411bd916d965c7a9b1969d24
Status: Downloaded newer image for elasticsearch:latest
docker.io/library/elasticsearch:latest
```
```
$ docker images // 安装的镜像
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
elasticsearch       latest              5acf0e8da90b        17 months ago       486MB
```
```
$ docker run -e ES_JAVA_OPTS="-Xms256m -Xmx256m" -d -p 9200:9200 -p 9300:9300 --name ES01 5acf0e8da90b // 初始化容器
8ed13535108a1bd611f0ce53aea3548494d9956f777c526ea10aaf95ec404683
```

```
$ docker ps  // 正常运行的容器
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                                                                                                      NAMES
8ed13535108a        5acf0e8da90b          "/docker-entrypoint.…"   33 seconds ago      Up 29 seconds       0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp                                                                             ES01
```

验证ES安装成功，[访问此url](http://localhost:9200/)

![](https://upload-images.jianshu.io/upload_images/2765653-7479295546e9d570.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### ES基础入门

ES使用JavaScript Object Notation 或者JSON作为文档的序列化格式。JSON序列化被大多数变成语言所支持，并且已经成为NoSQL领域的标准格式。

以下使用JSON文档来表示一个用户对象：

```
{
    "email": "john@smith.com",
    "first_name": "John",
    "last_name": "Smith",
    "info": {
        "bio": "Eco-warrior and defender of the weak",
        "age": 25,
        "interests": [ "dolphins", "whales" ]
    },
    "join_date": "2014/05/01"
}
```

ES集群可以包含多个索引(indices)（数据库），每一个索引可以包含多个类型(types)（表），每一个类型包含多个文档(documents)（行），然后每个文档包含多个字段(Fields)（列）

通过对比图来类比传统关系型数据库：

```
Relational DB -> Databases -> Tables -> Rows -> Columns
Elasticsearch -> Indices   -> Types  -> Documents -> Fields
```

假使现在Animal公司，需要创建一个员工目录，为此我们将进行如下操作

1. 为每个员工的文档(document)建立索引，每个文档包含了相应员工的所有信息。
2. 每个文档的类型为employee。
3. employee类型归属于索引megacorp。
4. megacorp索引存储在Elasticsearch集群中。

而上述这些步骤，通过一条命令就能完成所有这些动作：

```
PUT /animal/employee/1
{
    "first_name" : "John",
    "last_name" : "Smith",
    "age" : 25,
    "about" : "I love to go rock climbing",
    "interests" : ["sports","music"]
}
```

实际操作，借助Postman

![添加员工1](https://upload-images.jianshu.io/upload_images/2765653-a531722138c244ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![返回结果](https://upload-images.jianshu.io/upload_images/2765653-a19858e5b0389d49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![继续按照相同的步骤添加员工2](https://upload-images.jianshu.io/upload_images/2765653-576f171788cdeb4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![继续按照相同的步骤添加员工3](https://upload-images.jianshu.io/upload_images/2765653-a9c2a2d0cf7bfa00.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

检索文档，通过执行一个HTTP GET请求并指定文档的地址--索引库、类型和ID。使用这三个信息可以返回原始的JSON文档

``` 
GET /animal/employee/1
```

![GET](https://upload-images.jianshu.io/upload_images/2765653-cb80d3541782add2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![HEAD](https://upload-images.jianshu.io/upload_images/2765653-8340ded58a01fe50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![DELETE](https://upload-images.jianshu.io/upload_images/2765653-af71717ef1298b56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



我们尝试一个最简单的搜索全部员工的请求：

```
GET /megacorp/employee/_search
```

![展示了刚刚添加的3个员工，默认情况下搜索会返回前10个结果](https://upload-images.jianshu.io/upload_images/2765653-a3e1bac68cc35da6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

搜索姓氏中包含“Smith”的员工，使用轻量级的搜索方法。这种方法常被称作查询字符串(query string)搜索

```
GET /megacorp/employee/_search?q=last_name:Smith
```

![查询结果](https://upload-images.jianshu.io/upload_images/2765653-6049f9ac5bc0566b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用DSL语句查询，DSL(Domain Specific Language特定领域语言)以JSON请求体的形式出现。我们可以这样表示之前关于“Smith”的查询:

```
GET /megacorp/employee/_search
{
    "query" : {
        "match" : {
            "last_name" : "Smith"
        }
    }
}
```
比刚才更复杂的搜索，要查找姓氏为“Smith”的员工并且年龄大于30岁的员工。此时需要使用过滤器(filter)

```
GET /megacorp/employee/_search
{
    "query" : {
        "filtered" : {
            "filter" : {
                "range" : {
                    "age" : { "gt" : 30 } <1> // <1> 这部分查询属于区间过滤器(range filter),它用于查找所有年龄大于30岁的数据
                }
            },
            "query" : {
                "match" : {
                    "last_name" : "smith" <2> // <2> 这部分查询与之前的match语句(query)一致
                }
            }
        }
    }
}
```

全文搜索

```
// 所有喜欢“rock climbing”的员工
GET /megacorp/employee/_search
{
    "query" : {
        "match" : {
            "about" : "rock climbing"
        }
    }
}
// <1><2> 结果相关性评分。
默认情况下，ES根据结果相关性评分来对结果集进行排序，所谓的「结果相关性评分」就是文档与查询条件的匹配程度。很显然，排名第一的John Smith的about字段明确的写到“rock climbing”。
但是为什么Jane Smith也会出现在结果里呢？原因是“rock”在她的abuot字段中被提及了。因为只有“rock”被提及而“climbing”没有，所以她的_score要低于John。
这个例子很好的解释了Elasticsearch如何在各种文本字段中进行全文搜索，并且返回相关性最大的结果集。相关性(relevance)的概念在Elasticsearch中非常重要，而这个概念在传统关系型数据库中是不可想象的，因为传统数据库对记录的查询只有匹配或者不匹配。
```

短语搜索

目前我们可以在字段中搜索单独的一个词，这挺好的，但是有时候你想要确切的匹配若干个单词或者短语(phrases)。例如我们想要查询同时包含"rock"和"climbing"（并且是相邻的）的员工记录。

```
GET /megacorp/employee/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "rock climbing"
        }
    }
}
```

高亮我们的搜索

很多应用喜欢从每个搜索结果中高亮(highlight)匹配到的关键字，这样用户可以知道为什么这些文档和查询相匹配。在Elasticsearch中高亮片段是非常容易的。

```
GET /megacorp/employee/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "rock climbing"
        }
    },
    "highlight": {
        "fields" : {
            "about" : {}
        }
    }
}
```

#### SpringBoot 整合ES

通过向导快速创建SpringBoot，其他步骤可参考之前的文章
![](https://upload-images.jianshu.io/upload_images/2765653-d30b076ae636ef57.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

springboot默认支持两种技术来和ES交互

1. JEST（默认不生效）

```
// pom.xml注入依赖
<dependency>
    <groupId>io.searchbox</groupId>
    <artifactId>jest</artifactId>
    <version>5.3.3</version>
</dependency>
```

```
//application.properties
spring.elasticsearch.rest.uris=http://127.0.0.1:9200
```
```
public class Article {
    @JestId
    private Integer id;
    private String author;
    private String title;
    private String content;
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getAuthor() {
        return author;
    }
    public void setAuthor(String author) {
        this.author = author;
    }
    public String getContent() {
        return content;
    }
    public void setContent(String content) {
        this.content = content;
    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
    @Override
    public String toString() {
        return "Article{" +
                "id=" + id +
                ", author='" + author + '\'' +
                ", title='" + title + '\'' +
                ", content='" + content + '\'' +
                '}';
    }
}
```

```
@SpringBootTest
class MySpringBootEsApplicationTests {

    @Autowired
    JestClient jestClient;

    @Test
    void contextLoads() {
        // 给ES中索引保存一个文档
        Article article = new Article();
        article.setId(1);
        article.setTitle("AA");
        article.setTitle("11");
        article.setContent("good");

        // 构建一个所以对象
        Index index = new Index.Builder(article).index("sangyu").type("news").build();

        try{
            // 执行
            jestClient.execute(index);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // 测试搜索
    @Test
    public void search(){
        // 查询搜索
        String json = "{\n" +
                "    \"query\" : {\n" +
                "        \"match\" : {\n" +
                "            \"content\" : \"good\"\n" +
                "        }\n" +
                "    }\n" +
                "}";

        // 构建搜索功能
        Search search = new Search.Builder(json).addIndex("sangyu").addType("news").build();

        // 执行
        try{
            SearchResult result = jestClient.execute(search);
            System.out.println(result.getJsonString());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

2. 使用springboot 整合elasticsearch

环境

SpringBoot: 2.2.4.RELEASE
Elasticsearch: 6.7.2
JDK: 1.8

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:6.7.2
```

```
$ docker run -e ES_JAVA_OPTS="-Xms256m -Xmx256m" -d -p 9202:9200 -p 9302:9300 -e "discovery.type=single-node" --name ES03 2982ba071059 
9a0f07c705abf00f7faaefbbd4478aeb8fc49f0c40346ca8e2f028ca39d82a34
```

```
// 为了版本统一，修改pom.xml一览
<dependencies>
        <dependency>
            <groupId>org.elasticsearch</groupId>
            <artifactId>elasticsearch</artifactId>
            <version>6.7.2</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-elasticsearch</artifactId>
            <version>3.2.0.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.elasticsearch.client</groupId>
            <artifactId>elasticsearch-rest-high-level-client</artifactId>
            <version>6.7.2</version>
        </dependency>
        <dependency>
            <groupId>io.searchbox</groupId>
            <artifactId>jest</artifactId>
            <version>5.3.3</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.elasticsearch.client</groupId>
            <artifactId>x-pack-transport</artifactId>
            <version>6.7.2</version>
        </dependency>
    </dependencies>
```

```
// application.properties
elastic.host=127.0.0.1
elastic.port=9202
```

```
public class Article {
    @JestId
    private Integer id;
    private String author;
    private String title;
    private String content;
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getAuthor() {
        return author;
    }
    public void setAuthor(String author) {
        this.author = author;
    }
    public String getContent() {
        return content;
    }
    public void setContent(String content) {
        this.content = content;
    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
    @Override
    public String toString() {
        return "Article{" +
                "id=" + id +
                ", author='" + author + '\'' +
                ", title='" + title + '\'' +
                ", content='" + content + '\'' +
                '}';
    }
}
```

```
@Configuration
public class EsConf {

    @Value("${elastic.host}")
    private String host;

    @Value("${elastic.port}")
    private int port;


    @Bean
    public RestHighLevelClient elasticsearchClient() {
        RestClientBuilder builder = RestClient.builder(new HttpHost(host, port));
        return new RestHighLevelClient(builder);
    }

    @Bean
    public ElasticsearchRestTemplate elasticsearchTemplate() {
        return new ElasticsearchRestTemplate(elasticsearchClient());
    }
```

```
public interface StudentRepository extends ElasticsearchRepository<Student, Long> {
    List<Student> findByName(String name);
}
```
```
@SpringBootTest
class MySpringBootEsApplicationTests {
    @Autowired
    private StudentRepository studentRepository;
    Student stu = new Student();
    @Test
    public void save() {
        stu.setId(4L);
        stu.setName("Bob");
        stu.setHobby("biu biu biu~~");
        stu.setBirthday(new Date());
        studentRepository.save(stu);
    }

    @Test
    public void findById() {
        Student stu = studentRepository.findById(3L).orElse(null);
        System.out.println(stu);
    }

    @Test
    public void findByName() {
        List<Student> bob = studentRepository.findByName("Bob");
        bob.forEach(System.out::println);
    }

    @Test
    public void delete() {
        studentRepository.deleteById(3L);
    }
}
```

## 十六、springboot-任务

使用向导快速创建springboot，其他步骤可参考之前的文章

![](https://upload-images.jianshu.io/upload_images/2765653-8a20c6b3d11d4a75.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


异步任务 @EnableAsync,  @Async
 
```
@RestController
public class AsyncController {
    @Autowired
    AsyncService asyncService;
    @GetMapping("/hello")
    public String hello(){
        asyncService.hello();
        return "success";
    }
}
```

```
@EnableAsync // 开启异步注解 功能
@SpringBootApplication
public class MySpringBootTaskApplication {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootTaskApplication.class, args);
    }
}
```

```
@Service
public class AsyncService {
    /**
     * @Async 告诉spring这是一个异步方法 spring会开启一个线程池
     */
    @Async
    public void hello(){
        try{
            Thread.sleep(3000);
            System.out.println("end...");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("处理数据中...");
    }
}
```

定时任务 @EnableScheduling, @Scheduled

```
@Service
public class ScheduleService {
    /**
     * second,minute,hour,day of month（日）,month,day of week（周几）
     * 0 0/5 14 18 * ？每天14点，和18点，每隔5分钟执行一次
     * 0 15 10 ？ * 1-6 每隔月的周一到周六凌晨10：15分执行一次
     * 0 0 2 ？ * 6L 每个月最后一个周六凌晨2点执行一次
     * 0 0 2 LW * ？每个月的最后一个工作日凌晨2点执行一次
     * 0 0 2 2-4 ？ * 1#1 每个月的第一个周一凌晨2点到4点期间，每个整点都执行一次
     * 
     */
    @Scheduled(cron = "0/4 * * * * MON-SAT") //周一到周日 每4秒执行一次
    public void hello(){
        System.out.println("hello");
    }
}
```

```
@EnableScheduling // 开启基于注解的定时任务
@EnableAsync // 开启异步注解 功能
@SpringBootApplication
public class MySpringBootTaskApplication {

    public static void main(String[] args) {
        SpringApplication.run(MySpringBootTaskApplication.class, args);
    }
}
```

```
@RestController
public class AsyncController {
    @Autowired
    ScheduleService scheduleService;
    @GetMapping("/hello")
    public String hello(){
        scheduleService.hello();
        return "success";
    }
}
```

邮件任务

```
// pom.xml 注入依赖
<dependency>
    <groupId>com.sun.mail</groupId>
    <artifactId>javax.mail</artifactId>
    <version>1.6.1</version>
</dependency>
```

开启邮箱的POP3/SMTP服务 ([如何使用 Foxmail 等软件收发邮件？](http://service.mail.qq.com/cgi-bin/help?subtype=1&&id=28&&no=371))

![image.png](https://upload-images.jianshu.io/upload_images/2765653-0f7861b72e5085d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-03fd4b29df94b6d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
// application.properties
spring.mail.host=smtp.qq.com
spring.mail.username=935789914@qq.com
spring.mail.password=jmorsvzgrvfvbecb
spring.mail.properties.mail.smtp.ssl.enable=true
```

```
@SpringBootTest
class MySpringBootTaskApplicationTests {

    @Autowired
    JavaMailSenderImpl mailSender;

    @Test
    void contextLoads() {
        SimpleMailMessage message = new SimpleMailMessage();

        message.setSubject("通知");
        message.setText("今天是个特别的日子");

        message.setTo("935789914@qq.com");
        message.setFrom("935789914@qq.com");

        mailSender.send(message);
    }

    @Test
    void test02() throws MessagingException {
        //1. 创建一个复杂的消息邮件
        MimeMessage mimeMessage = mailSender.createMimeMessage();
        MimeMessageHelper helper = new MimeMessageHelper(mimeMessage,true);

        //2. 邮件设置
        helper.setSubject("通知");
        helper.setText("<p style=\"color:red;\">今天 7:30 开会</p>",true);

        helper.setTo("935789914@qq.com");
        helper.setFrom("935789914@qq.com");

        helper.addAttachment("sunset-above-mount-st-michael.jpg",new File("/Users/pengyapan/Downloads/PICTURE/sunset-above-mount-st-michael.jpg"));

        mailSender.send(mimeMessage);
    }

    @Test
    void test03(){
        System.out.println("\"color:red\"");
    }
}
```























