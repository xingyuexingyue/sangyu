- encode()方法：str通过encode()方法可以转换为bytes。
- decode()方法。如果我们从网络或磁盘上读取了字节流，那么读到的数据就是bytes。要把bytes变为str，就需要用decode()方法。

在读取文件的时候也可以设置encode
 open("filename", encoding='ascii', errors='ignore') as f: