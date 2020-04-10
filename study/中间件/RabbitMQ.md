## 一. 消息队列的用途

消息服务中间件可以提升系统异步通信、扩展解耦能力。

#### 异步通信

传统注册流程和使用消息队列比较

第一种：用户注册信息写入数据库后在按照顺序先后发送注册邮件和短信，走完这三步后用户才完成注册

![传统注册流程](https://upload-images.jianshu.io/upload_images/2765653-6b873176e68febfe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

第二种：用户注册消息写入数据库后通过开启线程池的方式，同时发送邮件和注册短信，两个线程完成后返回，用户注册完成

![采用多线程方式](https://upload-images.jianshu.io/upload_images/2765653-44595675b7b462de.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

第三种：用户注册消息写入数据库后将消息写入消息队列，此时发送邮件和发送短信通过异步读取消息队列执行具体的操作，但在写入消息队列之前已经返回给用户，用户注册完成，而发送短信和邮件是异步操作

![消息队列](https://upload-images.jianshu.io/upload_images/2765653-139cabe10b432502.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 应用解耦

传统方式下单后调用库存系统更新商品的剩余库存。采用消息队列方式，可达到应用解耦，下单后订单系统调用mq将消息写入到消息队列，由库存系统订阅消息队列并按照业务逻辑处理对应消息

![传统方式](https://upload-images.jianshu.io/upload_images/2765653-22b87ba5c1aa9615.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![采用消息队列方式](https://upload-images.jianshu.io/upload_images/2765653-88f873a102018d4f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 流量削峰

比如我们有100W用户同时抢100台手机，服务层并发请求压力至少为100W。

既然服务层知道库存只有100台手机，那完全没有必要把100W个请求都传递到数据库啊，那么可以先把这些请求都写到消息队列缓存一下，数据库层订阅消息减库存，减库存成功的请求返回秒杀成功，失败的返回秒杀结束。

![](https://upload-images.jianshu.io/upload_images/2765653-31bc636c311a2552.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 二. 消息队列的两个概念

- 消息代理（message broker）
- 目的地（destination）

当消息发送者发送消息以后，将由消息代理接管，消息代理保证消息传递到指定目的地。

消息队列主要有两种形式的目的地：

1. 队列（queue）：点对点消息通信

    消息发送者发送消息，消息代理将其放入一个队列中，消息接收者从队列中获取消息内容，消息读取后被移除队列，此时消息只有唯一的发送者和接收者，但并不是只能有一个接收者，这种情况下可以存在多个接收者，但一个接收者接收后，其他的就不再处理

2. 主题（topic）：发布(public) / 订阅(subscribe) 消息通信

    订阅式：发送者（发布者）发送消息到主题，多个接收者（订阅者）监听（订阅）这个主题，那么就会在消息到达时同时收到消息

再说下JMS和AMQP，JMS（Java Messge Service） JAVA消息服务是给予JVM消息代理的规范。ActiveMQ、HornetMQ是JMS实现；
AMQP是高级消息队列协议，也是一个消息代理的规范，兼容JMS，RabbitMQ是AMQP的实现，AMQP提供了五种消息模型：direct exchange、fanout exchange、topic exchange、headers exchange、system exchange；

## 三. RabbitMQ

![](https://upload-images.jianshu.io/upload_images/2765653-5185b52910306d9a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- Message
消息，消息是不具名的，它由消息头和消息体组成。消息体是不透明的，而消息头则由一系列的可选属性组成，这些属性包括routing-key（路由键）、priority（相对于其他消息的优先权）、delivery-mode（指出该消息可能需要持久性存储）等

- Publisher
消息的生产者，也是一个向交换器发布消息的客户端应用程序

- Exchange
交换器，用来接收生产者发送的消息并将这些消息路由给服务器中的队列；
Exchange有4种类型：direct（默认）、fanout、topic和headers，不同类型的Exchange转发消息的策略有所区别，direct指的是点对点，fanout、topic和headers指的是订阅

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
虚拟主机，表示一批交换器、消息队列和相关对象。虚拟主机是共享相同的身份认证和加密环境的独立服务器域。每个vhost本质上就是一个mini版的RabbitMQ服务器，拥有自己的队列、交换器、绑定和权限机制。vhost是AMQP概念的基础，必须在连接时指定，RabbitMQ默认的vhost是/

- Broker
表示消息队列服务器实体

#### 3.1 RabbitMQ 运行机制

AMQP中消息的路由过程和Java开发者熟悉的JMS存在一些差别，AMQP中增加了Exchange和Binding的角色。生产者把消息发布到Exchange上，消息最终到达队列并被消费者接收，而Binding决定交换器的消息应该发送到哪个队列上。

![](https://upload-images.jianshu.io/upload_images/2765653-47a135ed46e30333.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Exchange分发消息时类型不同分发策略不同，目前有四种类型：direct、fanout、topic、headers。headers匹配AMQP消息的header而不是路由键，headers交换器和direct交换器完全一致，但性能相差很多，目前几乎用不到了，所以直接看另外三种类型：

1. Direct

![Direct Exchange](https://upload-images.jianshu.io/upload_images/2765653-9591bc418fe83edd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

消息中的路由键如果和Binding中的binding key一致，交换器就将消息发到对应的队列中。路由键与队列名完全匹配，如果一个队列绑定到交换机要求路由键为 “dog”，则交换器只转发“dog”的消息到此消息队列。不会转发“dog.puppy”,也不会转发“dog.guard”等等。direct是完全匹配、单播的模式。

2. Fanout

![Fanout Exchange](https://upload-images.jianshu.io/upload_images/2765653-13363fd86236639e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

每个发到Fanout类型交换器的消息都会分到所有绑定的队列上去。fanout交换器不处理路由键，只是简单的将队列交换器上，每个发送到交换器的消息都会被转发到与该交换器绑定的所有队列上。很像子网广播，每个子网内的主机都获得了一份复制的消息。fanout类型转发消息是最快的

3. topic

![Topic Exchange](https://upload-images.jianshu.io/upload_images/2765653-f681086a9c560ba6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

topic交换器通过模式匹配分配消息的路由键属性，将路由键和某个模式进行匹配，此时队列需要绑定到一个模式上。它将路由键和绑定键的字符串切分为单词，这些单词之间用点个靠。它同样也会识别两个匹配符：符号# 和 符号*，#匹配0个或多个单词，*匹配一个单词

#### 3.2 RabbitMQ 使用

1. docker 安装 RabbitMQ

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

2. 安装成功后，[浏览器直接访问服务器地址](http://localhost:15672) ，默认用户和密码为：guest

![](https://upload-images.jianshu.io/upload_images/2765653-fec881c6f1d3f1fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/2765653-75cb5e7c671041a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 添加交换器，选择Durable持久化的原因是，关闭服务器后交换器还在

添加交换器的步骤
![](https://upload-images.jianshu.io/upload_images/2765653-f542a0de120b9cf3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加direct类型->
![](https://upload-images.jianshu.io/upload_images/2765653-4dc1f10b8f93eb0b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加fanout类型->
![](https://upload-images.jianshu.io/upload_images/2765653-7493ef4b15e26550.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加topic类型->
![](https://upload-images.jianshu.io/upload_images/2765653-01ef22bce23e53a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加的交换器在列表展示->
![添加的交换器在列表展示](https://upload-images.jianshu.io/upload_images/2765653-db0c450a09bde6ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. 添加消息队列 

添加消息队列的步骤
![添加消息队列的步骤](https://upload-images.jianshu.io/upload_images/2765653-14933c52c284bf7c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

添加的消息队列在列表展示
![添加的消息队列在列表展示](https://upload-images.jianshu.io/upload_images/2765653-c954410326974efd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


4. 交换器绑定Binding

交换器添加绑定的步骤
![](https://upload-images.jianshu.io/upload_images/2765653-cd518f6c0a1277f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-966a494c9e2ce538.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

direct交换器 绑定消息队列->
![direct交换器 绑定消息队列](https://upload-images.jianshu.io/upload_images/2765653-d3de912803cf1187.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

fonout交换器 绑定消息队列->
![fonout交换器 绑定消息队列](https://upload-images.jianshu.io/upload_images/2765653-0da5f3a56b2bf0a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

topic交换器 绑定消息队列->
![topic交换器 绑定消息队列](https://upload-images.jianshu.io/upload_images/2765653-e4e4b18dc54c090d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5. 发送消息到交换器

发送到direct交换器，根据绑定时路由键（Routing key）发送到消息队列

![](https://upload-images.jianshu.io/upload_images/2765653-b9534876d9e20d67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![发送消息的步骤](https://upload-images.jianshu.io/upload_images/2765653-0173d0f0cbeba65a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-b2e776a0540b7f29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

6. 查看发送消息结果

![查看发送消息结果](https://upload-images.jianshu.io/upload_images/2765653-667cbfb72697ec80.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

消息队列中get message
![](https://upload-images.jianshu.io/upload_images/2765653-eecb7e28debb72ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-7df01683040702d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

发送到fonout交换器，fonout绑定了所有队列 不管什么路由键是什么都可以接收消息
![](https://upload-images.jianshu.io/upload_images/2765653-d9dd2edb2e405a7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

查看发送消息结果，四个队列都接收到了这条消息
![查看发送消息结果，四个队列都接收到了这条消息](https://upload-images.jianshu.io/upload_images/2765653-9d6aa1c23ed1501f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

任意查看一个队列
![任意查看一个队列](https://upload-images.jianshu.io/upload_images/2765653-4b9b18a25747a28d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


发送到topic交换器，按照路由规则接收消息
![](https://upload-images.jianshu.io/upload_images/2765653-457bb879c5aadc49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4个消息队列都收到了
![4个消息队列都收到了](https://upload-images.jianshu.io/upload_images/2765653-d37872dd465a6ff1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

继续发送一个其他的消息测试
![继续发送一个其他的消息测试](https://upload-images.jianshu.io/upload_images/2765653-d1ae06136b9cd4fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这次只有两个收到了
![这次只有两个收到了](https://upload-images.jianshu.io/upload_images/2765653-d43bb25e0ea1182c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### 3.3 springboot 整合消息队列

选择注入依赖的时候，选择web和rabbitmq
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