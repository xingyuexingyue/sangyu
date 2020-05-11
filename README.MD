## 语言选择

目前大多数公司的开发语言都是 Java，推荐选择 Java

- [ ] Java
- [ ] Python

以下语言要简单掌握语法：

- [ ] JS
- [ ] H5/Bootstrap

## 数据结构

- 数组
    - 数组是一种效率最高的存储和随机访问对象引用序列的方式
        - [ ] [ ]  —— 访问数组中的元素
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
    - [ ] [使用数组实现栈（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=30)

- 队列
    - [ ] 先进先出
    - [ ] [使用数组实现队列（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=10)
        - enqueue(value) —— 在可容的情况下添加元素到尾部
        - dequeue() —— 删除最早添加的元素并返回其值
        - empty()
        - full()
    - [ ] [使用数组实现环形队列](https://www.bilibili.com/video/BV16t411g7wa?p=10)
        

- 链表
    - [ ] [单链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=16) 
    - [ ] [双向链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=24)
    - [ ] [环形链表实现（视频）](https://www.bilibili.com/video/BV16t411g7wa?p=27)
    
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

- 树
    - [ ] 遍历
    - [ ] 中序遍历（DFS：左、节点本身、右）
    - [ ] 后序遍历（DFS：左、右、节点本身）
    - [ ] 先序遍历（DFS：节点本身、左、右）

## 排序

- 实现各种排序 & 知道每种排序的最坏、最好和平均的复杂度分别是什么场景:
- 不要用冒泡排序 
    - [ ] 选择排序 
    - [ ] 冒泡排序
    - [ ] 插入排序
    - [ ] 快排
    - [ ] 归并排序 
    - [ ] 希尔排序

## 其他知识

- 递归（Recursion）
    - 常见题目
        - [ ] 计算阶乘
        - [ ] 斐波拉契数列
    - [ ] 尾递归
    
- 进程（Processe）和线程（Thread）
    - 进程和线程的区别是什么?
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
    - 常见的设计模式
        - [ ] 线程安全的单例模式(双检查)
        - [ ] 工厂模式
        - [ ] 适配器
        - [ ] 桥接
        - [ ] 策略
        - [ ] 模板方法


- 其他
    - [ ] Linux 常见命令
    - [ ] 常用sql
    - [ ] 事务
    - [ ] 线程池
    - [ ] 乐观锁
    - [ ] 悲观锁
    - [ ] git常用命令
    - [ ] redis 常用命令
    - [ ] es常用命令


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
    
- 要掌握的开发技术栈
    - [ ] 一个完整的CURD项目 [](https://github.com/xingyuexingyue/SSM-CURD)
        - 使用的技术点
            - Java语言：：spring+springmvc+mybaits+bootstrap+mysql
            - python语言：Django+bootstrap+mysql

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
    
        