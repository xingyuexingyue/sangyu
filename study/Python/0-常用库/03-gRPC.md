http://mp.weixin.qq.com/s?__biz=MjM5ODY4ODIxOA==&mid=2653208409&idx=1&sn=700996a572b7daf439d975b80f9a0e00&chksm=bd16fbec8a6172fa0fd97fbf367c8527a0979adea08bf6179f170122070ecd0e78404c16647c&mpshare=1&scene=23&srcid=&sharer_sharetime=1588235060812&sharer_shareid=6b4b42a26b513b2137265e480a0e0b4d#rd

http://mp.weixin.qq.com/s?__biz=MjM5ODY4ODIxOA==&mid=2653208697&idx=1&sn=cd2a22b75a274bb4fc6a24cd48225362&chksm=bd1684cc8a610dda910fe20fc9b0832751685d9a75da7b4bd6f614619d7a9370dd14f963f864&mpshare=1&scene=23&srcid=&sharer_sharetime=1588235071377&sharer_shareid=6b4b42a26b513b2137265e480a0e0b4d#rd

## 1 什么是 gRPC ？

gRPC 是一个高性能、通用的开源 RPC 框架，由 Google 主要面向移动应用开发并基于 HTTP/2 协议标准而设计，基于 ProtoBuf(Protocol Buffers) 序列化协议开发，且支持众多开发语言

自 gRPC 推出以来，已经广泛用于各种应用服务之中。在测试中，我们也越来越地遇到 gRPC 接口相关的测试内容。测试一个 gRPC 接口，我们往往需要一个测试用的客户端，本文就为大家介绍如何用 python 来实现一个简易的 gRPC 客户端程序。

###### 环境搭建

```
pip3 install grpcio
pip3 install grpcio-tools
```

###### 接口协议文档

根据 proto 协议文件生成所需的模块和方法。比如我们要测试的接口协议文档为 helloworld.proto，文档内容为：

```
// helloworld.proto
syntax = "proto3";


service Greeter {
    rpc SayHello(HelloRequest) returns (HelloReply) {}
}
message HelloRequest {
    string name = 1;
}


message HelloReply {
    string message = 1;
}
```

执行如下命令： 

```
python -m grpc_tools.protoc --python_out=. --grpc_python_out=. -I. helloworld.proto
```
生成的模块、方法会保存在两个文件之中，分别为helloworld_pb2.py 和 helloworld_pb2_grpc.py 文件。这两个文件是实现客户端时不可缺少的

###### 客户端实现

将自动生成的文件和模块引入到客户端的代码中，就可以调用一些内置方法来完成与 gRPC 接口的交互：

比如上面生成的文件是helloworld_pb2.py 和 helloworld_pb2_grpc.py，在 client.py 代码中引入，同时还有 grpc 模块：

```
import helloworld_pb2
import helloworld_pb2_grpc
import grpc


def run():

    # 连接 rpc 服务器
    channel = grpc.insecure_channel('localhost:50051')
    # 调用 rpc 服务
    stub = helloworld_pb2_grpc.GreeterStub(channel)
    response = stub.SayHello(helloworld_pb2.HelloRequest(name='test'))
    print("Greeter client received: " + response.message)


if __name__ == '__main__':
    run()
```

###### 服务端实现

```
# greeter_server.py

from concurrent import futures
import logging

import grpc

import helloworld_pb2
import helloworld_pb2_grpc


class Greeter(helloworld_pb2_grpc.GreeterServicer):

    def SayHello(self, request, context):
        return helloworld_pb2.HelloReply(message='Hello, %s!' % request.name)


def serve():
    server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))
    helloworld_pb2_grpc.add_GreeterServicer_to_server(Greeter(), server)
    server.add_insecure_port('[::]:50051')
    server.start()
    server.wait_for_termination()


if __name__ == '__main__':
    logging.basicConfig()
    serve()
```
###### 执行程序

一定要先运行 server 端代码，再运行client代码。可以看到运行结果

```
Greeter client received: Hello, test!
```

###### 总结

客户端代码关键的步骤为：
1. 连接 rpc 服务器
2. 对 service 获取一个 stub 用于调用接口
3. 发送数据、接收数据
