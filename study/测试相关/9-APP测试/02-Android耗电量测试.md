## 准备条件
     
充电100%后再多充30分钟后开始测试

关掉其他app排除影响

相同屏幕亮度，最大最好

设置屏幕不自动关闭

使用charles 3G网络限速

每次留bugreport

每次都要重新安装app（或者清楚数据），保证耗电量从0开始计算

## 无线adb技术

安装adb【各种baidu就行】

确保手机跟电脑都处于同一个网络

手机插线连着电脑，确保已连接上，使用【adb devices】命令check，是否连接

输入【adb tcpip 5555】，使用tcpip协议连接手机

1.无线连接手机

adb connect 192.168.1.8

2.清楚已有的耗电量数据

adb shell dumpsys batterystats --enable full-wake-history

3.设备耗电量数据重置

adb shell dumpsys batterystats --reset

4.寻找包名的uid

adb shell ps |find "com.nuomi"

以下是dos下出来的信息，u0_a445就是uid，需要去除下划线_，  即u0a445

u0_a445   7068  772   1646920 85320 SyS_epoll_ 0000000000 S com.nuomi:installdex
u0_a445   7158  772   1854944 226048 SyS_epoll_ 0000000000 S com.nuomi
u0_a445   7190  772   1663432 89120 SyS_epoll_ 0000000000 S com.nuomi:ultranet
u0_a445   7208  772   1641072 85336 SyS_epoll_ 0000000000 S com.nuomi:remote

5.确定测试包的名字和uid

 

adb shell dumpsys batterystats "com.nuomi" |find "u0a445"

6.然后执行业务场景，结束之后杀进程

7.杀完进程后，把耗电量信息传到电脑该目录下

adb bugreport>test.txt

8.等待传送结束，手机会震动以下，表示数据传输到电脑完毕

9.打开记录的txt文件，查找耗电量信息，如下图，1.98mah（毫安时）就是该业务场景的耗电量

![](https://upload-images.jianshu.io/upload_images/2765653-02ce7d55c2006eb0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

https://www.jianshu.com/p/5abd53abcc1e