test.cfg文件内容：

```
[sec_a]
a_key1 = 20
a_key2 = 10
  
[sec_b]
b_key1 = 121
b_key2 = b_value2
b_key3 = $r
b_key4 = 127.0.0.1
```

读配置文件   

```
import ConfigParser

# 生成 config 对象
conf = ConfigParser.ConfigParser()

# 用 config 对象读取配置文件
conf.read("test.cfg")

# 以列表形式返回所有的 section
sections = conf.sections()

# 得到指定 section 的所有 option
options = conf.options("sec_a")

# 得到指定 section 的所有键值对
kvs = conf.items("sec_a")

# 指定 section，option 读取值
str_val = conf.get("sec_a", "a_key1")
int_val = conf.getint("sec_a", "a_key2")
```

写配置文件

```
# 更新指定 section，option 的值
conf.set("sec_b", "b_key3", "new-$r")

# 写入指定 section 增加新 option 和值
conf.set("sec_b", "b_newkey", "new-value")

# 增加新的 section
conf.add_section('a_new_section')
conf.set('a_new_section', 'new_key', 'new_value')

# 写回配置文件
conf.write(open("test.cfg", "w"))
```