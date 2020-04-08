## 一、逻辑架构和存储引擎

![](https://upload-images.jianshu.io/upload_images/2765653-a051b969828a3f9f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如上图所示：MySQL服务器逻辑架构从上往下可以分为三层：

（1）第一层：处理客户端连接、授权认证等

（2）第二层：服务器层，负责查询语句的解析、优化、缓存以及内置函数的实现、存储过程等

（2）第三层：存储引擎，负责MySQL中数据的存储和提取。MySQL中服务器层不管理事务，事务是由存储引擎实现的。MySQL支持事务的存储引擎有InnoDB、NDB Cluster等，其中InnoDB的使用最为广泛；其他存储引擎不支持事务，如MyIsam、Memory等。


## 
