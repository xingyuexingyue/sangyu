## 一、Docker安装ubuntu

```
$ docker pull ubuntu:latest
latest: Pulling from library/ubuntu
423ae2b273f4: Already exists 
de83a2304fa1: Already exists 
f9a83bce3af0: Already exists 
b6b53be908de: Already exists 
Digest: sha256:04d48df82c938587820d7b6006f5071dbbffceb7ca01d2814f81857c631d44df
Status: Downloaded newer image for ubuntu:latest
docker.io/library/ubuntu:latest
```

运行容器

```
$ docker run -itd --name ubuntu-test ubuntu
e7c4e77b6b647ef406c9703dcff610f520df524a55d6ae8d672de06db3ce0974
```
进入容器

```
docker attach <容器 ID>
```

## 二、Linux目录结构

进入系统后查看当前路径 是 `/`

```
# pwd
/
```
查看`/`下的目录结构
```
 ls /
bin   etc   lib64  opt   run   sys  var
boot  home  media  proc  sbin  tmp
dev   lib   mnt    root  srv   usr
```

- /bin
这个目录存放着最经常使用的命令

- /boot
这个目录存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件

- /dev
这个目录下存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的

- /etc
这个目录用来存放所有的系统管理所需要的配置文件和子目录

- /home
普通用户的放置位置，刚装好后是空的 随着用户增多而增加

- /lib
这个目录存放着系统最基本的动态连接共享库

- /lost+found
这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件（碎片文件，某个文件丢失了可能在他里找回了）

- /media
Linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，Linux会把识别的设备挂载到这个目录下

- /mnt
临时挂载别的文件系统的，比如光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。

- /opt 
安装第三方软件的

- /proc
这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。
这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器：

```
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
```
- /root
系统管理员，也称作超级权限者的用户主目录

- /sbin 
超级用户的管理工具 系统不可缺少的

- /tmp
这个目录是用来存放一些临时文件的

- /usr：
这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下

- /usr/bin：
系统用户使用的应用程序。

- /usr/sbin：
超级用户使用的比较高级的管理程序和系统守护程序

- /usr/src：
内核源代码默认的放置目录

- /var：
这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件


## 三、Linux远程登录

Linux系统中是通过ssh服务实现的远程登录功能，默认ssh服务端口号为 22

### Mac使用vnc远程登录ubuntu16.04桌面

1、在Ubuntu上安装x11vnc，如下：

```
apt-get install x11vnc
```

2、如果上面的命名执行后提示这个错误

```
E: Unable to locate package x11vnc
```

那么，执行下面命令，再重新执行1步骤的命令

```
apt-get update
```

3、配置vnc密码

```
x11vnc -storepasswd
```

4、启动vnc服务
```
x11vnc -forever -shared -rfbauth ~/.vnc/passwd
```

5、在mac上安装vnc viewer，安装好后，在File菜单里New connection，填上ip，然后点击OK即可

### 终端利用ssh登录远程服务器

1、首先打开终端，然后输入sudo su - 回车进入根目录

2、然后输入：ssh -p 端口号 服务器用户名@ip （例如ssh -p 22 userkunyu@119.29.37.63
）回车，到这会让你输入yes或者no来确认是否连接，输入yes回车

```
ssh -p 50022 my@127.0.0.1
输入密码：
my@127.0.0.1:
```

3、然后输入在服务器上的用户密码回车

4、到此进入的是你在服务器上的账户的目录，即为连接成功

5、最后输入sudo su -进入服务器的根目录，进行操作

## 四、Linux 文件基本属性

Linux系统是一种典型的多用户系统，不同的用户处于不同的地位，拥有不同的权限。为了保证系统的安全性，Linux系统对不同的用户访问同一文件（包括目录文件）的权限做了不同的规定。

使用`ll`或者`ls-l`来显示一个文件的属性以及文件所属的用户和组

```
/# ls -l
total 64
drwxr-xr-x   2 root root 4096 Feb 19 09:17 bin
```

上面结果的中含义分别是：

第一个字符代表这个文件是目录、文件或链接文件等

- 当为[`d`]则是目录
- 当为[`-`]则是文件
- 当为[`l`]表示为链接文档
- 当为[`b`]表示为装置文件里面的可供储存的接口设备（可随机存取装置）
- 当为[`c`]表示装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)

接下来的字符中，以三个为一组，且均为「rwx」三个参数的组合。这三个权限的位置不会改变。如果没有权限，就会出现[ - ]

> [ r ]代表可读（read）
> [ w ]代表可写（write）
> [ x ]代表可写（execute）

所以```drwxr-xr-x ``含义是：

![](https://upload-images.jianshu.io/upload_images/2765653-a3eeb5d74bc29b43.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 五、Linux 文件和属组

```
drwxr-xr-x 3 mysql mysql 4096 Apr 21  2014 mysql
```

Linux系统按文件所有者、文件所有者同组用户和其他用户来规定了不同的文件访问权限。

所以上面的例子的含义是，mysql是一个目录文件，属主和属组都是mysql，属主有可读、可写、可执行的权限；与属主同组的其他用户有可读和可执行的权限；其他用户也有可读和可执行的权限。

更改文件属组

```
# 这里有个文件test 属主和属组都是root
ls -l
total 68
-rw-r--r--   1 root root   31 Mar 19 15:30 test
# 现在将这个文件属组修改为bin
chgrp bin test
# 执行上面的命名后查看是否修改了
ls -l
total 68
-rw-r--r--   1 root bin    31 Mar 19 15:30 test
# 将这个文件属主修改为bin
chown bin test
# 执行上面的命名后查看是否修改了
ls -l
-rw-r--r--   1 bin  bin    31 Mar 19 15:30 test
# 将test的拥有者和群组都改回为root
# 这次一起改
chown root:root test
# 执行上面的命名后查看是否修改了
root@e7c4e77b6b64:/# ls -l
total 68
-rw-r--r--   1 root root   31 Mar 19 15:30 test
```
更改文件9个属性，就是刚刚rwx三个为一组的基本权限，这三个权限可以使用数字来代表：

` r ` 表示4、` w ` 表示2、` x ` 表示1

属主身份/属组身份/其他用户身份分别用owner/group/others表示，这三个身份的权限是需要累加的，所以当权限为： [-rwxrwx---] 分数则是：

`owner = rwx = 4+2+1 = 7`
`group = rwx = 4+2+1 = 7`
`others= --- = 0+0+0 = 0`

现在我们将test文件的权限修改为770

```
# test 文件现在权限设置
-rw-r--r--   1 root root   31 Mar 19 15:30 test
# 修改权限
chmod 770 test
# 修改后查看
-rwxrwx---   1 root root   31 Mar 19 15:30 test
```

## 六、处理目录的常用命令

列出目录

```
root@e7c4e77b6b64:/# ls
bin   etc   lib64  opt   run   sys   usr
boot  home  media  proc  sbin  test  var
dev   lib   mnt    root  srv   tmp

# 列出全部文件，包含隐藏文件
root@e7c4e77b6b64:/# ls -a
.           bin   etc   lib64  opt   run   sys   usr
..          boot  home  media  proc  sbin  test  var
.dockerenv  dev   lib   mnt    root  srv   tmp

# 列出文件的属性与权限
root@e7c4e77b6b64:/# ls -l
total 68
drwxr-xr-x   2 root root 4096 Feb 19 09:17 bin
```

切换目录

```
# 现在的目录结构为：
# /tese/rese1/rese1-a
# /tese/rese1/rese1-b
# 打开/tese/rese1/rese1-a 以绝对路径的方式打开
root@e7c4e77b6b64:/# cd /tese/rese1/rese1-a
root@e7c4e77b6b64:/tese/rese1/rese1-a# 
# 现在我们已经进入rese1-a文件了
# 以相对路径的方式打开rese1-b
root@e7c4e77b6b64:/tese/rese1/rese1-a# cd ../rese1-b
root@e7c4e77b6b64:/tese/rese1/rese1-b# 
# 回到根目录， /root 这个目录
root@e7c4e77b6b64:/tese/rese1/rese1-b# cd ~
root@e7c4e77b6b64:~# 
# 回到当前目录的上一级目录
root@e7c4e77b6b64:~# cd ..
root@e7c4e77b6b64:/# 
```

显示目前所在的目录

```
root@e7c4e77b6b64:/# pwd
/
```

创建新目录

```
root@e7c4e77b6b64:/tese/rese1# mkdir rese1-c
root@e7c4e77b6b64:/tese/rese1# ls
rese1-a  rese1-b  rese1-c
```

删除空的目录
```
root@e7c4e77b6b64:/# rmdir dir
root@e7c4e77b6b64:/# ls
bin   etc   lib64  opt   run   sys   tmp
boot  home  media  proc  sbin  tese  usr
dev   lib   mnt    root  srv   test  var
# rmdir只能删除空目录
root@e7c4e77b6b64:/# rmdir hhaha
rmdir: failed to remove 'hhaha': Directory not empty
```

复制文件或目录
```
# 将/目录下的tese 复制到h1下并命名为testcp
# 使用-r 递归持续复制
cp -r  tese /h1/testcp
```

移动文件与目录，或修改名称
```
# 将h1移动到h2
root@e7c4e77b6b64:/# mv h1 h2
root@e7c4e77b6b64:/# cd h2
root@e7c4e77b6b64:/h2# ls
h1
# 修改h1的名称
root@e7c4e77b6b64:/h2# mv h1 h1test
root@e7c4e77b6b64:/h2# ls
h1test
```

补充一个的创建文件的命令

```
# 创建文件
# 如果文件不存在，可以创建一个空白文件
# 如果文件存在，可以修改文件的末次修改日期
root@e7c4e77b6b64:/# touch testtouch
root@e7c4e77b6b64:/# ls
bin  boot  dev  etc  h2  h3  hhaha  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tese  test  testtouch  testvim.txt  tmp  usr  var
```

## 七、文件内容查看

```
# 从第一行开始显示文件内容
root@e7c4e77b6b64:/# cat test
# 从最后一行开始显示
root@e7c4e77b6b64:/# tac test
# 显示行号
root@e7c4e77b6b64:/# nl test
# 一页一页翻页
root@e7c4e77b6b64:/# more test
--More--(16%) <== enter翻一行
```

在more这个程序运行过程中，有几个按键可以使用

` 空格键 ` 代表向下翻一页
` Enter ` 代表向下翻一行
` /字串 ` 在显示的内容中，搜索「字串」这个关键字
`:f` 显示档名以及目前显示的行数
`q` 立刻离开more，不在显示该文件内容
`b` 往回翻页

```
# 取出文件前面几行
root@e7c4e77b6b64:/# head test
# 默认显示前面10行 
# 使用-n 自定义显示的行数
root@e7c4e77b6b64:/# head -n 20 test
# 取出文件后面几行
root@e7c4e77b6b64:/# tail test
# 默认显示最后的10行，
# 使用-n自定义显示的行数
root@e7c4e77b6b64:/# tail -n 20 test
# 实时查看文件
# ctrl+c结束
root@e7c4e77b6b64:/# tail -f -n 20 test
```

## 八、vi/vim

基本上vi/vim共分为三种模式，分别是命名模式，输入模式，底部命令模式

```
# 进入一般模式
# 不管文件是否存在
root@e7c4e77b6b64:/# vim testvim.txt
```
进入输入模式（进入一般模式后按下i）

![](https://upload-images.jianshu.io/upload_images/2765653-da4b68dfb07c7a66.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入输入模式后回到一般模式（按下ESC）

![](https://upload-images.jianshu.io/upload_images/2765653-ae91595e044a8e2c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

进入底部命令模式（回到一般模式后按下: 进入底部命令模式）

![](https://upload-images.jianshu.io/upload_images/2765653-6f13dc845f9bc3f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

底部命令模式中

`q ` 退出程序
`w ` 保存文件
`wq ` 退出并保存程序

![](https://upload-images.jianshu.io/upload_images/2765653-44731c27396cdf60.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 九、查看CPU占用率

`top` 查看CPU占用率的命令

图片中两个红框 上面的占用百分率，下面是每个进程的CPU占用率，如果看到有些进程CPU占用超过100%，这种一般是该进程使用了多核。

![](https://upload-images.jianshu.io/upload_images/2765653-a474f753684bcb92.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

运行top命令之后，如果想退出该命令，键入q即可或按ctrl c

## 十、内存占用率


`free -m` 查看内存占用率的命令

图中左边的红框表示占用的内存，图中右边的红框表示剩余的内存

![](https://upload-images.jianshu.io/upload_images/2765653-72216547dd28ab5a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

`total `内存总数
`useed `已经使用的内存数
`free `空闲的内存数
`shared `当前已经废弃不用
`buffers/cache` 缓存的内存数

free + buffers/cache  表示可以挪用内存总数
used - buffers/cache 表示被程序实实在在吃掉的内存
 

## 十一、通过/proc/meminfo实时获取系统内存使用情况

Linux系统中`/proc/meminfo` 这个文件用来记录了系统内存使用的详细情况。

top和free命令中查询到的cpu和内存数据就是通过这个文件中的信息计算并按照特定的格式进行显示

```
root@e7c4e77b6b64:/# cat /proc/meminfo 
MemTotal:        2047132 kB <== 所有内存（RAM）大小，减去一些预留空间和内核的大小
MemFree:          111128 kB <== 完全没有用到的物理内存
MemAvailable:     161336 kB <==  在不使用交换空间的情况下，启动一个新的应用最大可用内存的大小
Buffers:           12356 kB <== 块设备所占用的缓存页，包括：直接读写块设备以及文件系统元数据(metadata)，比如superblock使用的缓存页
Cached:           161408 kB <== 表示普通文件数据所占用的缓存页
SwapCached:       134288 kB
Active:          1305232 kB
Inactive:         514932 kB
Active(anon):    1203872 kB
Inactive(anon):   449860 kB
Active(file):     101360 kB
Inactive(file):    65072 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:       1048572 kB
SwapFree:         230760 kB
Dirty:                36 kB
Writeback:             0 kB
AnonPages:       1614096 kB
Mapped:            91244 kB
Shmem:              7332 kB
Slab:              64048 kB
SReclaimable:      31156 kB
SUnreclaim:        32892 kB
KernelStack:       12784 kB
PageTables:        17696 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     2072136 kB
Committed_AS:    5894216 kB
VmallocTotal:   34359738367 kB
VmallocUsed:           0 kB
VmallocChunk:          0 kB
AnonHugePages:     20480 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       95660 kB
DirectMap2M:     2000896 kB
DirectMap1G:           0 kB
```

## 十二、搜索文本文件名

```
#  在文件搜索一个单词 cat
#  返回包含cat单词的文本行
root@e7c4e77b6b64:/# grep cat test
cat yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy

# 在多个文件中搜索一个单词
# 只有其中一个文件包含搜索单词
root@e7c4e77b6b64:/# grep "cat" test testvim.txt
test:cat yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
# 搜索两个文件都包含的单词
root@e7c4e77b6b64:/# grep "dog" test testvim.txt
test:dog hhhhhhhhhhhhhhhhhhhhhhhhhhhhh
testvim.txt:dog hhh
# 搜索除命中单词的所有行
# 使用-v
root@e7c4e77b6b64:/# grep -v "dog" testvim.txt
iiahhahahh
# 标记匹配颜色 --color = auto
root@e7c4e77b6b64:/# grep "dog" testvim.txt --color=auto
dog hhh
# 搜索条件使用正则表达式
# -E
root@e7c4e77b6b64:/#grep -E "[1-9]+"
# 统计文件或者文本中包含匹配字符串的行数 # -c 选项
root@e7c4e77b6b64:/# grep -c "test" test
157
# 输出包含匹配字符串的行数
# -n
root@e7c4e77b6b64:/# grep "cat" -n test
194:cat yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
# 输出匹配文件之前或者之后的行
# 输出之后的行 
# -A
root@e7c4e77b6b64:/# grep "dog" test -A 3
dog hhhhhhhhhhhhhhhhhhhhhhhhhhhhh
test
test
test
# 输出之前的行 
# -B
root@e7c4e77b6b64:/# grep "dog" test -B 3
test
testtest
test
dog hhhhhhhhhhhhhhhhhhhhhhhhhhhhh
```

## 十三、echo命令

echo命令用于在shell中打印shell变量的值，或者直接输出指定的字符串

```
# 用echo命令打印带有色彩的文字
echo -e "\e[1;31mThis is red text\e[0m"
```

![](https://upload-images.jianshu.io/upload_images/2765653-7d9d8520d2074098.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 十四、文件重定向

```
# 重定向将输入文本通过截取模式保存到文件
# 写入到文件之前，文件内容首先会被清空。
root@e7c4e77b6b64:/# echo "this is a text line one" > test    

# 重定向将输入文本通过追加模式保存到文件
# 写入文件之后，会追加到文件结尾
root@e7c4e77b6b64:/# echo "this is a cat hhaahhah" >> test

# 常见的错误输出到控制台
root@e7c4e77b6b64:/# cat linuxde.net
cat: linuxde.net: No such file or directory
# 将错误输出到文件
# 两种方式
# 文件的内容输入前会被晴空
root@e7c4e77b6b64:/# cat linuxde.net 2> test 
root@e7c4e77b6b64:/# cat linuxde.net &> test 
```

## 十五、管道 tee

tee命令数据重定向到给定文件和屏幕上

存在缓存机制，每1024个字节将输出一次。若从管道接收输入数据，应该是缓冲区满，才将数据转存到指定的文件中。若文件内容不到1024个字节，则接收完从标准输入设备读入的数据后，将刷新一次缓冲区，并转存数据到指定文件。

```
root@e7c4e77b6b64:/# ls | tee
bin
boot
dev
etc
# 将结果输出到文件
root@e7c4e77b6b64:/# ls | tee test 
# 结合cat
# tee可以省略 直接用|
# 下面命令的含义是 查看test文件内容并搜索bin 输出
root@e7c4e77b6b64:/# cat test | grep "bin"
bin
sbin
```

在理解下管道的含义，Linux允许将一个名字的输出，通过管道作为另一个命令的输入，所以在上面的例子中，`cat test | grep "bin"` cat test 就是显示文件的内容，就是输出到管道中，这些将会成为执行grep 命令的输入，根据输入搜索bin单词，除了grep还可以使用more ，内容多时more可以翻页查看

## 十六、查看执行命令所在位置

```
# which 查看执行命令所在位置
root@e7c4e77b6b64:/# which ls
/bin/ls
```

## 十七、进程信息

```
# 查看进程的详细状况
# ps默认只会显示当前用户通过终端启动的应用程序
root@e7c4e77b6b64:/# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.1  18624  2100 pts/0    Ss   13:29   0:01 /bin/bash
root      1695  0.0  0.1  34400  2824 pts/0    R+   19:03   0:00 ps aux
```
 







