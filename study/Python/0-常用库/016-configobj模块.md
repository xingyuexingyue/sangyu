读文件

```
from configobj import ConfigObj  
config = ConfigObj(filename)  

value1 = config['keyword1']  
value2 = config['keyword2']  

section1 = config['section1']  
value3 = section1['keyword3']  
value4 = section1['keyword4']  

value3 = config['section1']['keyword3']  
value4 = config['section1']['keyword4']    
``` 

写文件如下：
```
from configobj import ConfigObj
config = ConfigObj()
config.filename = filename

config['keyword1'] = value1
config['keyword2'] = value2

config['section1'] = {}
config['section1']['keyword3'] = value3
config['section1']['keyword4'] = value4

section2 = {
    'keyword5': value5,
    'keyword6': value6,
    'sub-section': {
        'keyword7': value7
        }
}
config['section2'] = section2

config['section3'] = {}
config['section3']['keyword 8'] = [value8, value9, value10]
config['section3']['keyword 9'] = [value11, value12, value13]

config.write()
```