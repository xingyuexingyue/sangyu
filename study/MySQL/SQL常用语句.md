## 一、MySQL的登录和退出

- `mysql -h 主机名 -u 用户名 -p`
    - `-h`：mysql的主机名，本机可以省略
    - `-u`: 登录的用户名
    - `-p`：使用密码登录，如果没有省略

- `mysql -u root -p` 登录本机的MySQL数据库
- 登录后输入exit或quit退出mysql

## 二、数据库使用

- `show database` 查看数据库
- `create database <数据库名>;` 创建数据库
- `use <数据库名>;` 使用某个库
- `select database();` 查看所在库

## 三、数据表使用

##### 1. 创建表

语法：`create table <table_name> (column_name column_type);`

```
create table IF NOT EXISTS user(
    `id` INT UNSIGNED AUTO_INCREMENT,
    `name` VARCHAR(100),
    `age` INT NOT NULL,
    `birthday` DATE,
    PRIMARY KEY( `id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
参数说明：

`auto-increment` 每次插入新记录时，自主地创建主键字段值

`primary key` 设置主键，可以使用多列来定义主键，以逗号隔开

`unsigned` 属性只针对整型 ，设置为非负数，用此类型增加数据长度

`Engine` 设置存储引擎

`not null` 字段不能为null

`null` 默认值为null

`default` 为字段设置一个默认值

##### 2. 查看表结果

`desc <table_name>`

## 四、查询语句

> 从下面开始所有例子会用到的表，可以通过这里参考链接: https://pan.baidu.com/s/1Tsf1G_CaXJqBx6pAPjxcqw 提取码: uje3
>
> MySQL执行外部sql脚本文件的命令：
>
> 1. mysql -u root -p
> 
> 2. source 路径\ss.sql


##### 1. 查询表中的单个字段

`select department_name from departments;`

##### 2. 查询表中的多个字段

`select department_name,manager_id from departments;`

##### 3. 查询表中的所有字段，列出所有字段

`select department_id,department_name,manager_id,location_id from departments;`

##### 4. 查询表中的所有字段，使用*

`select * from departments;`

使用3和4区别：列出所有字段会按照查询的顺序，*会按照表中列的顺序

##### 5. 查询结果去重

`select distinct department_name from departments;`

注意：如果查询出结果特别大的情况，不建议是用distinct，因为mysql会先查询出所有的结果，如果数据量大会占用特别大的内存

##### 6. 查询结果别名

`select department_name as name,manager_id  as id from departments;`

或者用空格 但别名中不能包含空格等特殊符号，如果包含""

##### 7. 查询员工号为176的员工的姓名和部门号的年薪

`select last_name,department_id,salary*12*(1+IFNULL(commission_pct,0)) as salary from employees;`

## 五、条件查询

##### 1. 执行顺序

`select 查询列表 from 表名 where 筛选条件`

![执行顺序](https://upload-images.jianshu.io/upload_images/2765653-3bc7543533af4026.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 条件表达式筛选：> < = != <> >= <=
> 
> 逻辑表达式筛选：and or not
> 
> and：两个条件都为true，结果为true，反之为false
> 
> or: 只要有一个条件为true，结果为true，反之为false
> 
> not：如果连接的条件本身为false，结果为true，反之为false

##### 2. 查询工资>12000的员工信息

`select * from employees where salary > 12000;`

##### 3. 查询工资在10000和20000之间的员工名、工资以及资金

`select last_name,salary,commission_pct from employees where salary>12000;`

##### 4. 使用between and

`select * from employees where salary between 10000 and 20000;`

##### 5. 查看部门编号不是在90-110之间，或者工资高于15000的员工信息

`select * from employees where not(department_id >= 90 and department <= 110) or salary >= 15000; `

##### 6. 查询没有commission_pct的员工信息

`select * from employees where comission_pct is null;`

##### 7.  查询有commission_pct的员工信息

`select * from employees where commission_pct is not null;`

这里要注意：= 或 <> 不能判断null值，只能通过is null或is not null可以判断null值


## 六、模糊查询

> 通配符 % _
>
> % 任意多个字符
>
> _ 任意单个字符

##### 1. 查询员工名中第二个字符为o的员工名

`select last_name,salary from employees where last_name like '_o_%;'`

##### 2. 查询员工的工种编号是IT_PROG、AD_VP、AD_PRES中的一个员工名和工种编号

`select last_name,job_id from employees where job_id in ('IT_PROG'、'AD_VP'、'AD_PRES');`

##### 3. 使用%查询出的结果没有null

`select * from employees where commission_pct like '%%' and last_name like '%%';`

## 七、排序查询

##### 1. 执行顺序

`select 查询列表 from 表 【where条件】order by 排序列表 【asc | desc】`

> asc 升序 默认升序
>
> desc 降序
>
> order by一般放在查询语句的最后面，limit子句除外

![查询顺序](https://upload-images.jianshu.io/upload_images/2765653-c585788cf3e98751.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 2. 查询部门编号>=90的员工信息，按入职时间的先后顺序进行排序

`select * from employeess where department_id >= 90 order by hiredate asc`

##### 3. 按年薪的高低显示员工的信息和年薪（按别名排序）

`select *,salary*12*(1+ifnull(commission_pct,0)) as mysalary from employees order by length(last_name) desc;`

##### 4. 按多个字段排序，查询员工信息，要求先按工资升序，再按员工编号降序

select * from employees order by salary asc,employee_id desc;

## 八、函数

> sum 求和
>
> avg 平均值
>
> max 最大值
>
> min 最小值
>
> count计算个数

`select sum(salary) from employees;`
`select avg(salary) from employees;`
`select max(salary) from employees;`
`select min(salary) from employees;`
`select count(distinct salary) from employees;`

##### 1. 统计行数count(*)

`select count(*) from employees;`

##### 2. 查询部门编号为90的员工个数

`select count(*) from employees where department_id = 90;`

##### 3. 查询员工表的最大入职时间和最小入职时间的相差天数

`select datediff(max(hiredate),min(hiredate)) days from employees;` 


## 九、分组查询

```
    from 表
    [where 筛选条件]
    gropu by 分组的列表
    [order by 子句]

注意：select后面的查询列表必须特殊，要求是分组函数和group by后出现的字段
```

##### 1. 查询每个工种的最高工资

`select max(salary),job_id from employees group by job_id;`

##### 2. 查询邮箱中包含a字符的，每个部门的平均工资

`select avg(salary),department_id from employees where email like '%a%' group by department_id;`

##### 3. 查询有奖金的每个领导手下员工的最高工资

`select max(salary),manager_id from employees where commission_pct is not null group by manager_id;`

##### 4. 查询哪个部门的员工个数>2

使用group by进行分组拿到每个部门的员工个数，再使用having筛选个数>2的部门

`select avg(salary),department_id,job_id from employees group by job_id having count(*) >2 ;`

##### 5. 按多个字段分组，查询每个部门每个工种的员工的平均工资

`select avg(salary),department_id,job_id from employees group by job_id,department_id;`

##### 6. 查询每个部门每个工种的员工的平均工资，并且按工资的高低显示

`select avg(salary),department_id,job_id from employees group by job_id,department_id order by avg(salary) desc;`

## 十、连表查询

##### 1. 查询员工名和对应的部门名

`select last_name,department_name from employees,departments  where employees.`department_id` = departments.`department_id`;`

##### 2. 查询员工的工资和工资级别

`select salary,grade_level from employees,job_grades where salary between job_grades.lowest_sal and job_grades.highest_sal;`

##### 3. 三表连接查询

`select last_name,department_name,city from employees,departments ,locations where employees.`department_id` = departments.`department_id` and departments.location_id = locations.location_id;`

## 十一、join

```
select 查询列表
from 表1 别名 【连接类型】
join 表1 别名
on 连接条件
【where 筛选条件】
【group by 分组】
【having 筛选条件】
【order by 排序列表】
```

先看一个两个表普通查询出来的结果，因为笛卡尔乘积，使我们看到的结果使两个表相乘的结果

```
select * from tbl_dept,tbl_emp;
+----+----------+--------+----+------+--------+
| id | deptName | iocAdd | id | name | deptId |
+----+----------+--------+----+------+--------+
|  1 | RD       | 11     |  1 | z3   |      1 |
|  2 | HR       | 12     |  1 | z3   |      1 |
|  3 | MK       | 13     |  1 | z3   |      1 |
|  4 | MIS      | 14     |  1 | z3   |      1 |
|  5 | FD       | 15     |  1 | z3   |      1 |
|  1 | RD       | 11     |  2 | z4   |      1 |
|  2 | HR       | 12     |  2 | z4   |      1 |
|  3 | MK       | 13     |  2 | z4   |      1 |
|  4 | MIS      | 14     |  2 | z4   |      1 |
|  5 | FD       | 15     |  2 | z4   |      1 |
|  1 | RD       | 11     |  3 | z5   |      1 |
|  2 | HR       | 12     |  3 | z5   |      1 |
|  3 | MK       | 13     |  3 | z5   |      1 |
|  4 | MIS      | 14     |  3 | z5   |      1 |
|  5 | FD       | 15     |  3 | z5   |      1 |
|  1 | RD       | 11     |  4 | w5   |      2 |
|  2 | HR       | 12     |  4 | w5   |      2 |
|  3 | MK       | 13     |  4 | w5   |      2 |
|  4 | MIS      | 14     |  4 | w5   |      2 |
|  5 | FD       | 15     |  4 | w5   |      2 |
|  1 | RD       | 11     |  5 | w6   |      2 |
|  2 | HR       | 12     |  5 | w6   |      2 |
|  3 | MK       | 13     |  5 | w6   |      2 |
|  4 | MIS      | 14     |  5 | w6   |      2 |
|  5 | FD       | 15     |  5 | w6   |      2 |
+----+----------+--------+----+------+--------+
```

##### 1. inner join

![](https://upload-images.jianshu.io/upload_images/2765653-909b05ea8a941b29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
# 查询出tbl_emp 表中所有员工的tbl_dept信息
select * from tbl_emp e inner join tbl_dept d on d.id = e.deptId;
+----+------+--------+----+----------+--------+
| id | name | deptId | id | deptName | iocAdd |
+----+------+--------+----+----------+--------+
|  1 | z3   |      1 |  1 | RD       | 11     |
|  2 | z4   |      1 |  1 | RD       | 11     |
|  3 | z5   |      1 |  1 | RD       | 11     |
|  4 | w5   |      2 |  2 | HR       | 12     |
|  5 | w6   |      2 |  2 | HR       | 12     |
+----+------+--------+----+----------+--------+
```

##### 2. left join

查询出tbl_emp 表中所有员工的tbl_dept信息，包括tbl_dept信息为空的员工

我们先在tbl_emp 表里面插入一条deptId不存在的记录

```
insert into tbl_emp(name,deptId) values ('h1',10);
Query OK, 1 row affected (0.10 sec)
```
然后使用left join查询

```
select * from tbl_emp e left join tbl_dept d on d.id = e.deptId; 
+----+------+--------+------+----------+--------+
| id | name | deptId | id   | deptName | iocAdd |
+----+------+--------+------+----------+--------+
|  1 | z3   |      1 |    1 | RD       | 11     |
|  2 | z4   |      1 |    1 | RD       | 11     |
|  3 | z5   |      1 |    1 | RD       | 11     |
|  4 | w5   |      2 |    2 | HR       | 12     |
|  5 | w6   |      2 |    2 | HR       | 12     |
|  6 | h1   |     10 | NULL | NULL     | NULL   |
+----+------+--------+------+----------+--------+
```

##### 3、right join

![](https://upload-images.jianshu.io/upload_images/2765653-48ee90f092dc5ced.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

查询出tbl_emp 表中所有员工的tbl_dept信息，包括所有的tbl_dept即使没有相关员工信息

```
 select * from tbl_emp e right join tbl_dept d on d.id = e.deptId;
+------+------+--------+----+----------+--------+
| id   | name | deptId | id | deptName | iocAdd |
+------+------+--------+----+----------+--------+
|    1 | z3   |      1 |  1 | RD       | 11     |
|    2 | z4   |      1 |  1 | RD       | 11     |
|    3 | z5   |      1 |  1 | RD       | 11     |
|    4 | w5   |      2 |  2 | HR       | 12     |
|    5 | w6   |      2 |  2 | HR       | 12     |
| NULL | NULL |   NULL |  3 | MK       | 13     |
| NULL | NULL |   NULL |  4 | MIS      | 14     |
| NULL | NULL |   NULL |  5 | FD       | 15     |
+------+------+--------+----+----------+--------+
```

##### 4、查询出tbl_emp 表中没有tbl_dept信息的员工

![](https://upload-images.jianshu.io/upload_images/2765653-29602a321cd53e6b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
select * from tbl_emp e left join tbl_dept d on d.id = e.deptId where d.id is null;
+----+------+--------+------+----------+--------+
| id | name | deptId | id   | deptName | iocAdd |
+----+------+--------+------+----------+--------+
|  6 | h1   |     10 | NULL | NULL     | NULL   |
+----+------+--------+------+----------+--------+
```

##### 5、查询出tbl_dept表中没有对应员工信息的岗位

![](https://upload-images.jianshu.io/upload_images/2765653-9f95a0d09c0e689a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
select * from tbl_emp e right join tbl_dept d on d.id = e.deptId where e.deptId is null;
+------+------+--------+----+----------+--------+
| id   | name | deptId | id | deptName | iocAdd |
+------+------+--------+----+----------+--------+
| NULL | NULL |   NULL |  3 | MK       | 13     |
| NULL | NULL |   NULL |  4 | MIS      | 14     |
| NULL | NULL |   NULL |  5 | FD       | 15     |
+------+------+--------+----+----------+--------+
```

## 十二、UNION

UNION  语法：
```
SELECT 查询列表 FROM 表名1
UNION
SELECT 查询列表 FROM 表名2;
```

UNION ALL 语法：
```
SELECT 查询列表 FROM 表名1
UNION ALL 
SELECT 查询列表 FROM 表名2;
```
> UNION 操作符用于合并两个或多个 SELECT 语句的结果集
> 并且，每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。
> 
> 默认，UNION 选取的是不同的值。如果允许重复的值，使用 UNION ALL。

首先看下两个测试表的数据

```
select * from Websites;
+----+---------------+----------------------+-------+---------+
| id | name          | url                  | alexa | country |
+----+---------------+----------------------+-------+---------+
|  1 | Google        | https://www.google.c |     1 | USA     |
|  2 | 淘宝          | https://www.taobao.c |    13 | CN      |
|  3 | 菜鸟教程      | http://www.runoob.co |  4689 | CN      |
|  4 | 微博          | http://weibo.com/    |    20 | CN      |
|  5 | Facebook      | https://www.facebook |     3 | USA     |
|  6 | stackoverflow | http://stackoverflow |     0 | IND     |
+----+---------------+----------------------+-------+---------+
```

```
select * from apps;
+----+------------+----------------------+---------+
| id | app_name   | url                  | country |
+----+------------+----------------------+---------+
|  1 | QQ APP     | http://im.qq.com/    | cn      |
|  2 | 微博 APP   | http://weibo.com/    | cn      |
|  3 | 淘宝 APP   | https://www.taobao.c | cn      |
|  4 | 淘宝 APP   | https://www.taobao.c | cn      |
+----+------------+----------------------+---------+
```

从 "Websites" 和 "apps" 表中选取所有不同的country（只有不同的值）

```
select country from Websites union select country from apps;
+---------+
| country |
+---------+
| USA     |
| CN      |
| IND     |
+---------+
```

使用 UNION ALL 从 "Websites" 和 "apps" 表中选取所有的country（也有重复的值）：

```
select country from Websites union all select country from apps; 
+---------+
| country |
+---------+
| USA     |
| CN      |
| CN      |
| CN      |
| USA     |
| IND     |
| cn      |
| cn      |
| cn      |
| cn      |
+---------+
```