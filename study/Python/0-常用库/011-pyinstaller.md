PyInstaller 是 Python 的第三方库，可以用来打包 python 应用程序，打包完的程序就可以在没有安装 Python 解释器的机器上运行。

支持 Python 2.7 / 3.4-3.7。可以在 Windows、Mac OS X 和 Linux 上使用，但是并不是跨平台的，如果希望打包成 .exe 文件，需要在 Windows 系统上运行 PyInstaller 进行打包工作。

###### 1 安装

```
 pip3 install pyinstaller
```

###### 2 HelloWorld.py

![](https://upload-images.jianshu.io/upload_images/2765653-af7f7801a8041456.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 3 执行命令生成可执行程序

```
pyinstaller -F HelloWorld.py
```

PyInstaller 会对脚本进行解析，并做出如下动作：

1. 在脚本目录生成 helloworld.spec 文件；
```
(venv) pengyapandeAir:MyTest pengyapan$ pyinstaller -F HelloWorld.py
# 301 INFO: PyInstaller: 3.6
# 301 INFO: Python: 3.7.0b4
# 322 INFO: Platform: Darwin-17.2.0-x86_64-i386-64bit
323 INFO: wrote /Users/pengyapan/PycharmProjects/MyTest/HelloWorld.spec
...
```
2. 创建一个 build 目录，写入一些日志文件和中间流程文件到 build 目录
```
6134 INFO: Warnings written to /Users/pengyapan/PycharmProjects/MyTest/build/HelloWorld/warn-HelloWorld.txt
6165 INFO: Graph cross-reference written to /Users/pengyapan/PycharmProjects/MyTest/build/HelloWorld/xref-HelloWorld.html
6187 INFO: checking PYZ
6187 INFO: Building PYZ because PYZ-00.toc is non existent
6188 INFO: Building PYZ (ZlibArchive) /Users/pengyapan/PycharmProjects/MyTest/build/HelloWorld/PYZ-00.pyz
6633 INFO: Building PYZ (ZlibArchive) /Users/pengyapan/PycharmProjects/MyTest/build/HelloWorld/PYZ-00.pyz completed successfully.
...
```
3. 创建 dist 目录，生成可执行文件到 dist 目录；
```
10077 INFO: Appending archive to EXE /Users/pengyapan/PycharmProjects/MyTest/dist/HelloWorld
10090 INFO: Fixing EXE for code signing /Users/pengyapan/PycharmProjects/MyTest/dist/HelloWorld
10103 INFO: Building EXE from EXE-00.toc completed successfully.
```

###### 4. 运行后目录结构：

![](https://upload-images.jianshu.io/upload_images/2765653-be3bc626dbf126d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在 finder 中找到项目所在路径并打开 dist 下的可执行文件运行后：

![](https://upload-images.jianshu.io/upload_images/2765653-8ab87fad4babdf32.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样一个简单的 python 脚本就运行起来了

但是，当你的代码需要调用一些图片和资源文件的，pyinstaller 时不会自动导入的，所以需要手动将这些资源添加的 .spec 中，否则运行是会报错提示找不到资源。

在项目中增加一个 HelloWorld.txt 文件

![](https://upload-images.jianshu.io/upload_images/2765653-8052cd6ed427366c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

修改 HelloWorld.py 中的代码，增加对 txt 文件的读取

![](https://upload-images.jianshu.io/upload_images/2765653-e0299eec99f19061.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

修改 HelloWorld.spec 

![](https://upload-images.jianshu.io/upload_images/2765653-94ee79ea733078ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

执行如下命令

```
pyinstaller HelloWorld.spec
```

 运行 dist 下的可执行文件运行

![](https://upload-images.jianshu.io/upload_images/2765653-a80be05ccdef1248.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


