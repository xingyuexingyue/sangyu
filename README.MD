## 语言选择

目前大多数公司的开发语言都是Java，推荐选择Java

- [ ] Java
- [ ] Python

以下语言要简单掌握语法：

- [ ] JS
- [ ] 前端

## 相关课程视频资源

- [ ] [Dubbo ](https://www.bilibili.com/video/av62353311/?pikaqiu)

- [ ] [Spring ](https://www.bilibili.com/video/av59570922/?pikaqiu)

- [ ] [SpringMVC ](https://www.bilibili.com/video/av59567541/?pikaqiu)

- [ ] [SpringBoot ](https://www.bilibili.com/video/av59572480/?pikaqiu)

- [ ] [MyBatis ](https://www.bilibili.com/video/av59564271/?pikaqiu)

- [ ] [rocketmq](https://www.bilibili.com/video/av11074519)

- [ ] [RabbitMQ消息中间件](https://www.imooc.com/learn/1042)

- [ ] [消息队列 Kafka ]()

- [ ] [Redis入门](https://www.imooc.com/learn/839)

- [ ] [MySQL](https://www.bilibili.com/video/av59623481/?pikaqiu)

- [ ] [Elasticsearch](https://www.bilibili.com/video/av59628430/?pikaqiu)

- [ ] [Git](https://www.bilibili.com/video/av59634634/?pikaqiu)

- [ ] [Nginx](https://www.bilibili.com/video/av59639498/?pikaqiu)

## 数据结构

- 数组
    - 数组是一种效率最高的存储和随机访问对象引用序列的方式
        - [ ] [ ]  —— 访问数组中的元素
        - [ ] length  —— 访问数组的长度（注意是数组的大小，不是实际保存的元素个数）
        - [ ] Arrays.toString() —— 将数组转换为String
        - [ ] Arrays.deepToString() —— 将多维数组转换为多个String
        - [ ] Arrays.fill() —— 给数组填充值
        - [ ] Arrays.equals() —— 比较两个数组是否相等；相等的条件是：元素个数必须相等，并且对应位置的元素也相等
        - [ ] Arrays.sort() —— 数组排序
        - [ ] Arrays.binarySearch() —— 在排好序的数组中查找元素
        - [ ] System.arraycopy() —— 复制数组；参数：源数组，从源数组什么位置开始复制，目标数组，从什么位置开始复制，需要复制的个数
        - [ ] Arrays.asList() —— 接收一个数组或是一个用逗号分隔的元素列表（使用可变参数），并将其转为一个List对象
        
        

- 动态数组
    - 实现一个可自动调整大小的动态数组
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

- 堆

- 栈 
    - [ ] 先进后出
    - [ ] [使用数组实现栈（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=30)
- 队列
    - [ ] 先进先出
    - [ ] [使用数组实现队列（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=10)
        - enqueue(value) —— 在可容的情况下添加元素到尾部
        - dequeue() —— 删除最早添加的元素并返回其值
        - empty()
        - full()
    - [ ] [使用数组实现环形队列](https://www.bilibili.com/video/BV16t411g7wa?p=10)
        

- [ ] 链表
    - [ ] [单链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=16) 
    - [ ] [双向链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=24)
    - [ ] [环形链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=27)
    
- [ ] 哈希表


## 树（Trees）

- 基本的树形结构
- 遍历
- 操作算法
- BFS（广度优先检索，breadth-first search）
    - 层序遍历（使用队列的 BFS 算法）
    - 时间复杂度： O(n)
    - 空间复杂度：
       - 最好情况： O(1)
       - 最坏情况：O(n/2)=O(n)
- DFS（深度优先检索，depth-first search）
    - 笔记：
    - 时间复杂度：O(n)
    - 空间复杂度：
       - 最好情况：O(log n) - 树的平均高度
       - 最坏情况：O(n)
- 中序遍历（DFS：左、节点本身、右）
- 后序遍历（DFS：左、右、节点本身）
- 先序遍历（DFS：节点本身、左、右）

## 二叉查找树（Binary search trees）：BSTs

- Java
    - [ ] 二叉查找树 —— 在 Java 中实现（视频）
    - [ ] 在二叉查找树中找到最小和最大的元素（视频）
    - [ ] 寻找二叉树的高度（视频）
    - [ ] 二叉树的遍历 —— 广度优先和深度优先策略（视频）
    - [ ] 二叉树：层序遍历（视频）
    - [ ] 二叉树的遍历：先序、中序、后序（视频）
    - [ ] 判断一棵二叉树是否为二叉查找树（视频）
    - [ ] 从二叉查找树中删除一个节点（视频）
    - [ ] 二叉查找树中序遍历的后继者（视频）
    
- 实现
    
    - [ ] insert // 往树上插值
    - [ ] get_node_count // 查找树上的节点数
    - [ ] print_values // 从小到大打印树中节点的值
    - [ ] delete_tree
    - [ ] is_in_tree // 如果值存在于树中则返回 true
    - [ ] get_height // 返回节点所在的高度（如果只有一个节点，那么高度则为1）
    - [ ] get_min // 返回树上的最小值
    - [ ] get_max // 返回树上的最大值
    - [ ] is_binary_search_tree
    - [ ] delete_value
    - [ ] get_successor // 返回给定值的后继者，若没有则返回-1

-  B 树
    - [ ] 实际中：B 树会被广泛适用于数据库中，而现代大多数的文件系统都会使用到这种树（或变种)。除了运用在数据库中，B 树也会被用于文件系统以快速访问一个文件的任意块。但存在着一个基本的问题，那就是如何将文件块 i 转换成一个硬盘块（或一个柱面-磁头-扇区）上的地址。

## 排序

- 笔记:
  - 实现各种排序 & 知道每种排序的最坏、最好和平均的复杂度分别是什么场景:
  - 不要用冒泡排序 - 大多数情况下效率感人 - 时间复杂度 O(n^2), 除非 n <= 16
  
- [ ] 冒泡排序

- [ ] 冒泡排序分析

- [ ] 插入排序

- [ ] 插入排序

- [ ] 归并排序 

- [ ] 快排

- [ ] 选择排序

## 其他知识

- 递归（Recursion）
    - [ ] 尾递归
    
- 进程（Processe）和线程（Thread）
    - 进程和线程的区别是什么?
    - 涵盖了:
        - 进程、线程、协程
        - 进程和线程的区别
        - 进程
        - 线程
        - 锁
        - 互斥
        - 监控
        - 死锁
        - 活锁
    - CPU 活动, 中断, 上下文切换
    - 现代多核处理器的并发式结构
    - 进程资源需要（内存：代码、静态存储器、栈、堆、文件描述符、I/O）
    - 线程资源需要（在同一个进程内和其他线程共享以上的资源，但是每个线程都有独立的程序计数器、栈计数器、寄存器和栈）
    - Fork 操作是真正的写时复制（只读），直到新的进程写到内存中，才会生成一份新的拷贝。

- 设计模式
    - 面向对象编程的 SOLID 原则:
    - [ ] 单一职责原则 | 每个对象的单一职责
    - [ ] 开闭原则 | 生产环境里的对象应该为扩展做准备而不是为更改
    - [ ] 里氏代换原则 | 基类和继承类遵循 ‘IS A’ 原则
    - [ ] 接口隔离原则 | 客户端被迫实现用不到的接口
    - [ ] 依赖反转原则 | 减少对象里的依赖。

## Linux 常见命令

## 常用sql

## 事务

## 线程池

## 乐观锁 

## 悲观锁

## git常用命令

## redis 常用命令

## es常用命令

## 异常
- 异常
    - [ ] 平时中常见的异常，以及如何排查

## HTTP相关
- http
    - [ ] HTTP协议：
    - [ ] 浏览器
    - [ ] Web服务器
    - [ ] CDN
    - [ ] DNS
    - [ ] URI/URL
    - [ ] HTTPS
    - [ ] 代理
    - [ ] TCP/IP
    - [ ] TCP/IP网络分层、TCP三次握手
    - [ ] HTTP与HTTPS的区别
    - [ ] HTTP请求方式和状态码
    - [ ] HTTP请求过程
    - [ ] HTTPS请求过程
    - [ ] HTTP2.0特点
    - [ ] SPDY协议
    - [ ] HTTP1.x的缺点
    - [ ] 为什么连接的时候是三次握手，关闭的时候却是四次握手？
    - [ ] http的长连接和短连接
    - [ ] 长轮询和短轮询
    - [ ] 长短轮询和长短连接的区别
    - [ ] cookie
    - [ ] session
    - [ ] cookie和session的区别


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
    - [ ] Selenium web前端自动化工具
    - [ ] appium app自动化工具
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
    
- 要掌握的开发技术栈
    - [ ] 一个完整的CURD项目 [](https://github.com/xingyuexingyue/SSM-CURD)
        - 使用的技术点
            - Java语言：：spring+springmvc+mybaits+bootstrap+mysql
            - python语言：Django+bootstrap+mysql
            
- 客户端IOS平台特性

- 客户端IOS平台特性

- H5平台特性

- Python
    - [ ] 基础语法
    - [ ] 常用库
        - SQLAlchemy
        - jsonpath
    - [ ] 常用类 


    
        