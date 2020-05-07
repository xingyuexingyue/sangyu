http://mp.weixin.qq.com/s?__biz=MjM5ODY4ODIxOA==&mid=2653208409&idx=1&sn=700996a572b7daf439d975b80f9a0e00&chksm=bd16fbec8a6172fa0fd97fbf367c8527a0979adea08bf6179f170122070ecd0e78404c16647c&mpshare=1&scene=23&srcid=&sharer_sharetime=1588235060812&sharer_shareid=6b4b42a26b513b2137265e480a0e0b4d#rd

http://mp.weixin.qq.com/s?__biz=MjM5ODY4ODIxOA==&mid=2653208697&idx=1&sn=cd2a22b75a274bb4fc6a24cd48225362&chksm=bd1684cc8a610dda910fe20fc9b0832751685d9a75da7b4bd6f614619d7a9370dd14f963f864&mpshare=1&scene=23&srcid=&sharer_sharetime=1588235071377&sharer_shareid=6b4b42a26b513b2137265e480a0e0b4d#rd

## 1 什么是 gRPC ？

gRPC 是一个高性能、通用的开源 RPC 框架，由 Google 主要面向移动应用开发并基于 HTTP/2 协议标准而设计，基于 ProtoBuf(Protocol Buffers) 序列化协议开发，且支持众多开发语言

自 gRPC 推出以来，已经广泛用于各种应用服务之中。在测试中，我们也越来越地遇到 gRPC 接口相关的测试内容。测试一个 gRPC 接口，我们往往需要一个测试用的客户端，本文就为大家介绍如何用 python 来实现一个简易的 gRPC 客户端程序。

## 2 环境搭建

