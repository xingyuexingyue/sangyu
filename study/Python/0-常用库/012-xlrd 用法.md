###### 1 安装

```
pip3 install xlrd
```
###### 2 常见方法

打开 Excel 文件读取数据，获得一个工作表对象

```
filename = '../case1.xls'
data = xlrd.open_workbook(filename)
```
返回所有 Sheet 对象

```
table = data.sheets()
```

通过索引顺序获取 Sheet 对象

```
table1 = data.sheets()[0]
```

返回所有 sheet 的名称

```
names = data.sheet_names()
```

检查某个 sheet 是否导入完毕

```
data.sheet_loaded('sheet1')
```

根据 sheet 索引或者名称获得对应的 sheet 对象，再由 sheet 对象获得 sheet 名称、行数、列数
```
sheet2 = data.sheet_by_index(0)
print(sheet2.name)
print(sheet2.nrows)
print(sheet2.ncols)
```

通过 sheet 名称获取此 sheet 下某行和某列的值

```
sheet3 = data.sheet_by_name('sheet1')
rows = sheet2.row_values(0)
cols = sheet2.col_values(0)
print(rows)
print(cols)
```

通过 sheet 名称获取此 sheet 下指定单元格的内容，cell(行数,列数)

```
sheet3.cell(1, 1).value.encode('utf-8')
```

获取单元格内容的数据类型 ctype : 0 empty,1 string, 2 number, 3 date, 4 boolean, 5 error
```
sheet2.cell(1, 0).ctype
sheet2.cell(1, 1).ctype
sheet2.cell(1, 2).ctype
```

excel 写数据

```
filename = '../case1.xls'
data = xlrd.open_workbook(filename)
write_data = copy(data)
sheet_data = write_data.get_sheet(sheet)
sheet_data. write(row, col, data)
filename = getFilePath('filename', 'excel')
write_data.save(filename)
```



