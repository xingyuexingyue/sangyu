## Java 基础 

- Java 容器
    - [ ] Collection 接口，List、Set、Queue 的最基本的接口
    - [ ] Iterator 迭代器 实现迭代器遍历集合中的元素 [代码位置]()
    - [ ] Map 映射表的基础接口

    - java.util.Collections
        - [ ] fill() 填充容器，只能条换不能添加新元素 [代码位置]()
        - [ ] nCopies() 填充容器 [代码位置]()
        
    - java.util.Collection [代码位置]()
        - [ ] add() 添加元素
        - [ ] addAll() 添加全部元素
        - [ ] contains() 判断容器中是否存在某元素
        - [ ] containsAll() 判断容器中是否包含另一个容器中的所有元素
        - [ ] isEmpty() 判断是否包含元素
        - [ ] iterator() 返回一个Iterator对象，遍历容器中的元素
        - [ ] remove() 移除元素
        - [ ] removeAll() 移除所有元素
        - [ ] clear() 移除所有元素
        - [ ] size() 长度
        - [ ] toArray() 返回一个数组
        
    - Map [代码位置]()
        - [ ] size()
        - [ ] isEmpty()
        - [ ] containsKey(Object key)
        - [ ] containsValue(Object value)
        - [ ] get(Object key)
        - [ ] put(K key, V value)
        - [ ] remove(Object key)
        - [ ] putAll(Map<? extends K, ? extends V> m)
        - [ ] clear()
        - [ ] keySet()
        - [ ] Collection<V> values()
        - [ ] Set<Map.Entry<K, V>> entrySet()       
        
    - 其他 
        - [ ] for 和 foreach 区别 [代码位置]()
        - [ ] equals 和 == 区别 [代码位置]()

- Java 并发
    - 线程的创建方式 
        - [ ] 继承 Thread 类 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/00-%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F.md#%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F%E7%AC%AC%E4%B8%80%E7%A7%8D%E7%BB%A7%E6%89%BF-thread-%E7%B1%BB)
        - [ ] 实现 Runnable 接口 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/00-%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F.md#%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F%E7%AC%AC%E4%BA%8C%E7%A7%8D%E5%AE%9E%E7%8E%B0-runnable-%E6%8E%A5%E5%8F%A3)
        - [ ] 实现 Callable 接口 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/00-%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F.md#%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F%E7%AC%AC%E4%B8%89%E7%A7%8D%E5%AE%9E%E7%8E%B0-callable-%E6%8E%A5%E5%8F%A3-%E6%9C%89%E8%BF%94%E5%9B%9E%E5%80%BC)
        - [ ] 线程池的方式 ExecutorService [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/00-%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F.md#%E7%BA%BF%E7%A8%8B%E5%88%9B%E5%BB%BA%E6%96%B9%E5%BC%8F%E7%AC%AC%E5%9B%9B%E7%A7%8D%E7%BA%BF%E7%A8%8B%E6%B1%A0%E7%9A%84%E6%96%B9%E5%BC%8F-executorservice)
            - newCachedThreadPool \ newFixedThreadPool \ newScheduledThreadPool \ newSingleThreadExecutor 
    - 线程生命周期 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/1-%E5%B9%B6%E5%8F%91/022-%E7%BA%BF%E7%A8%8B%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.md)
        - [ ] 新建状态（ new ）
        - [ ] 就绪状态 ( Runnable ）
        - [ ] 运行状态（ Running ）
        - [ ] 阻塞状态（ Blocked ）
        - [ ] 线程死亡（ Dead )
    - 线程的优先级 [代码位置]()
    - 其他
        - [ ] 为某个对象加锁
        - [ ] this 加锁
        - [ ] 执行代码的时候锁定当前对象
        - [ ] 锁定静态方法
        - [ ] 线程重入的问题
        - [ ] 同步方法和非同步方法是否可以同时调用
        - [ ] 对业务方法加锁
        - [ ] 子类调用父类的同步方法
        - [ ] 出现异常时，锁释放
        - [ ] volatile
        - [ ] 使用 synchronized 和 volatile 的区别
        - [ ] 使用 synchronized 解决 上面的问题
        - [ ] 使用 AtomXXX 类
        - [ ] 避免将锁定对象改为另一个对象
        - [ ] 不要以字符串作为锁的对象
        - [ ] 曾经的面试题
        - [ ] 使用 wait 和 notify
        - [ ] 使用 await 和 countdown
        
- Java 异常
    - [ ] Throwable、Error、Exception、RuntimeException
    - [ ] Throw 和 throws 的区别
    
- [ ] Java 反射

- Java 复制
    - [ ] 直接赋值复制
    - [ ] 浅拷贝
    - [ ] 深拷贝
    
    
## 常见问题汇总

- Java 并发

    - [ ] 线程创建方式
    - [ ] 为某个对象加锁
    - [ ] this 加锁
    - [ ] 执行代码的时候锁定当前对象
    - [ ] 锁定静态方法
    - [ ] 线程重入的问题
    - [ ] 同步方法和非同步方法是否可以同时调用
    - [ ] 对业务方法加锁
    - [ ] 一个同步方法是不是可以调用另一个同步方法
    - [ ] 子类调用父类的同步方法
    - [ ] 出现异常时，锁释放
    - [ ] volatile
    - [ ] 使用 synchronized 和 volatile 的区别
    - [ ] 使用 synchronized 解决上面的的问题
    - [ ] 使用 AtomXXX 类
    - [ ] synchronized 优化
    - [ ] 避免将锁定对象改为另一个对象
    - [ ] 不要以字符串作为锁的对象
    - [ ] 曾经的面试题
    - [ ] 使用 wait 和 notify 
    - [ ] 使用 await 和 countdown 
    - [ ] 设置线程优先级
    - [ ] 线程的生命周期 
      
## 数据结构

- 数组
    - 数组是一种效率最高的存储和随机访问对象引用序列的方式
    - [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/015-%E6%95%B0%E7%BB%84.md)
        - [ ] 数组初始化
        - [ ] [ ] —— 访问数组中的元素
        - [ ] length  —— 访问数组的长度（注意是数组的大小，不是实际保存的元素个数）
        - [ ] Arrays.toString() —— 将数组转换为String
        - [ ] Arrays.fill() —— 给数组填充值
        - [ ] Arrays.equals() —— 比较两个数组是否相等；相等的条件是：元素个数必须相等，并且对应位置的元素也相等
        - [ ] Arrays.sort() —— 数组排序
        - [ ] Arrays.binarySearch() —— 在排好序的数组中查找元素
        - [ ] System.arraycopy() —— 复制数组；参数：源数组，从源数组什么位置开始复制，目标数组，从什么位置开始复制，需要复制的个数
        - [ ] Arrays.asList() —— 接收一个数组或是一个用逗号分隔的元素列表（使用可变参数），并将其转为一个List对象    

- 动态数组
    - 实现一个可自动调整大小的动态数组
    - [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/011-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AAArrayList.md)
        - [ ] size() —— 数组元素的个数
        - [ ] capacity() —— 可容纳元素的个数
        - [ ] is_empty()
        - [ ] at(index) —— 返回对应索引的元素，索引越界报错
        - [ ] push(item)
        - [ ] insert(index, item) —— 在指定索引中插入元素，并把后面的元素依次后移
        - [ ] prepend(item) —— 可以使用上面的 insert 函数，传参 index 为 0
        - [ ] pop() —— 删除在数组末端的元素，并返回其值
        - [ ] delete(index) —— 删除指定索引的元素，并把后面的元素依次前移
        - [ ] remove(item) —— 删除指定值的元素，并返回其索引（即使有多个元素）
        - [ ] find(item) —— 寻找指定值的元素并返回其中第一个出现的元素其索引，若未找到则返回 -1
        - [ ] resize(new_capacity) // 私有函数
            - 若数组的大小到达其容积，则变大一倍
            - 获取元素后，若数组大小为其容积的1/4，则缩小一半
- 栈 
    - [ ] 先进后出 
    - [ ] [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/08-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E6%A0%88.md)

- 队列
    - [ ] 先进先出 有序
    - [ ] 普通队列 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/012-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E9%98%9F%E5%88%97.md)     
        - enqueue(value) —— 在可容的情况下添加元素到尾部
        - dequeue() —— 删除最早添加的元素并返回其值
        - empty()
        - full()
    - [ ] 环形队列 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/012-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E9%98%9F%E5%88%97.md#%E5%AE%9E%E7%8E%B0%E7%8E%AF%E5%BD%A2%E9%98%9F%E5%88%97)
        

- 链表
    - 特点：新增和删除更加高效
    - 单向链表 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md) 
    - 统计单链表中有效节点的个数 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md#%E7%BB%9F%E8%AE%A1%E5%8D%95%E9%93%BE%E8%A1%A8%E4%B8%AD%E6%9C%89%E6%95%88%E8%8A%82%E7%82%B9%E7%9A%84%E4%B8%AA%E6%95%B0)
    - 查找单链表中的倒数第k个节点[代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md#%E6%9F%A5%E6%89%BE%E5%8D%95%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACk%E4%B8%AA%E8%8A%82%E7%82%B9sina)
    - 单链表的反转 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md#%E5%8D%95%E9%93%BE%E8%A1%A8%E7%9A%84%E5%8F%8D%E8%BD%ACtencent)
    - 从尾到头打印单链表 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/09-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8D%95%E5%90%91%E9%93%BE%E8%A1%A8.md#%E4%BB%8E%E5%B0%BE%E5%88%B0%E5%A4%B4%E6%89%93%E5%8D%B0%E5%8D%95%E9%93%BE%E8%A1%A8baidu)
    - 双向链表 [代码位置](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/010-%E6%89%8B%E5%8A%A8%E5%AE%9E%E7%8E%B0%E4%B8%80%E4%B8%AA%E5%8F%8C%E5%90%91%E9%93%BE%E8%A1%A8.md)

- 哈希表
    - [ ] 创建 HashMap 对象 `HashMap<String,Integer> hashMap = new HashMap<>();`
    - [ ] 添加键值对 `hashMap.put("a",1);` 
    - [ ] 删除键值对 `hashMap.remove("a",5);`
    - [ ] 获取key 的 value `hashMap.get("cc");`
    - [ ] 判断 key 是否存在 `hashMap.containsKey("bb")'
    - [ ] 获得 key 的集合 `hashMap.keySet()`
    - [ ] 获得 key-value 的集合 `hashMap.entrySet();`
    - [ ] 替换 key 的 value `hashMap.replace("ff".5);`
    - [ ] [元素遍历](https://github.com/xingyuexingyue/sangyu/blob/master/study/Java/3-%E5%AE%B9%E5%99%A8%E7%B1%BB/015-HashMap.md)   

## 排序

- 实现各种排序 & 知道每种排序的最坏、最好和平均的复杂度分别是什么场景:
- 不要用冒泡排序 
    - [ ] 选择排序 [代码位置]()
    - [ ] 冒泡排序 [代码位置]()
    - [ ] 插入排序 [代码位置]()
    - [ ] 希尔排序 [代码位置]()
    - [ ] 归并排序 [代码位置]()
    - [ ] 快排 [代码位置]()




## 其他知识

- 递归（Recursion）
    - 常见题目
        - [ ] 计算阶乘 [代码位置]()
        - [ ] 斐波拉契数列 [代码位置]()
        - [ ] 爬楼梯 [代码位置]()
    - [ ] 尾递归
    
- 进程（Processe）和线程（Thread）
    - 进程和线程的区别是什么?
    - 进程资源需要（内存：代码、静态存储器、栈、堆、文件描述符、I/O）
    - 线程资源需要（在同一个进程内和其他线程共享以上的资源，但是每个线程都有独立的程序计数器、栈计数器、寄存器和栈）
    - Fork 操作是真正的写时复制（只读），直到新的进程写到内存中，才会生成一份新的拷贝。

- TCP / IP 
    - [ ] 分层：应用层、传输层 、网络层、网络接口层   
    - [ ] TCP 三次握手
    - [ ] TCP 四次挥手
    
- HTTP 原理
    - [ ] 无状态协议，指的是浏览器和服务器之间不需要建立持久的连接，这意味着客户端向服务端发出请求后，然后服务器响应，连接就关闭了，在服务器端不会保留连接的有关信息，所有 HTTP 连接都被构造成一套请求和应答
    - [ ] 传输流程
    - [ ] HTTP 状态码
    - [ ] HTTPS 安全的 HTTP 通道，加入了 SSL 层，端口号 443
       
- CDN       

- 设计模式
    - 面向对象编程的 SOLID 原则:
        - [ ] 单一职责原则 | 每个对象的单一职责
        - [ ] 开闭原则 | 生产环境里的对象应该为扩展做准备而不是为更改
        - [ ] 里氏代换原则 | 基类和继承类遵循 ‘IS A’ 原则
        - [ ] 接口隔离原则 | 客户端被迫实现用不到的接口
        - [ ] 依赖反转原则 | 减少对象里的依赖。
    - 常见的设计模式
        - [ ] 线程安全的单例模式(双检查)
        - [ ] 工厂模式
        - [ ] 适配器
        - [ ] 桥接
        - [ ] 策略
        - [ ] 模板方法
- 微服务        
    - 服务注册发现
        - [ ] 服务注册就是维护一个登记簿，管理系统内所有的服务地址。新的服务启动后，向注册中心推送自己的地址信息。依赖方连接注册中心订阅需要的服务，根据注册中心提供的地址访问
        - [ ] zookeeper 客户端注册 服务自身负责注册和注销，服务启动时向注册中心注册自己，服务下线时注销自己。期间还需要和注册中心保持心跳


- API 网关
    - API Gateway 是一个服务器，进入系统的唯一节点。封装内部系统的架构，并且提供 API 给各个客户端
    - 负责请求转发、合成和协议转换。所有来自客户端的请求都要先经过 API Gateway，然后路由这些请求到对应的微服务
    - API Gateway 将经常通过调用多个微服务来处理一个请求以及聚合多个服务的结果 

- 数据库
    - [ ] 存储引擎 数据库存储引擎是数据库底层软件组织，数据库管理系统使用数据引擎增删改查，不同的存储引擎提供不同的存储机制、索引技巧、索引水平等功能
    - [ ] InnoDB（B+树）
        - 适用场景：经常更新的表，适合处理多重并发的更新请求、支持事务、可以从灾难中恢复（bin-log日志）、外键约束、支持字段自增
    - [ ] 索引原则
    - [ ] 数据库三范式（建表）
    - [ ] 事务
        
        
- [ ] Linux 常见命令
- [ ] 常用sql
- [ ] git常用命令
- [ ] redis 常用命令
- [ ] es常用命令

## Spring 原理

- [ ] 常用注解
    - [ ] @Controller 标注控制层组件 分发处理器将会扫描使用了这个注解的类里的方法，并检测方法是否使用了@RequestMapping注解
    - [ ] @RestController @Controller 和 @responseBody 组合
    - [ ] @Component 通用组件，表示这个类被 Spring 管理
    - [ ] @Repository  注解 dao 层
    - [ ] @Service 标注业务服务层组件
    - [ ] @responseBody  将@Controller 方法返回的对象，通过 HttpMessageConverter 转换为指定格式，写入到 Response 对象的 body 数据区，一般类型为 json 或  xml 等
    - [ ] @RequestMapping 用于类和方法，用于类时表示所有请求的父路径
    - [ ] @Autowired 自动装配注入某个类
    - [ ] @PathVariable  从路径中获得参数
    - [ ] @requestParam 定义参数
    - [ ] @RequestHeader 获得请求头
    - [ ] @SessionAttributes 将值写到 session 作用域中
    - [ ] @Valid 实体数据校验，可以结合 hibernate validator 一起使用
    - [ ] @CookieValue 用来获取Cookie中的值
 
- Spring 第三方框架集成
    - [ ] shiro 认证
    - [ ] redis 缓存
    - [ ] Mybatis 持久
    - [ ] Spring-Task 定时任务
    - [ ] hibernate validator 校验框架
    
- Spring IOC 原理

## MyBatis 

- 知识点
    - [ ] #{} 和 ${} 的区别是什么？ 
    - [ ] 实体类中的属性名和表中字段名不一样
    - [ ] 模糊查询 like 语句该怎么写
    - [ ] Mapper 接口的工作原理
    - [ ] Mapper 接口的方法参数不同时方法是否能重载
    - [ ] Mybatis 是如何将 sql 执行结果封装为目标对象并返回的？都有哪些映射方式？
    - [ ] 如何执行批量插入
    - [ ] 如何获取自动生成的主键值
    - [ ] 在 mapper 中如何传递多个参数
    - [ ] Mybatis 动态 sql 有什么用？执行原理？有哪些动态 sql
    - [ ] xml 映射文件中，除了常见的slect | insert | update | delete 标签之外，还有哪些标签？
    - [ ] Mybatis 的 xml 映射文件中，不同的 xml 映射文件，id 是否可以重复？
    - [ ] 一对一、一对多的关联查询？
    - [ ] MyBatis 实现一对一有几种方式？具体怎么操作？
    - [ ] Mybatis 实现一对多有几种方式，怎么操作的？
    - [ ] 使用 MyBatis 的 mapper 接口调用时有哪些要求？
    - [ ] Mapper 接口绑定
    
        
    
        
        
## 测试相关的知识

- 测试包含点
    - [通过举例说明（文章）](https://github.com/xingyuexingyue/xingyue/blob/master/%E6%B5%8B%E8%AF%95%E7%9F%A5%E8%AF%86%E5%9F%BA%E7%A1%80/%E6%B5%8B%E8%AF%95%E5%AE%9E%E4%BE%8B.md#%E5%8A%9F%E8%83%BD%E6%80%A7%E6%B5%8B%E8%AF%95)
    - [ ] 界面测试 
    - [ ] 用户易用性测试
    - [ ] 功能性测试
    - [ ] 兼容测试率
    - [ ] 压力测试
    - [ ] 性能测试
    - [ ] APP新老版本兼容
- 测试流程有哪些
    - [ ] 1.需求评审
    - [ ] 2.需求评审后集中有问题的地方与产品私下后交流
    - [ ] 3.用例编写
        - 功能测试用例（由测试人员编写及执行，区分不同的优先级，执行的时候优先高优先级）
        - 冒烟测试（由开发人员编写及执行，在提测前执行） 
        - 接口测试用例（编写代码，由测试人员编写及执行，在功能测试前执行）
    - [ ] 4.提测后
        - 首轮用例执行（提交bug，并处理修改后的bug）
        - 二轮测试（针对重要的功能、重要的业务流程、及有bug的地方、一轮因为有bug没有执行的用例再次执行）
        - 三轮测试 (回归老的功能、兼容性测试、针对新功能的重要的功能、流程，整体重要的业务流程)
    - [ ] 5.上线前checklist
    - [ ] 6.上线
        - 通知开发上线，先上预环境（先上后端再上前端）（上线后对新老功能进行回归）
        - 通知开发上正式线上（上线后对新老功能回归、最好有回归的checklist，需要用外网）
- 如何开展一个性能测试
    - [ ] [JMeter实现多用户并发功能测试(文章)](https://github.com/xingyuexingyue/xingyue/blob/master/%E5%B7%A5%E5%85%B7/Jmeter.md)

- 一些工具
    - charles 
        - [ ] [charles(文章)](https://github.com/xingyuexingyue/xingyue/blob/master/%E5%B7%A5%E5%85%B7/Charles.md)
        - 常用到的用法
            - [ ] BreakPoints修改请求参数和响应数据
            - [ ] 映射远程地址 Map Remote
            - [ ] Throttle Setting修改网络连接
            - [ ] SSL Proxying 抓包HTTPS
            - [ ] Edit 修改请求内容
            - [ ] Map Local 接口重定向
            - [ ] 是将某个网络请求重定向到另一个网络请求
    - [ ] fiddler
    - [ ] postman 接口测试工具
    - [ ] swagger 接口管理工具，集成swagger扫描所有controller的url，方便直接通过url测试，返回json
    - [ ] sonar 代码静态扫描工具
    - [ ] Jmeter 性能测试工具
    - [ ] Monkey app随机自动点工具，用来暴力测试，稳定性测试
    - [ ] jenkins 实现持续集成化，可应用到接口，定时执行接口用例，或每次更新代码触发执行

- 接口测试
    - 接口测试的常用方法
    - 测试中会用到一些jar包
        - Java
            - [ ] testng
            - [ ] junnit
            - [ ] springtest
            - [ ] httpClient
        - python
            - [ ] unniest
- 消息队列测试
    - [ ] 被测应用为生产者
    - [ ] 被测应用消费者
    - [ ] 异常场景
            
- 测试中常用到的一些脚本
    - [ ] 快速生成测试数据及管理
    - [ ] 处理文本
    - [ ] 处理excel
    
- 微服务下的测试
    - [ ] mock 
    - [ ] 使用dubbo mock请求方的响应数据  
    
- 练习
    - [ ] 一个完整的CURD项目 [](https://github.com/xingyuexingyue/SSM-CURD)
        - spring+springmvc+mybaits+bootstrap+mysql
       

## 相关课程视频资源

- [ ] [Dubbo ](https://www.bilibili.com/video/av62353311/?pikaqiu)

- [ ] [Spring ](https://www.bilibili.com/video/av59570922/?pikaqiu)

- [ ] [SpringMVC ](https://www.bilibili.com/video/av59567541/?pikaqiu)

- [ ] [SpringBoot ](https://www.bilibili.com/video/av59572480/?pikaqiu)

- [ ] [MyBatis ](https://www.bilibili.com/video/av59564271/?pikaqiu)

- [ ] [rocketmq](https://www.bilibili.com/video/av11074519)

- [ ] [RabbitMQ](https://www.imooc.com/learn/1042)

- [ ] [消息队列 Kafka ]()

- [ ] [Redis入门](https://www.imooc.com/learn/839)

- [ ] [MySQL](https://www.bilibili.com/video/av59623481/?pikaqiu)

- [ ] [Elasticsearch](https://www.bilibili.com/video/av59628430/?pikaqiu)

- [ ] [Git](https://www.bilibili.com/video/av59634634/?pikaqiu)

- [ ] [Nginx](https://www.bilibili.com/video/av59639498/?pikaqiu)

- [ ] [单链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=16) 

- [ ] [双向链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=24)

- [ ] [环形链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=27)
    
- [ ] [使用数组实现队列（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=10)

- [ ] [使用数组实现栈（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=30)   
- [ ] [使用数组实现环形队列](https://www.bilibili.com/video/BV16t411g7wa?p=10)     