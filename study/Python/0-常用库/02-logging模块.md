###### 日志

日志是跟踪软件运行时所发生的事件的一种方法。软件开发者在调用日志函数，表明发生了特定的事件。事件由描述性消息描述，该描述性消息可以可选地包含可变数据（即，对于事件的每次出现都潜在地不同的数据）。事件还具有开发者归因于事件的重要性；重要性也可以称为级别或重要性

###### logging 级别

logging提供了一组便利的函数，用来做简单的日志。它们是 debug()、 info()、 warning()、 error() 和 critical()

级别级别按照严重程度从低到高为：DEBUG < INFO < WARNING < ERROR < CRITICAL

每个级别对应的适用性描述：

| 级别 | 适用范围 |
|---|---|
|  DEBUG  |详细信息，一般只在调试问题时使用|
| INFO |证明事情按预期工作|
| WARNING |某些没有预料到的事件的提示，或者在将来可能会出现的问题提示|
| ERROR |由于更严重的问题，软件已不能执行一些功能了|
| CRITICAL |严重错误，表名软件已不能继续运行了|

默认级别 WARNING ，这意味着仅仅这个等级以上的才会反馈信息，除非 logging 模块被用来做其它事情

每个级别对应的数字值

| 级别 | 数字值|
|---|---|
| NOTSET  | 0 |
|  DEBUG  | 10 |
| INFO | 20 |
| WARNING | 30 |
| ERROR | 40 |
| CRITICAL | 50 |

被跟踪的事件能以不同的方式被处理。最简单的方法是把它们在控制台上打印出来。另一种常见的方法就是写入磁盘文件

###### 默认级别打印到控制台

```
import logging

logging.debug('debug 信息')
logging.warning('只有这个会输出')
logging.info('info 信息')
```
在上面的代码中，最终控制台只有 `logging.warning('只有这个会输出')` 会输出，这是因为默认的日志级别是 warning ，只有它以及它以上的级别信息会输出

##### 修改默认级别打印到控制台

```
import logging

logging.basicConfig(format='%(asctime)s - %(pathname)s[line:%(lineno)d] - %(levelname)s: %(message)s',
                    level=logging.DEBUG)
logging.debug('debug 信息')
logging.info('info 信息')
logging.warning('warning 信息')
logging.error('error 信息')
logging.critical('critial 信息')
```

利用 logging.basicConfig() 修改日志默认级别为DEBUG，然后调用 debug, info, warning, error, critical，所有信息的log都会打印到控制台

##### 保存 log 到文件

```
import logging

logging.basicConfig(level=logging.DEBUG,
                    filename='new.log',
                    filemode='a',
                    format='%(asctime)s - %(pathname)s[line:%(lineno)d] - %(levelname)s: %(message)s')
logging.debug('debug 信息')
logging.info('info 信息')
logging.warning('warning 信息')
logging.error('error 信息')
logging.critical('critial 信息')
```
如果配置了日志保存到文件中，那么控制台将不会输出，同样使用 logging.basicConfig() 方法，只是方法中用到了 filename 参数设置为要保存日志的地址和日志文件的名称和格式；另一个要注意的参数是 filemode 它有两个值可以传入，默认是 a，追加写入到日志文件中，就是之前写入的日志文件不会被覆盖，除了 a 还有 w 会覆盖之前写入的日志，如果不写的话，默认就是 a，追加模式

##### Logger 对象

logging库采取了模块化的设计，提供了许多组件：记录器、处理器、过滤器和格式化器。

- Logger 暴露了应用程序代码能直接使用的接口
- Handler 将（记录器产生的）日志记录发送至合适的目的地 
- Filter 提供了更好的粒度控制，它可以决定输出哪些日志记录
- Formatter 指明了最终输出中日志记录的布局

**Loggers**

1. 首先，它们向应用代码暴露了许多方法，这样应用可以在运行时记录消息
2. 记录器对象通过严重程度（默认的过滤设施）或者过滤器对象来决定哪些日志消息需要记录下来
3. 记录器对象将相关的日志消息传递给所有感兴趣的日志处理器

常见的配置方法：

Logger.setLevel() 指定logger将会处理的最低的安全等级日志信息, debug是最低的内置安全等级，critical是最高的内建安全等级。例如，如果严重程度为INFO，记录器将只处理INFO，WARNING，ERROR和CRITICAL消息，DEBUG消息被忽略


Logger.addHandler()和Logger.removeHandler() 从记录器对象中添加和删除处理程序对象。

Logger.addFilter()和Logger.removeFilter() 从记录器对象添加和删除过滤器对象。

**Handlers**

处理程序对象负责将适当的日志消息（基于日志消息的严重性）分派到处理程序的指定目标。Logger 对象可以通过 addHandler() 方法增加零个或多个 handler 对象。举个例子，一个应用可以将所有的日志消息发送至日志文件，所有的错误级别（error）及以上的日志消息发送至标准输出，所有的严重级别（critical）日志消息发送至某个电子邮箱。在这个例子中需要三个独立的处理器，每一个负责将特定级别的消息发送至特定的位置。

常见的有4种：
1. logging.StreamHandler  控制台输出 
2. logging.FileHandler  文件输出
和StreamHandler类似，用于向一个文件输出日志信息。不过FileHandler会帮你打开这个文件。它的构造函数是：
FileHandler(filename[,mode])
filename是文件名，必须指定一个文件名。
mode是文件的打开方式。默认是’a'，即添加到文件末尾。
3. logging.handlers.RotatingFileHandler 按照大小自动分割日志文件，一旦达到指定的大小重新生成文件 
它的构造函数是：
RotatingFileHandler( filename[, mode[, maxBytes[, backupCount]]])
其中filename和mode两个参数和FileHandler一样。
maxBytes用于指定日志文件的最大文件大小。如果maxBytes为0，意味着日志文件可以无限大，这时上面描述的重命名过程就不会发生。
backupCount用于指定保留的备份文件的个数。比如，如果指定为2，当上面描述的重命名过程发生时，原有的chat.log.2并不会被更名，而是被删除。

4. logging.handlers.TimedRotatingFileHandler  -> 按照时间自动分割日志文件 
这个Handler和RotatingFileHandler类似，不过，它没有通过判断文件大小来决定何时重新创建日志文件，而是间隔一定时间就 自动创建新的日志文件。重命名的过程与RotatingFileHandler类似，不过新的文件不是附加数字，而是当前时间。它的构造函数是：
TimedRotatingFileHandler( filename [,when [,interval [,backupCount]]])
其中filename参数和backupCount参数和RotatingFileHandler具有相同的意义。
interval是时间间隔。
when参数是一个字符串。表示时间间隔的单位，不区分大小写。它有以下取值：
S 秒
M 分
H 小时
D 天
W 每星期（interval==0时代表星期一）
midnight 每天凌晨

配置方法：
setLevel()方法和日志对象的一样，指明了将会分发日志的最低级别。为什么会有两个setLevel()方法？记录器的级别决定了消息是否要传递给处理器。每个处理器的级别决定了消息是否要分发。

setFormatter()为该处理器选择一个格式化器。

addFilter()和removeFilter()分别配置和取消配置处理程序上的过滤器对象。


** Formatters**














