os.path 模块主要用于获取文件的属性

1. os.path.basename(path) 返回文件名
```
print(os.path.basename("/Users/pengyapan/PycharmProjects/Practise/os/MyTest.py"))
// 运行结果
MyTest.py
```
2. os.path.abspath(path) 返回绝对路径
```
print(os.path.abspath("MyTest.py"))
// 运行结果
/Users/pengyapan/PycharmProjects/Practise/os/MyTest.py
```
3. os.path.dirname(path) 返回文件路径
```
print(os.path.dirname("/Users/pengyapan/PycharmProjects/Practise/os/MyTest.py"))
// 运行结果
/Users/pengyapan/PycharmProjects/Practise/os
```
4. os.path.exists(path) 判断 path 是否存在，如果存在返回 true，如果不存在返回 false
```
print(os.path.exists("/Users/pengyapan/PycharmProjects/Practise/os/MyTest111.py"))
# 运行结果
false
```
5. os.path.getsize(path) 返回文件大小，如果文件不存在就返回错误
```
print(os.path.getsize("/Users/pengyapan/PycharmProjects/Practise/os/MyTest.py")	)
// 运行结果
382
```
6. os.path.join(path1[, path2[, ...]]) 把传入的多个 path 路径合成一个路径
```
print(os.path.join("/Users/pengyapan", "PycharmProjects", "Practise", "os", "haha.py"))
// 运行结果
/Users/pengyapan/PycharmProjects/Practise/os/haha.py
```
7. os.path.samefile() 判断目录或文件是否相同
```
path1 = "/Users/pengyapan/PycharmProjects/Practise/os"
path2 = "/Users/pengyapan/PycharmProjects/Practise/os"
path3 = "/Users/pengyapan/PycharmProjects/Practise/Practise"
print(os.path.samefile(path1, path3))
# 运行结果
false
```
8. os.path.split() 把路径分割成 dirname 和 basename，返回一个元组
```
print(os.path.split("/Users/pengyapan/PycharmProjects/Practise/os/MyTest.py"))
# 运行结果
('/Users/pengyapan/PycharmProjects/Practise/os', 'MyTest.py')
```