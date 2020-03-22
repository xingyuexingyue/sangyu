## 目录

[一、什么是分布式系统](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E4%B8%80%E4%BB%80%E4%B9%88%E6%98%AF%E5%88%86%E5%B8%83%E5%BC%8F%E7%B3%BB%E7%BB%9F)

[二、应用的架构演变图](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E4%BA%8C%E5%BA%94%E7%94%A8%E7%9A%84%E6%9E%B6%E6%9E%84%E6%BC%94%E5%8F%98%E5%9B%BE)

[三、什么是RPC](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E4%B8%89%E4%BB%80%E4%B9%88%E6%98%AFrpc)

[四、PRC基本原理](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E5%9B%9Bprc%E5%9F%BA%E6%9C%AC%E5%8E%9F%E7%90%86)

[五、PRC框架](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E4%BA%94prc%E6%A1%86%E6%9E%B6)

[六、Dubbo简介](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E5%85%AD-dubbo%E7%AE%80%E4%BB%8B)

[七、Dubbo基本概念](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E4%B8%83dubbo%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5)

[八、zookeeper 基本介绍](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E5%85%ABzookeeper-%E5%9F%BA%E6%9C%AC%E4%BB%8B%E7%BB%8D)

[九、zookeeper环境搭建(mac)](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E4%B9%9Dzookeeper%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BAmac)

[十、mac安装dubbo-admin管理控制台](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E5%8D%81mac%E5%AE%89%E8%A3%85dubbo-admin%E7%AE%A1%E7%90%86%E6%8E%A7%E5%88%B6%E5%8F%B0)

[十一、dubbo-helloworld](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E5%8D%81%E4%B8%80dubbo-helloworld)

[十二、Dubbo安装监控中心-Dubbo-Monitor-simple](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E5%8D%81%E4%BA%8Cdubbo%E5%AE%89%E8%A3%85%E7%9B%91%E6%8E%A7%E4%B8%AD%E5%BF%83-dubbo-monitor-simple)

[十三、Dubbo与SpringBoot整合](https://github.com/xingyuexingyue/sangyu/blob/master/study/Dubbo.md#%E5%8D%81%E4%B8%89dubbo%E4%B8%8Espringboot%E6%95%B4%E5%90%88)


## 一、什么是分布式系统 

分布式系统是若干独立计算机的集合，这些计算机对于用户来说就像单个相关系统

分布式系统（distributed system）是建立在网络之上的软件系统

分布式系统出现的原因是：随着互联网的发展，网站应用的规模不断扩大，常规的垂直应用架构已无法应对，分布式服务架构以及流动计算架构势在必行，需要一个治理系统确保架构有条不紊的演进

## 二、应用的架构演变图

![](https://upload-images.jianshu.io/upload_images/2765653-d7d76c9e3e0791ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上图描述了从单一应用架构-->垂直应用架构-->分布式服务架构-->流动计算架构，应用的发展演变过程

**1. 单一应用架构**

当网站流量很小时，只需一个应用，将所有功能都部署在一起，以减少部署节点和成本。此时，用于简化增删改查工作量的数据访问框架（ORM）是关键

![单一应用架构图](https://upload-images.jianshu.io/upload_images/2765653-629740078a3aaac4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

适用于小型网站，小型管理系统，将所有功能都部署到一个功能里，简单易用。

缺点：

1. 性能扩展都比较差
2. 协同开发问题
3. 不利于升级维护

**2. 垂直应用架构**

当访问量逐渐增大，单一应用增加机器带来的加速度越来越小，将应用拆成互不相干的几个应用，以提升效率，此时，用于加速前端页面开发的Web框架(MVC)是关键。

![垂直应用架构图](https://upload-images.jianshu.io/upload_images/2765653-225b10dec5f06d13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


当一个应用拆分为几个小应用，部署到不同的服务器上，并且每个小应用都是完整的，从页面到业务逻辑到程序和DB，当某一个应该访问量比较大的时候，可以对这个应该多增加几个服务器

通过切分业务来实现各个模块独立部署，降低了维护和部署的难度，团队各司其职更易管理性能扩展也更方便，更有针对性

缺点：
1. 每个应用的完整性，比如页面的修改都要重新部署，没有做到界面+业务逻辑的实现分离

2.每个应用无法做到完全的独立，比如订单可能要用到用户的信息，每个应用之间有交互的需要

**3. 分布式服务架构**

当垂直应用越来越多，应用之间交互不可避免，将核心业务抽取出来，作为独立的服务，逐渐形成稳定的服务中心，使前端应用能更快速的响应多变的市场需求。此时，用于提高业务复用及整合分布式服务框架（RPC）是关键

![分布式服务架构图](https://upload-images.jianshu.io/upload_images/2765653-c3c94a98d46a2cdd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



分布式服务架构拆分不同的功能业务，并且不同的功能页面又将界面与业务逻辑分离，业务逻辑和界面是部署到不同服务器，不同的服务器之间的服务调用通过RPC(远程过程调用)调用(同一台服务器是简称件通信)

分布式服务架构带来的问题，是如何进行远程过程调用，以及如何拆分业务提升业务的复用程度，通过RPC(分布式服务框架)可以解决远程过程调用，但其他问题是，随着业务拆分越来越多，可能会有成千上万的服务器在运行不同的服务，会出现资源浪费的情况，**是否可以提高资源的利用率，通过访问量来动态分配服务器**

**4. 流动计算架构**

当服务越来越多，容量的评估，小服务资源的浪费等问题逐渐显现，此时需增加一个调度中心基于访问压力实时管理集群容量，提高集群利用率。此时，用于提高机器利用率的资源调用和治理中心(SOA)是关键

![流动计算架构图](https://upload-images.jianshu.io/upload_images/2765653-8b31d4289e9116b1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


流动计算架构引入调度中心，维护注册中心的所有服务调用关系，实时管理服务集群，根据不同的服务的访问请求量调整服务器数量，并且根据相同服务不同服务器请求的数量调整下次访问哪台服务器处理请求，以此提高集群利用率

## 三、什么是RPC

RPC(Remote Procedure Call)是指远程过程调用，是一种进程间通信方式，他是一种技术的思想，而不是规范。它允许程序调用另一个地址空间（通常是共享网络的另一台机器）的过程或函数，而不是程序员显式编码这个远程调用的细节。即程序员无论是调用本地的还是远程的函数，本质上编写的调用代码基本相同


## 四、PRC基本原理

![RPC基本原理图](https://upload-images.jianshu.io/upload_images/2765653-37f31bd0a8f08b23.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


举个例子

A服务器上有段代码
```
hello(){
  String msg = b.hi(new User("Tom"));
  System.out.println(msg);
}
```

另一台B服务器上有段代码

```
String hi(User user){
  return "hi : " + user.getName();
}
```
![A服务器方法调用B服务器方法的过程](https://upload-images.jianshu.io/upload_images/2765653-89f1ba331b75b2df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

A服务器方法调用B服务器方法，然后由A打印出B方法的返回值，A方法相当于Client，客户端发起调用请求，Client Sub在A服务器发现A要调用的方法在另一台服务器B，**将A服务器和B服务器建立连接**，并将传递的参数对象进行序列化，将内容发送给B服务器的 Server Sub，将序列化的内容反序列化，并调用对应的方法，拿到调用方法产生的返回值，将返回结果序列化传递A服务器，A收到后反序列化并展示调用结果

决定RPC性能是：序列化与反序列化效率、通讯效率(各个服务器之间建立连接)

序列化之间传递的数据不同类型之间的速度二进制流优于JSON优于XML；

## 五、PRC框架

dubbo、gRPC、Thrift、HSF

## 六、 Dubbo简介

Apache Dubbo是一款高性能、轻量级的开源Java RPC框架，它提供了三个核心能力：面向接口的远程方法调用，智能容错和负载均衡，以及服务自动注册和发现

## 七、Dubbo基本概念

![](https://upload-images.jianshu.io/upload_images/2765653-f2e614957a6e66d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**服务提供者(Provider)** :暴露服务的服务提供方，服务提供者在启动时，向注册中心注册自己提供的服务

**服务消费者(Consumer)** :调用远程服务的服务消费方，服务消费者在启动时，向注册中心订阅自己所需的服务，服务消费者，从提供者地址列表中，基于软件负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用

**注册中心(Registry)** :注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者

**监控中心(Monitor)** :服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心

**调用关系说明**

- 服务容器负责启动，加载，运行服务提供者

- 服务提供者在启动时，向注册中心注册自己提供的服务

- 服务消费者在启动时，向注册中心订阅自己所需的服务

- 注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者

- 服务消费者，从提供者地址列表中，基于软件负载均衡算法，选一台提供者进行调用，如果调用失败，再选另一台调用

- 服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心

**注册中心**

![注册中心](https://upload-images.jianshu.io/upload_images/2765653-cfd3258a76ebe6df.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

注册中心：相当于维护了一个清单，所有的服务都在注册中心注册，用于发现服务，和及时了解服务的问题，如果用户服务要了解订单服务，RPC就可以根据注册中心随机或按照一定的算法选择一个服务，找到一个服务建立起来通信，从而达到远程服务调用的作用

## 八、zookeeper 基本介绍

zookeeper是Apacahe Hadoop的子项目，是一个树型的目录服务，支持变更推送，适合作为Dubbo服务的注册中心，工业强度高，可用于生产环境，并推荐使用

## 九、zookeeper环境搭建(mac)

[此地址](https://archive.apache.org/dist/zookeeper/zookeeper-3.4.13/)
下载zookeeper-3.4.10.tar.gz
```
MacOS:10.13.1
zookeeper-3.4.13
```
1. 下载后通过命令行进入压缩包所在的目录并执行解压命令

```
tar -zxvf zookeeper-3.4.10.tar.gz  // 解压
```

2.  进入conf目录下，修改默认配置文件名称，将zoo_sample.cfg 修改为zoo.cfg 
```
cd zookeeper-3.4.10/conf  // 切换目录
mv zoo_sample.cfg zoo.cfg // 修改名称
```

3.打开文件zoo.cfg

dataDir：临时数据存储位置
clientPort：zookeeper的端口号

![](https://upload-images.jianshu.io/upload_images/2765653-02ed08831e941b3b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. 通过命令切换目录到zookeeper的目录下，启动Server

```
cd zookeeper-3.4.10/bin // 切换目录
./zkServer.sh start // 启动服务
ZooKeeper JMX enabled by default
Using config: zookeeper-3.4.10/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
```
5. cli连接

zookeeper启动后，重新打开新的命令行窗口切换目录到zookeeper的目录下，启动cli，通过cli连接zookeeper服务器

```
cd zookeeper-3.4.10/bin //切换到 bin目录
./zkCli.sh -server 127.0.0.1:2181
```

6. 使用zkCli.cmd测试

ls /:列出zookeeper根下保存的所有节点
create -e/aaa 123:创建一个aaa节点，值为123
get /aaa:获取/aaa节点的值


```
./zkCli.sh -server 127.0.0.1:2181
[zk: 127.0.0.1:2181(CONNECTED) 0] help //输入help命令
ZooKeeper -server host:port cmd args
    stat path [watch]
    set path data [version]
    ls path [watch]
    delquota [-n|-b] path
    ls2 path [watch]
    setAcl path acl
    setquota -n|-b val path
    history
    redo cmdno
    printwatches on|off
    delete path [version]
    sync path
    listquota path
    rmr path
    get path [watch]
    create [-s] [-e] path data acl
    addauth scheme auth
    quit
    getAcl path
    close
    connect host:port

/////////////////////官方测试命令////////////////////////

[zk: 127.0.0.1:2181(CONNECTED) 2] ls /
[zookeeper]
[zk: 127.0.0.1:2181(CONNECTED) 3] create /zk_test my_data
Created /zk_test
[zk: 127.0.0.1:2181(CONNECTED) 4] ls /
[zookeeper, zk_test]
[zk: 127.0.0.1:2181(CONNECTED) 5] get /zk_test
my_data
cZxid = 0x2
ctime = Wed Feb 28 15:18:45 CST 2018
mZxid = 0x2
mtime = Wed Feb 28 15:18:45 CST 2018
pZxid = 0x2
cversion = 0
dataVersion = 0
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 7
numChildren = 0
[zk: 127.0.0.1:2181(CONNECTED) 6] set /zk_test junk
cZxid = 0x2
ctime = Wed Feb 28 15:18:45 CST 2018
mZxid = 0x3
mtime = Wed Feb 28 15:20:23 CST 2018
pZxid = 0x2
cversion = 0
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 4
numChildren = 0
[zk: 127.0.0.1:2181(CONNECTED) 7] get /zk_test
junk
cZxid = 0x2
ctime = Wed Feb 28 15:18:45 CST 2018
mZxid = 0x3
mtime = Wed Feb 28 15:20:23 CST 2018
pZxid = 0x2
cversion = 0
dataVersion = 1
aclVersion = 0
ephemeralOwner = 0x0
dataLength = 4
numChildren = 0
[zk: 127.0.0.1:2181(CONNECTED) 8] delete /zk_test
[zk: 127.0.0.1:2181(CONNECTED) 9] ls
[zk: 127.0.0.1:2181(CONNECTED) 10] ls /
[zookeeper]
```

7. 停止Server
```
> ./zkServer.sh stop ////停止后，如果CLi没有关闭，将报错
```

## 十、mac安装dubbo-admin管理控制台

dubbo本身并不是一个服务软件。它其实就是一个jar包能够帮你的java程序连接到zookeeper，并利用zookeeper消费、提供服务。所以你不用在Linux上启动什么dubbo服务

但是为了让更好的管理监控众多的dubbo服务，官方提供了一个可视化的监控程序，不过这个监控即使不装也不影响使用

1. [此地址](https://github.com/locationbai/incubator-dubbo-ops-master)下载zip包并解压到本地目录下

2. 下载后查看/dubbo-admin/pom.xml 文件，Dubbo2.6之后的版本都是打jar包的方式，2.5之前都是打war包的方式(打包会形成一个web 项目需要放到tomcat里面)

![](https://upload-images.jianshu.io/upload_images/2765653-0776bcff19c13541.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 打开/dubbo-admin/src/main/resources/application.properties 文件,dubbo.registry.address 是zookeeper的地址，现在默认是本机服务器的2181端口，如果没问题可以不修改

![](https://upload-images.jianshu.io/upload_images/2765653-e835031aeefdeb99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
4. 打jar包，打开命令行窗口，进入/dubbo-admin文件所在目录，使用mvn命令(前提是要保证maven已经装好)，执行命令

```
mvn clean package // 清理并打包，清理不是必须的
```

5. 打包成功后，进入/dubbo-admin/target查看生成的jar包，

![](https://upload-images.jianshu.io/upload_images/2765653-ffa4ab8a9d6aa66a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6. 打开命令行窗口，进入上一步所在jar的目录，执行命令运行jar包

```
java -jar dubbo-admin-0.0.1-SNAPSHOT.jar
```

7. 启动后，浏览器输入http://192.168.1.100:7001/ ，打开dubbo admin的控制台，账号和密码都是root，前提一定要确保zookeeper是启动的，控制台可以监控所有的服务和应用，以及哪些是消费者，哪些是提供者

![](https://upload-images.jianshu.io/upload_images/2765653-dddecf5596975be4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 十一、dubbo-helloworld

某个电商系统，订单服务需要调用用户服务获取某个用户的所有地址，

现在需要创建两个服务模块进行测试：

|  模块  | 功能 |
|  ----  | ----  |
|订单服务web模块  | 创建订单|
| 用户服务service模块 | 查询用户地址 |

订单服务web模块一般指的是对外HTTP服务，用户服务service模块一般指的是对外提供RPC服务

测试预期结果：
订单服务web模块在A服务器，用户服务模块在B服务器，A可以远程调用B功能

![](https://upload-images.jianshu.io/upload_images/2765653-3933a2af5832d8f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

工程架构

1. 分包
建议将服务接口，服务模型，服务异常等均放在API包中，因为服务模型及异常也是API的一部分，同时，这样做也符合分包原则：重用分布等价原则(REP)，共用重用原则（CRP）-在本例中相当于gmall-interface工程，在gmall-interface工程提供了javabean和service 接口

2. 粒度
服务接口尽可能大粒度，每个服务方法应代表一个功能，而不是某功能的一个步骤，否则将面临分布式事务问题，Dubbo暂未提供分布式事务支持

服务接口建议以业务场景为单位划分，并对相近业务做抽象，防止接口数量爆炸

![](https://upload-images.jianshu.io/upload_images/2765653-9f0c48dcd0a8c9cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**创建服务提供者**

1. 使用idea 创建一个新的Maven Project 

![](https://upload-images.jianshu.io/upload_images/2765653-341200dd74db4169.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. 设置GroupId和ArtifactId,GroupId 一般为反转域名来定义，ArtifactId则是项目的具体名称

![](https://upload-images.jianshu.io/upload_images/2765653-241db0cc49e035fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 直接finish
 ![](https://upload-images.jianshu.io/upload_images/2765653-2aeab8ecba502aa7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4.在gmall下常见module，创建maven项目next

![](https://upload-images.jianshu.io/upload_images/2765653-1e96db8623f2e37c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


5.GroupId是创建project时加过的，ArtifactId是当前项目module的名称，点击next

 ![](https://upload-images.jianshu.io/upload_images/2765653-f47e60841a71da66.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


6. Module name尽量和第二步ArtifactId加的一样，没问题后Finsh，Module就创建成功了，在提供者的目录下创建具体接口实现

![](https://upload-images.jianshu.io/upload_images/2765653-b0106097442ecd17.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

目录结构

![](https://upload-images.jianshu.io/upload_images/2765653-18803bc3eaef66bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**user-service-provider用户模块：对用户接口的实现**

UserServiceImpl：服务方提供实现接口(UserService)
provider.xml：用 Spring 配置声明暴露服务
MainApplication：加载 Spring 配置

代码

```
// UserServiceImpl：服务方提供实现接口(UserService)
public class UserServiceImpl implements UserService {
    @Override
    public List<UserAddress> getUserAddressList(String userId){
        UserAddress address1 = new UserAddress(1,"北京","1","beijing","1234567891","Y");
        UserAddress address2 = new UserAddress(1,"上海","2","shanghai","1234567892","N");
        return Arrays.asList(address2,address1);
    }
}
```

```
// MainApplication：加载 Spring 配置
public class MainApplication {
    public static void main(String[] args) throws IOException {
        ClassPathXmlApplicationContext ioc = new ClassPathXmlApplicationContext("provider.xml");
        ioc.start();
        System.in.read();
    }
}
```
```
// pom.xml 
// 引入dubbo依赖
// 因为注册中心使用的是zookeeper，所以引入zookeeper依赖
// 引入gmall-interface依赖（使用bean和接口）
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>gmall-test-test</artifactId>
        <groupId>com.sangyu</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.sangyu</groupId>
    <artifactId>user-service-provider</artifactId>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.6</source>
                    <target>1.6</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>com.sangyu</groupId>
            <artifactId>gmall-interface</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <!-- 引入dubbo -->
        <!-- https://mvnrepository.com/artifact/com.alibaba/dubbo -->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>dubbo</artifactId>
            <version>2.6.2</version>
        </dependency>
        <!-- 注册中心使用的是zookeeper，引入操作zookeeper的客户端-->
        <dependency>
            <groupId>org.apache.curator</groupId>
            <artifactId>curator-framework</artifactId>
            <version>2.12.0</version>
        </dependency>
    </dependencies>
</project>
```

```
// provider.xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
       xsi:schemaLocation="http://www.springframework.org/schema/beans        http://www.springframework.org/schema/beans/spring-beans-4.3.xsd        http://dubbo.apache.org/schema/dubbo        http://dubbo.apache.org/schema/dubbo/dubbo.xsd">

    <!-- 提供方应用信息，用于计算依赖关系 -->
    <dubbo:application name="user-service-provider"  />

    <!-- 使用multicast广播注册中心暴露服务地址 -->
    <dubbo:registry address="zookeeper://127.0.0.1:2181" />

    <!-- 用dubbo协议在20880端口暴露服务 -->
    <dubbo:protocol name="dubbo" port="20880" />

    <!-- 声明需要暴露的服务接口 -->
    <dubbo:service interface="com.sangyu.gmall.service.UserService" ref="UserServiceImpl" />

    <!-- 和本地bean一样实现服务 -->
    <bean id="UserServiceImpl" class="com.sangyu.gmall.service.impl.UserServiceImpl" />
</beans>

```
**创建服务消费者**

创建module过程和服务提供者不同，在gmall项目下创建module，并ArtifactId设置为order-service-consumer

目录结构

![](https://upload-images.jianshu.io/upload_images/2765653-f0401782c769e9a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**order-service-consumer订单模块：调用用户模块**

OrderServiceImpl：服务方提供实现接口(UserService)
consumer.xml：用 Spring 配置声明暴露服务
MainApplication：加载 Spring 配置

代码

```
// OrderServiceImpl：服务方提供实现接口(UserService)
@Service // 使用spring的注解将OrderServiceImpl注入到容器中
public class OrderServiceImpl implements OrderService {

    @Autowired //使用Autowired将UserService注入进来，UserService已经在consumer.xml配置后已经在容器中了
    UserService userService;

    @Override
    public void initOrder(String userId) {
        System.out.println("用户id：" + userId);

        List<UserAddress> addressList = userService.getUserAddressList(userId);

        for (UserAddress userAddress : addressList) {
            System.out.println(userAddress.getUserAddress());
        }

    }
}

```

```
// MainApplication：加载 Spring 配置
public class MainApplication {
    @SuppressWarnings("resource")
    public static void main(String[] args) throws IOException {
        ClassPathXmlApplicationContext applicationContext =new ClassPathXmlApplicationContext("consumer.xml");
        OrderService orderService = applicationContext.getBean(OrderService.class);
        orderService.initOrder("1");
        System.out.println("调用完成");
        System.in.read();
    }
}
```
```
// consumer.xml：用 Spring 配置声明暴露服务
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:dubbo="http://dubbo.apache.org/schema/dubbo"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd
		http://dubbo.apache.org/schema/dubbo http://dubbo.apache.org/schema/dubbo/dubbo.xsd
		http://code.alibabatech.com/schema/dubbo http://code.alibabatech.com/schema/dubbo/dubbo.xsd">
    <context:component-scan base-package="com.sangyu.gmall.service.impl"></context:component-scan>

    <!-- 消费方应用名，用于计算依赖关系，不是匹配条件，不要与提供方一样 -->
    <dubbo:application name="order-service-consumer"  />

    <!-- 使用zookeeper广播注册中心暴露发现服务地址 -->
    <dubbo:registry address="zookeeper://127.0.0.1:2181" />

    <!--声明需要调用的远程服务的接口；生成远程服务代理  -->
    <dubbo:reference id="UserService" interface="com.sangyu.gmall.service.UserService" />
</beans>
```

```
// pom.xml
// 引入dubbo依赖
// 因为注册中心使用的是zookeeper，所以引入zookeeper依赖
// 引入gmall-interface依赖（使用bean和接口）
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <artifactId>gmall-test-test</artifactId>
        <groupId>com.sangyu</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.sangyu</groupId>
    <artifactId>order-service-consumer</artifactId>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.6</source>
                    <target>1.6</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>com.sangyu</groupId>
            <artifactId>gmall-interface</artifactId>
            <version>1.0-SNAPSHOT</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>dubbo</artifactId>
            <version>2.6.2</version>
        </dependency>
        <dependency>
            <groupId>org.apache.curator</groupId>
            <artifactId>curator-framework</artifactId>
            <version>2.12.0</version>
        </dependency>
    </dependencies>
</project>

```
**创建公共接口层**

创建module过程和服务提供者不同，在gmall项目下创建module，并ArtifactId设置为gmall-interface，提供javabean和服务接口

作用：定义公共接口，也可以导入公共依赖

目录结构
![](https://upload-images.jianshu.io/upload_images/2765653-bddc6266e43f229a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

代码
```
// UserAddress类(javabean)
public class UserAddress {
    private Integer id;
    private String userAddress; // 用户地址
    private String userId; // 用户id
    private String consignee; // 收货人
    private String phoneNum; // 电话号码
    private String isDefault; // 是否为默认地址 Y-是 N-否
    public UserAddress() {
        super();
    }
    public UserAddress(Integer id, String userAddress, String userId, String consignee,
                       String phoneNum, String isDefault) {
        this.id = id;
        this.userAddress = userAddress;
        this.userId = userId;
        this.consignee = consignee;
        this.phoneNum = phoneNum;
        this.isDefault = isDefault;
    }
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getUserAddress() {
        return userAddress;
    }
    public void setUserAddress(String userAddress) {
        this.userAddress = userAddress;
    }
    public String getUserId() {
        return userId;
    }
    public void setUserId(String userId) {
        this.userId = userId;
    }
    public String getConsignee() {
        return consignee;
    }

    public void setConsignee(String consignee) {
        this.consignee = consignee;
    }
    public String getPhoneNum() {
        return phoneNum;
    }
    public void setPhoneNum(String phoneNum) {
        this.phoneNum = phoneNum;
    }
    public String getIsDefault() {
        return isDefault;
    }
    public void setIsDefault(String isDefault) {
        this.isDefault = isDefault;
    }
}
```

```
// 用户服务接口
public interface UserService {
    /**
     * 按照用户id返回所有的收获地址
     * @param userId
     * @return
     */
    public List<UserAddress> getUserAddressList(String userId);
}
```

```
// OrderService接口初始化订单
public interface OrderService {

    /**
     * 初始化订单
     * @param userId
     */
    public void initOrder(String userId);
}
```

**测试运行**

先运行服务提供者user-service-provider，再运行服务调用者order-service-provider，两者运行前要的保证zookeeper是运行状态

```
// 运行结果
用户id：1
上海
北京
调用完成
```

## 十二、Dubbo安装监控中心-Dubbo-Monitor-simple

[下载地址：incubator-dubbo-ops-master-master](https://github.com/locationbai/incubator-dubbo-ops-master)


1. 下载后解压缩，使用命令行窗口进入incubator-dubbo-ops-master-master文件夹，打开dubbo-monitor-simple，执行命令

 ```
mvn package
```

2. 进入/incubator-dubbo-ops-master-master/dubbo-monitor-simple/target，查看dubbo-monitor-simple-2.0.0.jar，这是打包成功的jar包，除此之外还有dubbo-monitor-simple-2.0.0-assembly.tar.gz，这是同时打的一个压缩包，解压到当前文件夹

![](https://upload-images.jianshu.io/upload_images/2765653-0154f14788f7c35d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


3. 进入解压缩后的文件夹：/dubbo-monitor-simple-2.0.0/conf/dubbo.properties

![](https://upload-images.jianshu.io/upload_images/2765653-05cdcec636b3b7d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

dubbo.registry.address: 注册中心的地址及端口号
dubbo.protocol.port：与其他服务与监控中心通信的端口号
dubbo.jetty.port：监控中心web页面的访问端口号

4. 启动监控中心，使用命令行窗口进入/dubbo-monitor-simple-2.0.0/assembly.bin目录下，执行命令

```
./start.sh start  // 启动服务
./stop.sh stop  // 关闭服务
```

5. 启动成功后，[打开链接](http://localhost:8080/)

![](https://upload-images.jianshu.io/upload_images/2765653-bd8bb8fc27be5c12.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6. 服务消费者的修改consumer.xml配置

```
// 增加监控中心配置
// 监控中心协议，如果为protocol="registry"，表示从注册中心发现监控中心地址，否则直连监控中心。
<dubbo:monitor protocol="registry"></dubbo:monitor>
```

7. 服务提供者的修改provider.xml配置
```
// 增加监控中心配置
// 监控中心协议，如果为protocol="registry"，表示从注册中心发现监控中心地址，否则直连监控中心。
<dubbo:monitor protocol="registry"></dubbo:monitor>
```

8. 重新运行服务提供者和服务消费者，[打开链接](http://localhost:8080/) ，整合springboot后可以通过Statistics和Charts查看调用的情况包括调用信息和调用统计图

![](https://upload-images.jianshu.io/upload_images/2765653-8f0e65c41742e470.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 十三、Dubbo与SpringBoot整合

**创建服务的提供者**

1. 还是在gmall下新建module工程

![](https://upload-images.jianshu.io/upload_images/2765653-6d1e9348ec408b7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. Group和gmall的相同，Artifact如图所示，完成后next

![](https://upload-images.jianshu.io/upload_images/2765653-9d90dbbde22b28b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


3. 直接next

![](https://upload-images.jianshu.io/upload_images/2765653-4d352d55f2ef756d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. 直接finish

![](https://upload-images.jianshu.io/upload_images/2765653-41dff18d4a13b4d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.复制UserServiceImpl的实现到boot-user-service-provider下
并修改pom.xml配置

目录结构
![](https://upload-images.jianshu.io/upload_images/2765653-cf33ce29ae1b158a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
// pom.xml
// 注入gmall-interface依赖
// 注入dubbo-spring-boot-starter依赖
<dependency>
	<groupId>com.sangyu</groupId>
	<artifactId>gmall-interface</artifactId>
	<version>1.0-SNAPSHOT</version>
</dependency>
 <dependency>
	<groupId>com.alibaba.boot</groupId>
	<artifactId>dubbo-spring-boot-starter</artifactId>
	<version>0.2.0</version>
</dependency>
```

```
// UserServiceImpl类
@Service // 使用dubbo提供的用于暴露服务
@Component
public class UserServiceImpl implements UserService {
    @Override
    public List<UserAddress> getUserAddressList(String userId){
        UserAddress address1 = new UserAddress(1,"北京","1","beijing","1234567891","Y");
        UserAddress address2 = new UserAddress(1,"上海","2","shanghai","1234567892","N");
        return Arrays.asList(address2,address1);
    }
}
```

```
// BootUserServiceProviderApplication类
@EnableDubbo // 开启基于注解的dubbo功能
@SpringBootApplication
public class BootUserServiceProviderApplication {
	public static void main(String[] args) {
      SpringApplication.run(BootUserServiceProviderApplication.class, args);
	}
}
```

```
// application.properties
dubbo.application.name=user-service-provider
dubbo.registry.address=127.0.0.1:2181
dubbo.registry.protocol=zookeeper
dubbo.protocol.name=dubbo
dubbo.protocol.port=20880
dubbo.monitor.protocol=registry
```
**创建服务的消费者**

1. 还是在gmall下新建module工程

![](https://upload-images.jianshu.io/upload_images/2765653-6d1e9348ec408b7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2. Group和gmall的相同，Artifact如图所示，完成后next

![](https://upload-images.jianshu.io/upload_images/2765653-9d90dbbde22b28b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 选择web，next

![](https://upload-images.jianshu.io/upload_images/2765653-07873b6a6d06d96f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4. 直接finish

![](https://upload-images.jianshu.io/upload_images/2765653-41dff18d4a13b4d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.复制OrderServiceImpl的实现到boot-order-service-consumer下
并修改pom.xml配置

目录结构
![](https://upload-images.jianshu.io/upload_images/2765653-42531c18a933bde2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
// pom.xml
// 注入gmall-interface依赖
// 注入dubbo-spring-boot-starter依赖
<dependency>
	<groupId>com.sangyu</groupId>
	<artifactId>gmall-interface</artifactId>
	<version>1.0-SNAPSHOT</version>
</dependency>
 <dependency>
	<groupId>com.alibaba.boot</groupId>
	<artifactId>dubbo-spring-boot-starter</artifactId>
	<version>0.2.0</version>
</dependency>
```

```
// OrderServiceImpl类
@Service
public class OrderServiceImpl implements OrderService {
    @Reference
    UserService userService;
    @Override
    public List<UserAddress> initOrder(String userId) {
        System.out.println("用户id：" + userId);
        List<UserAddress> addressList = userService.getUserAddressList(userId);
        return addressList;
    }
}
```

```
// BootOrderServiceConsumer01Application类
@EnableDubbo
@SpringBootApplication
public class BootOrderServiceConsumer01Application {
	public static void main(String[] args) {
		SpringApplication.run(BootOrderServiceConsumer01Application.class, args);
	}
}
```

```
// application.properties
server.port=8081
dubbo.application.name=boot-order-service-consumer
dubbo.registry.address=zookeeper://127.0.0.1:2181
dubbo.monitor.protocol=registry
```

```
// OrderController类
@Controller
public class OrderController {
    @Autowired
    OrderService orderService;
    @ResponseBody
    @RequestMapping("/initOrder")
    public List<UserAddress> initOrder(@RequestParam("uid") String userId){
        return orderService.initOrder(userId);
    }
}
```

6. 分别运行服务提供者和服务消费者，[打开链接访问](http://localhost:8081/initOrder?uid=1)

![](https://upload-images.jianshu.io/upload_images/2765653-149ab09a6625dc4b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

7. [监控中心](http://localhost:8080/)查看访问次数和调用统计图


![Statistics-访问次数](https://upload-images.jianshu.io/upload_images/2765653-5f3ddef9d2aa14ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![Charts-调用统计图](https://upload-images.jianshu.io/upload_images/2765653-2cd738c3d06667c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

