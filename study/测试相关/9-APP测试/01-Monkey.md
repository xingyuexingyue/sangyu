## Monkey的测试策略

一.  分类

Monkey测试针对不同的对象和不同的目的采用不同的测试方案，首先测试的对象、目的及类型如下：

测试的类型分为：应用程序的稳定性测试和压力测试

测试对象分为：单一apk和apk集合

测试的目的分为：解决问题的测试(忽略异常的测试)和验收测试（不忽略异常的测试）

二. 应用程序的稳定性测试：

1. 针对单个apk

(1) 不忽略异常

在进行单个apk的验收测试时，则使用单一apk且不忽略异常的命令执行。

例如：
monkey -p com.android.mms --throttle 1000 -s 100-v -v -v 15000 > /mnt/sdcard/monkey_test.txt &

(2) 忽略异常

在进行单个apk的解决问题的测试时，则使用单一apk且忽略异常的命令执行，这样可以在一次执行的过程中发现应用程序中的多个问题。

例如：
monkey -p com.android.mms --throttle 1000 -s 100--ignore-crashes --ignore-timeouts --ignore-security-exceptions--ignore-native-carshes --monitor-native-crashes -v -v -v 15000 >/mnt/sdcard/monkey_test.txt &


2. 针对多个apk

(1) 不忽略异常

例如：

monkey --pkg-whitelist-file /data/whitelist.txt--throttle 1000 -s 100 -v -v -v 15000 > /mnt/sdcard/monkey_test.txt &

(2) 忽略异常

例如：

monkey --pkg-whitelist-file /data/whitelist.txt--throttle 1000 -s 100 --ignore-crashes --ignore-timeouts--ignore-security-exceptions --ignore-native-carshes --monitor-native-crashes-v -v -v 15000 > /mnt/sdcard/monkey_test.txt &

三. 应用程序的压力/健壮性测试

应用程序的压力/健壮性测试，其主要是缩短monkey测试中事件与事件之间的延迟时间，验证在快速的事件响应的过程中，程序是否能正常运行。这种压力/健壮性测试主要是针对单一apk来执行；我们可以将--throttle的值设定为500或者更小，一般都使用500毫秒的延迟事件。

在进行apk的集合测试时，对于高频率使用的apk、长时间使用的apk都要包含在执行的应用程序中间。

APK分类具体：

高频率使用的apk如：Phone、Contacts、Message、Settings、File Manager、Gallery、Input Method

长时间使用的apk如：Phone、Browser、Music player、Camera、Video player、Email、Chat

其他的apk如：Calendar、Notepad、Calculator、FM Radio、Google Search

