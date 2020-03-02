## Docker 在macos的安装

1、使用 Homebrew 来安装 Docker
```
$ brew cask install docker

==> Creating Caskroom at /usr/local/Caskroom
==> We'll set permissions properly so we won't need sudo in the future
Password:          # 输入 macOS 密码
==> Satisfying dependencies
==> Downloading https://download.docker.com/mac/stable/21090/Docker.dmg
######################################################################## 100.0%
==> Verifying checksum for Cask docker
==> Installing Cask docker
==> Moving App 'Docker.app' to '/Applications/Docker.app'.
&#x1f37a;  docker was successfully installed!
```
2、载入 Docker app 后，点击 Next，如果需要macOS 登陆密码，输入就好了。

3、安装成功后，会弹出一个 Docker 运行的提示窗口，顶部状态栏上会出现一个小鲸鱼的图标

![](https://upload-images.jianshu.io/upload_images/2765653-32afd0a0aae0b28e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4、点击顶部状态栏中的鲸鱼图标打开操作菜单，会出现安装成功的界面，点击got it 关闭

![](https://upload-images.jianshu.io/upload_images/2765653-52409fd9d3ec7e1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

之后打开鲸鱼图标会显示操作菜单

![](https://upload-images.jianshu.io/upload_images/2765653-44cfbdd955389ebf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


查看安装后的 Docker 版本。

```
$ docker --version
Docker version 19.03.1, build 74b1e89
```

5、配置加速器，提高拉取镜像的速度，状态栏点击鲸鱼图标打开菜单栏，网易镜像地址：http://hub-mirror.c.163.com


![](https://upload-images.jianshu.io/upload_images/2765653-e02abff6f716585c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![](https://upload-images.jianshu.io/upload_images/2765653-169df53afb5d99fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
// 查看是否配置成功，出现下面的内容说明安装成功
// Registry Mirrors:
//    http://hub-mirror.c.163.com
$ docker info 
 Registry Mirrors:
 http://hub-mirror.c.163.com/
 Live Restore Enabled: false
 Product License: Community Engine
```

## Docker 介绍

>Docker是一个开源的应用容器引擎，基于Go语言并遵从Apache2.0协议开源
>Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发到任何流行的Linux机器上，也可以实现虚拟化。
>容器是完全使用沙箱机制，相互之间不会有任何接口，更重要的是容器性能开销极低

Docker支持将软件编译成一个镜像；然后在镜像中各种软件做好配置，将镜像发布出去，其他使用者可以直接使用这个镜像。运行中的这个镜像称为容器，容器启动后非常快速。

## Docker 核心概念

- docker镜像 （Images）
用于创建docker容器的模板，开发者可上传

- docker容器
容器是独立运行的一个或一组应用。发布的镜像，使用者运行这个镜像称为容器，一个镜像可以运行多个容器

- docker客户端
客户端通过命令行或者其他工具使用DockerAPI 与Docker的守护进程通信，就是说连接docker主机进行操作

- docker主机（Host）
一个物理或者虚拟的机器用于执行Docker守护进程和容器，可以理解为安装了Docker程序的机器

- docker仓库
Docker仓库用来保存镜像，可以理解为代码控制中的代码仓库。Docker Hub [https://hub.docker.com/](https://hub.docker.com/) 提供了庞大的镜像集合供使用

使用Docker的步骤：

1）安装Docker

2）去Docker仓库找到需要软件对应的镜像

3）使用Docker这个镜像，这个镜像就会生成一个Docker容器

4）对容器的启动停止就是对软件的启动停止

## Docker的常用命令

（此处以Mysql为例）

1、打开[Docker Hub](https://hub.docker.com/)，查看可用的 MySQL 版本

![](https://upload-images.jianshu.io/upload_images/2765653-bde5a90a844a9314.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-99d4ac48655c9391.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

默认是最新版本 mysql:latest ，下面还有其他可用的版本，按照需要复制红框的内容，然后命名行输入

![](https://upload-images.jianshu.io/upload_images/2765653-0f1a9682621bfc11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

命令行查看可用版本 

```
$  docker search mysql
```

```
NAME                              DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   9164                [OK]                
mariadb                           MariaDB is a community-developed fork of MyS…   3263                [OK]                
mysql/mysql-server                Optimized MySQL Server Docker images. Create…   677                                     [OK]
centos/mysql-57-centos7           MySQL 5.7 SQL database server                   70                                      
mysql/mysql-cluster               Experimental MySQL Cluster Docker images. Cr…   63                                      
centurylink/mysql                 Image containing mysql. Optimized to be link…   61                                      [OK]
deitch/mysql-backup               REPLACED! Please use http://hub.docker.com/r…   41                                      [OK]
bitnami/mysql                     Bitnami MySQL Docker Image                      36                                      [OK]
...
```

2、拉取镜像

```
// 拉取官方的最新版本的镜像
$ docker pull mysql:latest
```

```
// 也可使用默认拉取最新版本镜像
$ docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql
6d28e14ab8c8: Pull complete 
dda15103a86a: Pull complete 
55971d75ab8c: Pull complete 
f1d4ea32020b: Pull complete 
61420072af91: Pull complete 
05c10e6ccca5: Pull complete 
7e0306b13322: Pull complete 
900b113c001e: Pull complete 
06cd07c30bf4: Pull complete 
df0d65aee5aa: Pull complete 
53eeb6e0335c: Pull complete 
6cf8f9563e97: Pull complete 
Digest: sha256:f91e704ffa9f19b9a267d9321550a0772a1b64902226d739d3527fd6edbe3dfe
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest
```

可能会出现的异常，在拉取镜像的时候出现下面的错误
```
$ docker pull tomcat
Error saving credentials: error storing credentials - err: exit status 1, out: `The user name or passphrase you entered is not correct.`
```

解决方法：使用下面的命名，然后根据提示输入用户名和密码登录即可，如果忘记用户名或密码，或者没有的，在官网注册或找回密码就可以了
```
$ docker login
```

3、查看本地镜像

```
$ docker images
REPOSITORY                                      TAG                 IMAGE ID            CREATED             SIZE
mysql                                           latest              c8ad2be69a22        2 days ago          465MB
```
4、运行容器 ，就是刚刚安装的镜像 
```
$ docker run -itd --name mysql-test -p 6606:6606 -e MYSQL_ROOT_PASSWORD=123456 mysql
5aa405af510f10336d9f34d5f8a7b0865035c0f1c855fc32f1f24ff5fbb6e263
```

```
// -p 3306:3306 ：表示映射容器服务的 3306 端口到宿主机的 3306 端口，外部主机可以直接通过 宿主机ip:3306 ， 访问到 MySQL 的服务
// MYSQL_ROOT_PASSWORD=123456：设置 MySQL 服务 root 用户的密码
// --name 设置容器名称
// -d 后台运行
//  -t让docker分配一个伪终端并绑定到容器的标准输入上
// -i则让容器的标准输入保持打开.
```

查看运行的容器

```
$ docker ps
```

有时候会发现运行容器后，使用```docker ps```却没有显示
 
```
// 使用命令查看所有运行过的容器
$ docker ps -a
CONTAINER ID        IMAGE                                                 COMMAND                  CREATED             STATUS                           PORTS                                                                                                                      NAMES                                                                                                                        
d1b20d117a73        rabbitmq:management                                   "docker-entrypoint.s…"   5 days ago          Exited (255) About an hour ago   0.0.0.0:4369->4369/tcp, 0.0.0.0:5671-5672->5671-5672/tcp, 0.0.0.0:15671-15672->15671-15672/tcp, 0.0.0.0:25672->25672/tcp   myrabbit                                                                                                                                                                                 
```

由上图可以看出这个容器不是没有运行，而是运行过然后自动退出了。可以查看日志来观察退出的原因

```
// 根据CONTAINER ID查看对应容器日志
$ docker logs  [CONTAINER ID]
```
```
// 根据CONTAINER ID删除对应容器
$ docker rm [CONTAINER ID]
// 删除所有的容器
$ sudo docker container prune
Password:
WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
```

5、停止容器docker stop [CONTAINER ID]、启动容器 docker start   [CONTAINER ID]

```
// 停止容器
$ docker stop 5aa405af510f
5aa405af510f

//启动容器
$ docker start  5aa405af510f
5aa405af510f
pengyapandeMacBook-Air:WebDriverAgent pengyapan$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                         NAMES
5aa405af510f        mysql               "docker-entrypoint.s…"   3 minutes ago       Up 3 seconds        3306/tcp, 33060/tcp, 0.0.0.0:6606->6606/tcp   mysql-test
```

6、使用一个镜像启动多个容器，互相独立
```
$ docker pull tomcat
Using default tag: latest
latest: Pulling from library/tomcat
50e431f79093: Pull complete 
dd8c6d374ea5: Pull complete 
c85513200d84: Pull complete 
55769680e827: Pull complete 
e27ce2095ec2: Pull complete 
5943eea6cb7c: Pull complete 
3ed8ceae72a6: Pull complete 
91d1e510d72b: Pull complete 
98ce65c663bc: Pull complete 
27d4ac9d012a: Pull complete 
Digest: sha256:2c90303e910d7d5323935b6dc4f8ba59cc1ec99cf1b71fd6ca5158835cffdc9c
Status: Downloaded newer image for tomcat:latest
docker.io/library/tomcat:latest
$ docker images
REPOSITORY                                      TAG                 IMAGE ID            CREATED             SIZE
tomcat                                          latest              4e7840b49fad        2 days ago          529MB
$ docker run -d -p 8889:8080 tomcat
d608a9214b0059aa599d740c305251da8039dfc630b1fa6926f640561b6ff70e
$ docker run -d -p 8887:8080 tomcat
e1c801d0d780030e4246fd33efee206a361224f71588aa67470dbc61b9991d29
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                         NAMES
e1c801d0d780        tomcat              "catalina.sh run"        11 seconds ago      Up 9 seconds        0.0.0.0:8887->8080/tcp                        lucid_newton
d608a9214b00        tomcat              "catalina.sh run"        17 seconds ago      Up 14 seconds       0.0.0.0:8889->8080/tcp                        
```

7、其他高级操作

```
// 文件挂载
$ docker run --name mysql -v /my/custom:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456 mysql 
// 把主机的/my/custom文件夹挂载到mysqldocker容器的/etc/mysql/conf.d文件里面，现在镜像内就可以共享宿主机里的文件了，改mysql的配置文件就只需要把mysql配置文件放在/my/custom
```
```
// 指定mysql的一些参数，指定mysql的编码集，建表的时候不需要再次指定了
$ docker run --name mysql -v /my/custom:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=123456 mysql --character-set-server=utf8mb4 --collection-server=utf8mb4_unicode_ci
```