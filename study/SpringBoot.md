## SpringBoot 项目创建

SpringBoot - HelloWorld

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

使用向导快速创建SpringBoot项目

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


## YAML

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






















