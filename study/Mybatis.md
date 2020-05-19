
## #{} 和 ${} 的区别是什么？ 

`#{}` 会将 sql 中的 #{} 替换为？号，调用 PreparedStatement 的 set 方法来赋值。可以有效的防止 SQL 注入，提高系统安全性
`${}` 替换成变量的值

## 实体类中的属性名和表中字段名不一样

第一种方法：查询 sql 语句中定义字段名的别名，别名和实体类的属性名一致

```xml
<select id = "selectorder" parametertype = "int" resulttype="me.gacl.domain.order">
    select order_id id,order_no orderNo,order_price price from orders where order_id = #{id};
</select>
```

第二种方法：通过 <resultMap> 来映射字段名和实体类属性名一一对应的关系

```xml
<select id="getOrder" parametertype = "int" resultMap = "ordersultmap">
    select * from orders where order_id = #{id};
</select>
```

```xml
<resultMap type = "me.gacl.domain.order" id = "ordersultmap" >
    <!-- 用 id 属性来映射主键字段 -->
    <id property = "id" column = "order_id"/>

    <!-- 用 result 属性来映射非主键字段，property 为实体类属性名，column 为数据库表中的属性 -->
    <result property = "orderno" column = "order_no"></result>
    <result property = "price" column = "order_price"></result>
</resultMap>
```

## 模糊查询 like 语句该怎么写

第一种方法：Java 代码中添加 sql 通配符

```
String wildCardName = "%smi%";
list<name> names = mapper.selectlike(wildCardName);
```

```xml
<select id = "selectlike">
    select * from foo where bar like #v{value};
</select>
```

第二种方法：在 sql 语句中拼接通配符，会引起 sql 注入

```
String wildCardName = "smi"
list<name> names = mapper.selectlike(wildCardName);
```

```xml
<select id = "selectlike">
    select * from foo where bar like "%"#{value}"%";
</select>
```

## Mapper 接口的工作原理

Mapper 接口的全限名，映射文件中的 namespace 的值

Mapper 接口的方法名，映射文件中 Mapper 的 Statement 的 id 值

Mapper 接口的方法名的参数，就是传递给 sql 的参数

Mapper 接口没有实现类，当调用接口方法时，接口全限名 + 方法名拼接串作为 key 值，可以定位到 MapperStatement。

在 Mybatis 中，每一个 <select> <insert> <update> <delete> 标签，都会被解析为一个 MapperStatement 对象

举例：

com.mybatis3.mapper.StudentMapper.findStudentById，可以唯一找到 namespace 为 com.mybatis3.mappers.StudentMapper 下面 id 为 findStudentById 的 MapperStatement

## Mapper 接口的方法参数不同时方法是否能重载

Mapper 接口里的方法，是不能重载的，因为是使用全限名 + 方法名的保存和寻找策略。

## Mybatis 是如何将 sql 执行结果封装为目标对象并返回的？都有哪些映射方式？

第一种：使用 <resultMap> 标签，逐一定义数据库列名和对象属性名之间的映射关系
第二种：使用 sql 列的别名功能，将列的别名书写为对象属性名

有了列名和属性名的映射关系后，Mybatis 通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，哪些找不到映射关系的属性，是无法完成赋值的

## 如何执行批量插入

首先创建一个简单的 insert 语句：

```xml
<insert id = "insertname">
    insert into names(name) values(#{value});
</insert>
```

然后在java代码中像下面这样执行批处理插入：

```
list<String> names = new ArrayList<>();
names.add("fred");
names.add("barney");
names.add("betty");
names.add("wilma");

SqlSession sqlSession = sessionFactory.openssion(executorType.batch);
try{
    NameMapper mapper = sqlSession.getMapper(nameMapper.class);
    for (String name : names){
        mapper.insertname(name);
    }
    sqlSession.commit();
}catch(Exception e){
    e.printStackTrace();
    sqlSession.rollback();
    throw e;
}finally{
    sqlSession.close();
}
```

## 如何获取自动生成的主键值

insert 方法总是返回一个 int 值，这个值代表的是插入的行数

如果采用自增长策略，自动生成的键值在 insert 方法执行完成后可以被设置到传入的参数对象中。

```xml
<inert id = "insertname" usegeneratedkeys = "true" keyproperty = "id">
    insert into names (name) values (#{name})
   
</inert>
```

```
name name = new name();
name.setName("fred);
int rows = mapper.insertName(name);
// id 设置到对象中
int rows = mapper.insertame(name);
system.out.println("rows inserted = " + rows);
system.out.println("generated key value = " + name.getid());
```

## 在 mapper 中如何传递多个参数

第一种：mapper 接口的犯法

```
public UserselectUser(String name,String area);
```

对应的 xml，#{0} 代表接收的是 mapper 层中的第一个参数，#{1} 代表 dao 层中第二个参数，更多参数一致往后加即可

```xml
<select id = "selectUser" resultMap = "BaseResultMap">
    select * from user_user_t where user_name = #{0} and anduser_area = #{1}
</select>
```

第二种：使用 @param 注解

```
public interface usermapper{
    user selectUser(@param("username") String username,@param("hashpassword")String hashedpassword);
}
```

然后，就可以在 xml 像下面这样使用（推荐封装为一个 map，作为单个参数传递给 mapper）

```xml
<select id="selectuser" resulttype="user">
    select id,username,hashedpassword from some_table where username = #{username} and hashedpasswoed = #{hashedpassword};
</select>
```

第三种：多个参数封装成 map

```
try{
    Map<String,Obejct> map = new HashMap<>();
    map.put("start",start);
    map.put("end",end);
    return sqlSession.selectList("StudentID.pagination",map);
}catch(Exception e){
     e.printStackTrace();
     sqlSession.rollback();
     throw e;
}finally{
    MYbatisUtil.closeSqlSession();
}
```

## Mybatis 动态 sql 有什么用？执行原理？有哪些动态 sql

Mybatis 动态 sql 可以在 xml 映射文件内，以标签的形式编写动态 sql，执行原理是根据表达式的值完成逻辑判断并动态 sql 的功能

Mybatis 提供了 9 种动态 sql 标签：trim | where | set | foreach | if | choose | when | otherwise | bind

## xml 映射文件中，除了常见的slect | insert | update | delete 标签之外，还有哪些标签？

<resultMap>、<parameterMap>、<sql>、<include>、<selectKey>，加上动态 sql 的9个标签，其中<sql>为sql片段标签，通过<include> 标签引入 sql 片段，<selectKey> 为不支持自增的主键生成策略标签

## Mybatis 的 xml 映射文件中，不同的 xml 映射文件，id 是否可以重复？

不同的 xml 映射文件，如果配置了 namespace，那么 id 可以重复；如果没有配置 namespace，那么 id 不能重复

原因就是 namespace + id 是作为 Map<String，MapperStatement> 的 key 使用的，如果没有 namespace，就剩下 id，那么 id 重复会导致数据互相覆盖。有了 namespace，自然 id 就可以重复，namespace 不同，namespace + id 自然也就不同。

## 一对一、一对多的关联查询？

```
<mapper namespace = "com.lcb.mapping.userMapper">
    <!-- association 一对一关联查询-->
    <select id = "getClass" parameterType = "int" resultMap = "ClassesResultMap">
            select * from class c,teacher t where c.teacher_id = t.t_id and c.c_id = #{id};    
    </select>
    <resultMap type = "com.lcb.user.Classes" id = "ClassesResultMap">
        <id property = "id" column = "c_id"></id>
        <result proerty = "name column = "c_name"></result>
        <association property = "teacher" javaType = "com.lcb.user.Teacher"> 
            <id property = "id" column = "t_id"></id>
            <result property = "name" column = "t_name""></result>
        </association>
    </resultMap>

    <!-- collection 一对多关联查询-->
    <select id = "getClass2" parameterType = "int" resultMap = "ClassesResultMap2">
        select * from class c,teacher t,student s where c.teacher_id = t.t_id and c.c_id = s.class_id and c.c_id = #{id};
    </select>
    <resultMap type = "com.lcb.user.Classes" id = "ClassesResultMap2">
            <id property = "id" column = "c_id"></id>
            <result proerty = "name column = "c_name"></result>
            <association property = "teacher" javaType = "com.lcb.user.Teacher"> 
                <id property = "id" column = "t_id"></id>
                <result property = "name" column = "t_name""></result>
            </association>
            
            <collection property = "student" ofType = "com.lcb.user.Student">
                <id property = "id" column = "s_id"></id>
                <result property = "name" column = "s_name"></result>
            </collection>
    </resultMap>
</mapper>
```

## MyBatis 实现一对一有几种方式？具体怎么操作？

有联合查询和嵌套查询，联合查询是几个表联合查询，只查询一次，通过在 resultMap 里面配置 association 节点配置一对一的类就可以完成

嵌套查询是先差一个表，根据这个表里面的结果的外键 id，去再另外一个表里面查询数据，也是通过 association 配置，但另外一个表的查询通过 select 属性配置

## Mybatis 实现一对多有几种方式，怎么操作的？

有联合查询和嵌套查询。联合查询是几个表联合查询，只查询一次，通过在 resultMap 里面的 collection 节点配置一对多的类就可以完成；

嵌套查询是先查一个表，根据这个表里面的结果的外键，去另外一个表里面查询数据，也是通过配置 collection，但另外一个表的查询通过 select 节点配置

## 使用 MyBatis 的 mapper 接口调用时有哪些要求？

1. Mapper 接口方法名和 mapper.xml 中定义的每个 sql 的 id 相同；
2. Mapper 接口方法的输入参数类型和 mapper.xml 中定义的每个 sql 的 parameterType 的类型相同
3. Mapper 接口方法的输出参数类型和 mapper.xml 中定义的每个 sql 的 resultType 的类型相同
4. Mapper.xml 文件中的 namespace 即时 mapper 接口的类路径

## Mapper 编写有哪几种方式



