## 目录

[一、idea创建SpringMVC项目](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E4%B8%80idea%E5%88%9B%E5%BB%BAspringmvc%E9%A1%B9%E7%9B%AE)

[二、SpringMVC-HelloWorld](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E4%BA%8Cspringmvc-helloworld)

[三、@RequestMapping 注解](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E4%B8%89requestmapping-%E6%B3%A8%E8%A7%A3)

[四、@RequestParam 注解](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%9B%9Brequestparam-%E6%B3%A8%E8%A7%A3)

[五、@RequestHeader 注解](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E4%BA%94requestheader-%E6%B3%A8%E8%A7%A3)

[六、@CookieValue 注解](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%85%ADcookievalue-%E6%B3%A8%E8%A7%A3)

[七、使用POJO对象绑定请求参数值](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E4%B8%83%E4%BD%BF%E7%94%A8pojo%E5%AF%B9%E8%B1%A1%E7%BB%91%E5%AE%9A%E8%AF%B7%E6%B1%82%E5%8F%82%E6%95%B0%E5%80%BC)

[八、ModelAndView](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%85%ABmodelandview)

[九、 Map&Model](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E4%B9%9D-mapmodel)

[十、@SessionAttributes 注解](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%8D%81sessionattributes-%E6%B3%A8%E8%A7%A3)

[十一、@ModelAttribute 注解](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%8D%81%E4%B8%80modelattribute-%E6%B3%A8%E8%A7%A3)

[十二、使用servlet原生API作为参数](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%8D%81%E4%BA%8C%E4%BD%BF%E7%94%A8servlet%E5%8E%9F%E7%94%9Fapi%E4%BD%9C%E4%B8%BA%E5%8F%82%E6%95%B0)

[十三、SpringMVC自定义视图](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%8D%81%E4%B8%89springmvc%E8%87%AA%E5%AE%9A%E4%B9%89%E8%A7%86%E5%9B%BE)

[十四、Springmvc 重定向](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%8D%81%E5%9B%9Bspringmvc-%E9%87%8D%E5%AE%9A%E5%90%91)

[十五、SpringMVC-处理静态资源](https://github.com/xingyuexingyue/sangyu/blob/master/study/SpringMVC.md#%E5%8D%81%E4%BA%94springmvc-%E5%A4%84%E7%90%86%E9%9D%99%E6%80%81%E8%B5%84%E6%BA%90)

## 一、idea创建SpringMVC项目

1. Create New Project 单击进入下一步
![](https://upload-images.jianshu.io/upload_images/2765653-9a373cd2ea85583d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 左侧选择Maven，勾选Create from archetype，选择3，next
![](https://upload-images.jianshu.io/upload_images/2765653-31c9202f6dc01f97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. GroupId 和 ArtifactId 填写后next

![](https://upload-images.jianshu.io/upload_images/2765653-49fabb03ea5b8bdc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. Local repository maven项目的本地仓库默认是在.m2文件夹下。settings.xml 文件里面会所直至的本地仓库的地址和这个地址是一样的
User setting file我这里用的是.m2/settings.xml
这里没有问题后Finish
![](https://upload-images.jianshu.io/upload_images/2765653-9d10a46a7812ed0d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.  可以选择 Enable Auto-import 自动导入，这样每次maven添加新的依赖后都会自动导入jar包
![](https://upload-images.jianshu.io/upload_images/2765653-d6cfa4b001c5e1c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6. 打开pom.xml文件 添加依赖，(这里要注意的版本一致的问题,添加的spring相关的依赖，要保持版本的一致)，在<dependencies>  </dependencies>下

```
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
    <!--日志-->
    <dependency>
      <groupId>commons-logging</groupId>
      <artifactId>commons-logging</artifactId>
      <version>1.1.1</version>
    </dependency>
   
    <!--J2EE-->
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.2</version>
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
    </dependency>
    <!--mysql驱动包-->
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>5.1.35</version>
    </dependency>
    <!--springframework-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
<dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-test</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context-support</artifactId>
      <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>com.github.stefanbirkner</groupId>
      <artifactId>system-rules</artifactId>
      <version>1.16.1</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.8.9</version>
    </dependency>
    <!--其他需要的包-->
    <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-lang3</artifactId>
      <version>3.4</version>
    </dependency>
    <dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <version>1.3.1</version>
    </dependency>
  </dependencies>
```
7. 添加springMVC框架，右击项目文件夹springmvc-test07，选择Add framework support

![](https://upload-images.jianshu.io/upload_images/2765653-1d231424dc56b7b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

将下图中的Spring和Spring下的Spring MVC都勾上，之前配置pom.xml文件时，已经自动下载了spring相关文件，所以这里就直接用之前下载好的就可以了，OK。（注意：点了Add framework support之后，在下图中有可能会找不到Spring，解决办法在下图的下方）

![](https://upload-images.jianshu.io/upload_images/2765653-aedc1a1dca7936d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果在Add framework support中找不到Spring，那是因为项目中可能已经存在Spring相关文件，但不一定是完善的。因此我们要将已经存在的Spring给删掉，重新添加，方法如下：

点击File，选择Project Structure，选择Facets，就会看到有一个Spring啦，右击它，点删除就行啦，然后再回到上面第3步重新Add framework support，Spring就会出现啦。


![1](https://upload-images.jianshu.io/upload_images/2765653-06bd0b906be2bec3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![2](https://upload-images.jianshu.io/upload_images/2765653-faab64f392864c71.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加Spring框架后，目录下多了两个xml文件
![](https://upload-images.jianshu.io/upload_images/2765653-d152e6ff5a90e79a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

8.完善目录结构：src/main文件夹下创建java、resources文件夹；src文件夹下创建test文件夹

![](https://upload-images.jianshu.io/upload_images/2765653-c720a12cb8b089f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

创建好之后，File-->Project Structure或者Ctrl+Alt+Shift+再或者选中文件夹后右键打开工具栏，选择Mar Directory as，选择Modules，给java，resources，test文件夹标记。

![](https://upload-images.jianshu.io/upload_images/2765653-7c8f2c36a5fb9c2e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

单击选中java文件夹，再单击Sources，resources文件夹对应Resources，test文件夹对应Tests，OK，这时候被标记的文件夹就变色了，说明标记成功。

![](https://upload-images.jianshu.io/upload_images/2765653-5cc96c316ff8573e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/2765653-83d69d6fe3e3221e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接下来在java文件夹里建立需要的包，结构如下:

![](https://upload-images.jianshu.io/upload_images/2765653-7da30e3ea33d51c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


9. 现在可以对SpringMVC进行设置了，首先配置web.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
 
    <display-name>Archetype Created Web Application</display-name>
    <!--welcome pages-->
    <welcome-file-list>
        <welcome-file>index.jsp</welcome-file>
    </welcome-file-list>
 
    <!--配置springmvc DispatcherServlet-->
    <servlet>
        <servlet-name>springMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <!--配置dispatcher.xml作为mvc的配置文件-->
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/dispatcher-servlet.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
        <async-supported>true</async-supported>
    </servlet>
    <servlet-mapping>
        <servlet-name>springMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    <!--把applicationContext.xml加入到配置文件中-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/applicationContext.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
</web-app>
```

10. 配置dispatcher-servlet.xml，负责mvc的配置,```<context:component-scan base-package="com.sangyu.controller"/>```中的base-package要和自己的项目保持一致，不然会报错

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!--此文件负责整个mvc中的配置-->

    <!--启用spring的一些annotation -->
    <context:annotation-config/>

    <!-- 配置注解驱动 可以将request参数与绑定到controller参数上 -->
    <mvc:annotation-driven/>

    <!--静态资源映射-->
    <!--本项目把静态资源放在了webapp的statics目录下，资源映射如下-->
    <mvc:resources mapping="/css/**" location="/statics/css/"/>
    <mvc:resources mapping="/js/**" location="/statics/js/"/>
    <mvc:resources mapping="/image/**" location="/statics/images/"/>
    <mvc:default-servlet-handler />  <!--这句要加上，要不然可能会访问不到静态资源，具体作用自行百度-->

    <!-- 对模型视图名称的解析，即在模型视图名称添加前后缀(如果最后一个还是表示文件夹,则最后的斜杠不要漏了) 使用JSP-->
    <!-- 默认的视图解析器 在上边的解析错误时使用 (默认使用html)- -->
    <bean id="defaultViewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>
        <property name="prefix" value="/views/"/><!--设置JSP文件的目录位置-->
        <property name="suffix" value=".jsp"/>
        <property name="exposeContextBeansAsAttributes" value="true"/>
    </bean>

    <!-- 自动扫描装配 -->
    <context:component-scan base-package="com.sangyu.controller"/>
</beans>
```

11. 配置applicationContext.xml，负责一些非MVC组件的配置，暂时没有所以是空的，但也可以扫描一下


```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd 
                           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
    <context:component-scan base-package="com.sangyu"/>
</beans>
```

12. 在controller包里新建一个DemoController.java，代码如下：

```
package com.sangyu.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/home")
public class DemoController {

    @RequestMapping("/index")
    public String index(){
        return "index";
    }
}
```
在views文件夹下新建一个index.jsp，statics/css下新建一个index.css

![](https://upload-images.jianshu.io/upload_images/2765653-73193d981dd39d37.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

13. 接下来该配置Tomcat了，点击Run，选择Edit Configurations

![](https://upload-images.jianshu.io/upload_images/2765653-e248ea3e73bc45a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击加号选择Tomcat server --> Local

![](https://upload-images.jianshu.io/upload_images/2765653-42ab51b1f9449c26.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们先配置Deployment吧，点击加号，选择Artifact...

![](https://upload-images.jianshu.io/upload_images/2765653-b685c215731c58de.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

选择第二个，一定要选择war exploded，要不然会报错，OK

![](https://upload-images.jianshu.io/upload_images/2765653-39c5301990986c79.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里的名字和项目名一样，这里也就是springmvc-test07
![](https://upload-images.jianshu.io/upload_images/2765653-7ba59e1aaabb6743.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

设置Server，可以给Tomcat取个名字，Configure 选择自己安装好的Tomcat，根据个人习惯设置一个默认的浏览器。

然后On 'Update' action 和 On frame deactivation两项都选择Update classes and resources，这是为了当我们修改了jsp、css、js等静态资源的时候，立即生效，不需要重启Tomcat，直接在页面上刷新就可以看到效果。之前之所以先配置Deployment，是因为要先配置里面的Artifact，这两项要依赖于exploded，要不然Update classes and resources是没有的，只是为了方便而已啦。设置完成后，OK

![](https://upload-images.jianshu.io/upload_images/2765653-f4d055d24162dad4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

14. 运行Tomcat试试吧，在地址栏输入 http://localhost:8080/Demo/home/index.jsp

![](https://upload-images.jianshu.io/upload_images/2765653-5826892ec08ca1d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](https://upload-images.jianshu.io/upload_images/2765653-0a8e461f77105d8d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


运行时可能会报这个异常：```严重: Error configuring application listener of class org.springframework.web.context.ContextLoaderListener```

可能导致的原因时由于tomcat服务器里的项目的web-info\lib下没有加载了依赖包，通过下面的方式导入所有的jar到web-info\lib中，就可以了

![](https://upload-images.jianshu.io/upload_images/2765653-86fff7e4752415c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 二、SpringMVC-HelloWorld


1. 创建Maven工程：[可以参考这个链接](https://www.jianshu.com/p/790ff88d3a64)

2. pom注入依赖的jar包
```
<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
    <!-- https://mvnrepository.com/artifact/commons-logging/commons-logging -->
    <dependency>
      <groupId>commons-logging</groupId>
      <artifactId>commons-logging</artifactId>
      <version>1.1.1</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-beans -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>5.1.12.RELEASE</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.1.12.RELEASE</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-core -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>5.1.12.RELEASE</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-expression -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>5.1.12.RELEASE</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-web -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.1.12.RELEASE</version>
    </dependency>
    <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.1.12.RELEASE</version>
    </dependency>
  </dependencies>
```
3.  配置web.xml文件
```
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
  <display-name>Archetype Created Web Application</display-name>
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/applicationContext.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- 配置DispatcherServlet的一个初始化参数：配置SpringMVC配置文件的位置和名称-->
        <!-- 实际上也可以不通过contextConfigLocation 来配置SpringMVC的配置文件，而使用默认的-->
        <!-- 默认的配置文件为：/WEB-INF/<servlet-name>-servlet.xml -->
<!--        <init-param>-->
<!--            <param-name>contextConfigLocation</param-name>-->
<!--            <param-value>classpath:springmvc:xml</param-value>-->
<!--        </init-param>-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```
4. 配置dispatcher-servlet.xml文件

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!-- 配置自动扫描的包-->
    <context:component-scan base-package="com.sangyu.springmvc"></context:component-scan>
    <!-- 配置视图解析器：如何把handler方法返回值解析为实际的物理视图-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"></property>
        <property name="suffix" value=".jsp"></property>
    </bean>
</beans>

```

5. 编写HelloWorld.java文件
```
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HelloWorld {
    /**
     * 1. 使用@RequestMapping 注解来映射请求的URL
     * 2. 返回值会通过视图解析器解析为实际的物理视图，对于InternalResourceViewResolver
     * 视图解析器，会做如下的解析：
     * 通过prefix + returnVal + suffix，得到实际的物理视图，然后做转发操作
     * /WEB-INF/views/success.jsp
     * @return
     */
    @RequestMapping("/helloworld")
    public String hello(){
        System.out.println("hello world");
        return "success";
    }
}
```

6. 编写index.jsp
```
<html>
<body>
<h2>Hello World!</h2>
<a href="helloworld">Hello World!</a>
</body>
</html>
```

7. 创建success.jsp文件
```
<body>
<h4> success page</h4>
</body>
```

8. 配置tomcat，[可以参考这个链接](https://www.jianshu.com/p/790ff88d3a64)，tomcat配置完成后如下图：
![](https://upload-images.jianshu.io/upload_images/2765653-460b114987f4e0dc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-8bf2b7f2f6990357.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


9. 整个项目的目录结构

![](https://upload-images.jianshu.io/upload_images/2765653-f1900f203a08d50c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

10. 执行tomcat
![](https://upload-images.jianshu.io/upload_images/2765653-bf3548169a55e2fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-4df47de4eb8b4305.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



11. HelloWorld 运行流程图

![](https://upload-images.jianshu.io/upload_images/2765653-44705bf02925f53f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 三、@RequestMapping 注解

SpringMVC 使用@RequestMapping注解为控制器指定可以处理哪些URL请求，在控制器的类定义及方法定义处都可标注：

- 类定义处：提供初步的请求映射信息。相当于WEB应用的根目录

```
@Controller
@RequestMapping("/springmvc")
public class HelloWorld {
    @RequestMapping("/helloworld")
    public String hello(){
        System.out.println("hello world");
        return "success";
    }
}
// 请求的URL
<a href="springmvc/helloworld">Hello World!</a>
```

- 方法处：提供进一步的细分映射信息。相对于类定义处的URL。若类定义处未标注，则方法处标记的URL相当于WEB应用的根目录

```
@Controller
public class HelloWorld {
    @RequestMapping("/helloworld")
    public String hello(){
        System.out.println("hello world");
        return "success";
    }
}
// 请求的URL
<a href="helloworld">Hello World!</a>
```

@RequestMapping的value、method、params及heads分别表示请求URL、请求方法、请求参数及请求头的映射条件，联合使用多个条件可让请求映射更加精确化

params

```
@RequestMapping(value = "/helloworld01",params = "myParam=myValue") // 请求必须包含名为param1的请求参数,且值为myValue
    public String hello01(){
        System.out.println("hello world");
        return "success";
    }

    @RequestMapping(value = "/helloworld02",params = "myParam") // 请求必须包含名为param1的请求参数
    public String hello02(){
        System.out.println("hello world");
        return "success";
    }

    @RequestMapping(value = "/helloworld03",params = "!myParam!") // 请求不能包含名为param1的请求参数
    public String hello03(){
        System.out.println("hello world");
        return "success";
    }

    @RequestMapping(value = "/helloworld04",params = "myParam!=myValue") // 请求必须包含名为param1的请求参数，但值不能为value1
    public String hello04(){
        System.out.println("hello world");
        return "success";
    }

    @RequestMapping(value = "/helloworld05",params = {"param1=value1","param2"}) // 请求必须包含名为param1和param2的请求参数，且param1参数的值必须为value1
    public String hello05(){
        System.out.println("hello world");
        return "success";
    }
```
在index.jsp中验证params
```
<a href="springmvc/helloworld02?myParam">test param</a>
<a href="springmvc/helloworld03?myParammmmmm">test !param</a>
<a href="springmvc/helloworld04?myParam=myValueeeeeeee">test param1!=value1</a>
<a href="springmvc/helloworld05?param1=value1&param2=2222">test {"param1 = value1","param2"}</a>
```



Ant 风格资源地址支持3种匹配符：

```
    @RequestMapping(value = "/helloworld06/*/abc") //中间的*可以替代任意数量字符
    public String hello06(){
        System.out.println("hello world");
        return "success";
    }

    @RequestMapping(value = "/helloworld07/**/abc") //中间的**可以匹配任意层级，或者/helloworld06/abc
    public String hello07(){
        System.out.println("hello world");
        return "success";
    }

    @RequestMapping(value = "/helloworld08/abc??") //一个？匹配一个字符
    public String hello08(){
        System.out.println("hello world");
        return "success";
    }
```

```
<a href="springmvc/helloworld06/aaaaaabbb/abc">test ant*</a>
<br><br>
<a href="springmvc/helloworld07/aaaaaabbb/ggggggg/hhhhhhh/abc">test ant**</a>
<br><br>
<a href="springmvc/helloworld07/abc">test ant**hhhh</a>
<br><br>
<a href="springmvc/helloworld08/abc11">test ant？？</a>
```
### @PathVariable注解 映射URL绑定的占位符

URL中的{xxx}占位符可以通过@PathVariable("xxx")绑定到操作方法的入参中

```
@Controller
@RequestMapping("/springmvc")
public class HelloWorld {
    @RequestMapping("/helloworld/{id}")
    public String hello(@PathVariable("id") Integer id){
        System.out.println("hello world" + id);
        return "success";
    }
}
// 请求的URL
<a href="/springmvc/helloworld/1">qqq</a>
```


### HiddenHttpMethodFilter 过滤器

使用HiddenHttpMethodFilter前要先了解下REST概念，**REST是指（资源）表现层状态转化。是目前最流行的一种互联网软件架构**

> 资源：网络上的一个实体，或者说是网络上的一个具体信息。它可以是一段文本、一张图片等等，每种资源对应一个特定的URI。因此URI即为每一个资源的独一无二的标识符
>
> 表现层：把资源具体呈现出来的形式。比如，文本可以用txt格式表现，也可以用HTML格式、XML格式等
>
> 状态转化：每发出一个请求，就代表了客户端和服务器的一次交互过程。HTTP协议，是一个无状态协议，即所有的状态都保存在服务器端，因此，如果客户端想要操作服务器，必须通过某种手段，让服务器端发生“状态转化”，而这种转化是建立在表现层之上的，所以就是“表现层状态转化”。具体说，就是HTTP协议里面，四个表示操作方式的动词：GET、POST、DELETE、PUT，它们分别对应四种基本操作：获取资源、新建资源、删除资源、更新资源

```
/order/1 HTTP GET : 得到 id = 1的order
/order/1 HTTP DELETE ： 删除id = 1的order
/order/1 HTTP PUT ： 更新id=1的order
/order HTTP POST：新增order
```

浏览器form表单只支持GET和POST请求，而DELETE、PUT等method并不支持，HiddenHttpMethodFilter可以将这些请求转换为标准的http方法，使得支持GET、POST、PUT与DELETE请求

web.xml增加HiddenHttpMethodFilter的配置
```
// web.xml
<!DOCTYPE web-app PUBLIC
 "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
 "http://java.sun.com/dtd/web-app_2_3.dtd" >
<web-app>
    <display-name>Archetype Created Web Application</display-name>
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>/WEB-INF/applicationContext.xml</param-value>
    </context-param>
    <!-- 配置org.springframework.web.filter.HiddenHttpMethodFilter：可以把POST请求转为DELEte或POST请求-->
    <filter>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
    </filter>
    <filter-mapping>
        <filter-name>HiddenHttpMethodFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```
```
@Controller
@RequestMapping("/springmvc")
public class HelloWorld {
     /**
     * 如何发送PUT请求和DELETE请求呢？
     * 1。 配置HiddenHttpMethodFilter
     * 2。发送POST请求，并携带一个name="_method"的隐藏域，值为DELETE 或 PUT
     * @param id
     * @return
     */
    @RequestMapping(value = "/helloworld/{id}",method = RequestMethod.GET)
    public String testRestGet(@PathVariable Integer id){
        System.out.println("GET" + id);
        return "success";
    }

    @RequestMapping(value = "/helloworld",method = RequestMethod.POST)
    public String testRestPost(){
        System.out.println("POST");
        return "success";
    }

    @RequestMapping(value = "/helloworld/{id}",method = RequestMethod.DELETE)
    public String testRestDelete(@PathVariable Integer id){
        System.out.println("DELETE" + id);
        return "success";
    }

    @RequestMapping(value = "/helloworld/{id}",method = RequestMethod.PUT)
    public String testRestPut(@PathVariable Integer id){
        System.out.println("PUT" + id);
        return "success";
    }
}
```


```
<%--GET请求--%>
<a href="/springmvc/helloworld/1">GET</a>

<%--POST请求--%>
<form action="springmvc/helloworld" method="post">
    <input type="submit" value="POST">
</form>

<%--DELETE请求--%>
<form action="/springmvc/helloworld/1" method="post">
    <input type="hidden" name="_method" value="DELETE">
    <input type="submit" value="DELETE">
</form>

<%--PUT请求--%>
<form action="/springmvc/helloworld/1" method="post">
    <input type="hidden" name="_method" value="PUT">
    <input type="submit" value="PUT">
</form>
```

## 四、@RequestParam 注解

在处理方法入参使用@RequestParam 可以把请求参数传递给请求方法：
- value：参数名
- required：是否必须。默认为true，表示请求参数中必须包含对应的参数，若不存在，将抛出异常

```
// 两个参数是必须的，必须携带参数和参数值
@Controller
@RequestMapping("/springmvc")
public class HelloWorld {
    @RequestMapping("/helloparam01")
    public String testRequestParam(@RequestParam(value="username") String un , // 这个时候两个参数是必须的，必须携带参数和参数值
                              @RequestParam(value = "age" )int age) {
        System.out.println("test,username: " + un + ",age : " + age );
        return "success";
    }
}
```

```
// 这个时候age参数不是必须的
@Controller
@RequestMapping("/springmvc")
public class HelloWorld {   
    @RequestMapping("/helloparam02")
    public String testRequestParam01(@RequestParam(value="username") String un , // 这个时候age参数不是必须的
                                     @RequestParam(value = "age",required = false)Integer age){
        System.out.println("test,username: " + un + ",age : " + age );
        return "success";
    }
}
```

```
// 参数使用默认值
@Controller
@RequestMapping("/springmvc")
public class HelloWorld {
    @RequestMapping("/helloparam03")
    public String testRequestParam02(@RequestParam(value="username") String un , // 参数使用默认值
                                     @RequestParam(value = "age",required = false,defaultValue = "0")int age){
        System.out.println("test,username: " + un + ",age : " + age );
        return "success";
    }
}
```

## 五、@RequestHeader 注解

使用@RequestHeader 绑定请求报头的属性值

- 请求头包含了若干个属性，服务器可据此获知客户端的信息，通过@RequestHeader 即可将请求头中的属性值绑定到处理方法的入参中

```
@Controller
@RequestMapping("/springmvc")
public class HelloWorld {
    @RequestMapping(value = "/helloworld")
    public String testRequestHeader(@RequestHeader(value = "Accept-Language")String al) {
        System.out.println("test: "  + al );
        return "success";
    }
}
// 请求的URL
<a href="/springmvc/helloworld">Test</a>
```

## 六、@CookieValue 注解

使用@CookieValue可让处理方法入参绑定某个Cookie值

```
@Controller
@RequestMapping("/springmvc")
public class HelloWorld {
    @RequestMapping(value = "/helloworld")
    public String testRequestHeader(@CookieValue("JSESSIONID") String sessionID) {
        System.out.println("test: " + sessionID);
        return "success";
    }
}
// 请求的URL
<a href="/springmvc/helloworld">TestCookie</a>
```

## 七、使用POJO对象绑定请求参数值

SpringMVC 会按请求参数名和POJO属性名进行自动匹配，自动为该对象填充属性值。支持级联属性

```
public class User {

    private String username;
    private String password;

    private String email;
    private int age;
    private Address address;

    public void setUsername(String username) {
        this.username = username;
    }

    public String getUsername() {
        return username;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getPassword() {
        return password;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getEmail() {
        return email;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    public Address getAddress() {
        return address;
    }

    @Override
    public String toString() {
        return "User{" +
                "username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", email='" + email + '\'' +
                ", age=" + age +
                ", address=" + address +
                '}';
    }
}
```

```
public class Address {

    private String province;
    private String city;

    public void setProvince(String province) {
        this.province = province;
    }

    public String getProvince() {
        return province;
    }

    public void setCity(String city) {
        this.city = city;
    }

    public String getCity() {
        return city;
    }

    @Override
    public String toString() {
        return "Address{" +
                "province='" + province + '\'' +
                ", city='" + city + '\'' +
                '}';
    }
}
```
```
@Controller
@RequestMapping("/springmvc")
public class TestController {


    /**
     * SpringMVC 会按请求参数名和POJO属性名进行自动匹配
     * @param user
     * @return
     */
    @RequestMapping("/testPojo")
    public String testPojo(User user){
        System.out.println("testPojo : " + user);
        return "success";
    }
}
```
```
<form action="/springmvc/testPojo" method="post">
    username:<input type="text" name="username">
    password:<input type="password" name="password">
    email:<input type="text" name="email">
    age:<input type="text" name="age">
    city:<input type="text" name="address.city">
    province:<input type="text" name="address.province">
    <input type="submit" name="Submit">
</form>
```

## 八、ModelAndView

控制器处理方法的返回值是ModelAndView，则其既包含视图信息，也包含模型数据信息

```
// success.jsp 返回的目标页面
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
</head>
<body>
<h4> success page</h4>
time:${requestScope.time}
time:${time}
</body>
</html>
```

```
// index.jsp
<a href="/springmvc/testModelAndView">testModelAndView</a>
```

```
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;
import java.util.Date;

@Controller
@RequestMapping("/springmvc")
public class TestController {

    @RequestMapping("/testModelAndView")
    public ModelAndView testModelAndView(){
        String viewName = "success";
        ModelAndView modelAndView = new ModelAndView(viewName);

        // 添加模型数据到ModelAndView中
        modelAndView.addObject("time",new Date());
        return modelAndView;
    }
}
```

## 九、 Map&Model

Spring MVC 在内部使用了一个```org.springframework.ui.Model```接口存储模型数据，具体步骤：
1）SpringMVC在调用方法前会创建一个隐含的数据模型，作为模型数据的存储容器， 成为”隐含模型”
2）如果方法的入参类型为Map或Model，会将隐含模型的引用传递给这些入参。
3）在方法体内，可以通过这个入参对象访问到模型中的所有数据，也可以向模型中添加新的属性数据

Spring Web MVC 提供Model、Map或ModelMap让我们能去暴露渲染视图需要的模型数据。

```
@Controller
@RequestMapping("/springmvc")
public class TestController {
    /**
     * 目标方法可以添加Map类型（实际上也可以是Model类型或ModelMap类型）的参数
     * @param map
     * @return
     */
    @RequestMapping("/testMap")
    public String testMap(Map<String,Object> map, Model model, ModelMap modelMap){
        model.addAttribute("a","aaa");
        map.put("names", Arrays.asList("Tom","Jerry","Mike"));
        modelMap.put("b","bbbbb");
        return "success";
    }
}

```

```
// success.jsp 返回的目标页面
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
</head>
<body>
<h4> success page</h4>
name:${requestScope.names}<br>
a:${requestScope.a}<br>
b:${requestScope.b}<br>
</body>
</html>
```

```
// index.jsp
<a href="/springmvc/testMap">testMap</a>
```

## 十、@SessionAttributes 注解

> - 若希望在多个请求之间共用某个模型属性数据，则可以在控制器上标注一个@SessionAttributes，配置需要在session中存放的数据范围，Spring MVC将存放在model中对应的数据暂存到HttpSession 中。
>
> - @SessionAttributes只能使用在类定义上。
> 
> - @SessionAttributes 除了可以通过属性名指定需要放到会话中的属性处，还可以通过模型属性的对象类型指定哪些模型属性需要放到会话中
>             
>      1. @SessionAttributes(types=User.class) 会将model中所有类型为 User的属性添加到会话中。
>      2. @SessionAttributes(value={"user1","user2"}) 会将model中属性名为user1和user2的属性添加到会话中。
>      3. @SessionAttributes(types={User.class,Dept.class}) 会将model中所有类型为 User和Dept的属性添加到会话中。
>      4. @SessionAttributes(value={"user1","user2"},types={Dept.class}) 会将model中属性名为user1和user2以及类型为Dept的属性添加到会话中。
> - value和type之间是并集关系


通过一个例子来说明


```
public class User {

    private String username;
    private String password;

    private String email;
    private int age;
    private Address address;

    public void setUsername(String username) {
        this.username = username;
    }

    public String getUsername() {
        return username;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getPassword() {
        return password;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getEmail() {
        return email;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    public Address getAddress() {
        return address;
    }

    @Override
    public String toString() {
        return "User{" +
                "username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", email='" + email + '\'' +
                ", age=" + age +
                ", address=" + address +
                '}';
    }

    public User(String username,String password,String email,int age){
        super();
        this.username = username;
        this.password = password;
        this.email = email;
        this.age = age;
    }

    public User(){}
}
```

```
@Controller
@RequestMapping("/springmvc")
@SessionAttributes(value = {"user"},types = {String.class})
public class TestController {
    /**
     * @SessionAttributes 除了可以通过属性名指定需要放到会话中属性外（使用的是value属性值）
     * 还可以通过模式属性的对象类型指定哪些模型属性需要放到会话中（实际上使用的是types属性值）
     * 注意，该注解只能放在类的上面，而不能修饰方法
     * @param map
     * @return
     */
    @RequestMapping("/testSessionAttributes")
    public String testSessionAttributes(Map<String,Object> map){

        User user = new User("Tom","123","aa@aa.com",15);
        map.put("user",user);
        map.put("school","hhh");
        return "success";
    }
}
```

```
// success.jsp 返回的目标页面
<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
</head>
<body>
<h4> success page</h4>
request user:${requestScope.user}
session user:${sessionScope.user}
request school:${sessionScope.school}
session school:${sessionScope.school}
</body>
</html>
```
```
// index.jsp
<a href="/springmvc/testSessionAttributes">testMap</a>
```

## 十一、@ModelAttribute 注解

### @ModelAttribute 注释方法

```
@Controller
@RequestMapping("/springmvc")
public class TestController {
    /**
     * 运行流程：@ModelAttribute注释的方法会在此controller每个方法执行前被执行
     * 1. 执行 @ModelAttribute 修饰的方法：模拟数据库取出行为，将user对象存储到map中，键为 user
     * 2. 然后在渲染页面时，模拟回显数据，将model中的数据取出并显示在页面，并把表单的请求参数赋给User对象的对应属性
     * 3. sprinngMVC 最后把上述对象传入目标方法的参数
     * 要注意的是：在存入map时，map的键值要和被@RequestMapping("/testModelAttribute")修饰的目标方法入参类型的第一个字符串的字符串一致
     * @param user
     * @return
     */
    @RequestMapping("/testModelAttribute")
    public String testModelAttribute01(User user){
        System.out.println("修改： " + user);
        return "success";
    }

    /**
     * @ModelAttribute 标记的方法，会在每个目标方法执行之前被SpringMVC调用
     * @param id
     * @param map
     */
    @ModelAttribute
    public void testModelAttribute(@RequestParam(value = "id",required = false)
                                                 Integer id,Map<String,Object> map){

        if(id != null){
            // 模拟从数据库中获取对象
            User user = new User(1,"Tom","123456","aa@aa.com",12);
            System.out.println("从数据库中获取一个对象：" + user);
            map.put("user",user);
        }
    }
}
```
```
public class User {

    private Integer id;
    private String username;
    private String password;

    private String email;
    private int age;
    private Address address;

    public void setUsername(String username) {
        this.username = username;
    }

    public String getUsername() {
        return username;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getPassword() {
        return password;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getEmail() {
        return email;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public int getAge() {
        return age;
    }

    public void setAddress(Address address) {
        this.address = address;
    }

    public Address getAddress() {
        return address;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public Integer getId() {
        return id;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", email='" + email + '\'' +
                ", age=" + age +
                '}';
    }

    public User(Integer id,String username, String password, String email, int age){
        super();
        this.username = username;
        this.password = password;
        this.email = email;
        this.age = age;
        this.id = id;
    }

    public User(){}
}
```

```
<!--
    模拟修改操作
    1. 原始数据：1，Tom，aa@aa.com，12
    2. 密码不能被修改
    3. 表单回显，模拟操作直接填写对应的属性值

-->
<form action="/springmvc/testModelAttribute" method="post">
    <input type="hidden" name="id" value="1">
    username:<input type="text" name="username" value="Tom">
    email:<input type="text" name="email" value="aa@aa.com">
    age:<input type="text" name="age" value="12">
    <input type="submit" name="Submit">
</form>
```
### @ModelAttribute 注释参数

@ModelAttribute("user") User user注释方法参数，参数user的值来源于testModelAttribute03()方法中的model属性。

```
@ModelAttribute("user")
    public User testModelAttribute03(){
        return new User(1,"aa","123","aa@aa.com",12);
    }

    @RequestMapping("/testModelAttribute01")
    public String testModelAttribute04(@ModelAttribute("user") User user){
        user.setUsername("bb");
        return "success";
    }
```

## 十二、使用servlet原生API作为参数

```
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>javax.servlet-api</artifactId>
  <version>3.1.0</version>
  <scope>provided</scope>
</dependency>
```

```
 /**
     * 可以使用Servlet 原生的API作为目标方法的参数 具体支持以下类型： 
     * HttpServletRequest
     * HttpServletResponse
     * HttpSession
     * java.secutiy.Principal
     * Locale InputStream
     * OutputStram
     * Reader
     * writer
     * @param request
     * @param response
     * @param out
     * @throws IOException
     */
    @RequestMapping("/testServletAPI")
    public void testServletAPI(HttpServletRequest request, HttpServletResponse response, Writer out) throws IOException {
        System.out.println("testServletAPI, " + request + ", " + response);
        out.write("hello springmvc");
//        return "success";
    }
```

## 十三、SpringMVC自定义视图

```
@Component
public class HelloView implements View {

    @Override
    public String getContentType() {
        return "text/html";
    }

    @Override
    public void render(Map<String, ?> map, HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws Exception {

        httpServletResponse.getWriter().print("hello view ,time :" + new Date());
    }
}
```

```
@Controller
@RequestMapping("/springmvc")
public class TestController {
    @RequestMapping("/testView")
    public String testView(){
        System.out.println("testView");
        return "helloView";
    }
}
```

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <!-- 配置自动扫描的包-->
    <context:component-scan base-package="com.sangyu.springmvc"></context:component-scan>
    <!-- 配置视图解析器：如何把handler方法返回值解析为实际的物理视图-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"></property>
        <property name="suffix" value=".jsp"></property>
    </bean>
<!--BeanNameViewResolver ：将逻辑视图名解析为一个Bean，Bean的id等于逻辑视图名-->
<!-- 通过order 属性来定义视图解析器的优先级，order越小优先级越高-->
    <bean class="org.springframework.web.servlet.view.BeanNameViewResolver">
        <property name="order" value="100"></property>
    </bean>
</beans>
```

```
<a href="/springmvc/testView">Test testView</a>
```

## 十四、Springmvc 重定向

如果返回的字符串中前缀带forward: 或 redirect:指示符时，SpringMVC会特殊处理
- redirect:/index.jsp：会完成一个到index.jsp的重定向操作
- forward:/index.jsp：会完成一个到index.jsp的转发操作
```
@Controller
@RequestMapping("/springmvc")
public class TestController {
    @RequestMapping("/testRedirect")
    public String testRedirect(){
        System.out.println("testRedirect");
        return "redirect:/index.jsp"; // 会完成一个到success.jsp的重定向的操作
    }
}
```

```
<a href="/springmvc/testRedirect">Test testRedirect</a>
```

## 十五、SpringMVC-处理静态资源

若将DispatcherServlet 请求映射配置为/，则SpringMVC 将捕获WEB容器的所有请求，包括静态资源的请求，SpringMVC会将他们当成一个普通请求处理因此找不到对应处理器将导致错误，可以在SpringMVC的配置文件中配置```<mvc:default-servlet-handler/>```的方式解决静态资源的问题。

  ```<mvc:default-servlet-handler/>``` 将在SpringMVC上下文中定义一个DefaultServletHttpRequestHandler，它会对进入DispatcherServlet的请求进行筛查，如果发生是没有既让过映射的请求，就将该请求交由WEB应用服务器默认的Servlet处理，如果不是静态资源的请求，才由DispatcherServlet继续处理

![](https://upload-images.jianshu.io/upload_images/2765653-092fa39b7ff62c48.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-ddb45304a9f6da9b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)








