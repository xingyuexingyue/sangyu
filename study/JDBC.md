## 目录

[一、通过Driver 接口获取数据库连接]()

[二、通过DriverManager 接口获取数据库连接]()

[三、通过Statement 执行更新操作]()

[四、通过ResultSet 执行查询操作]()

[五、通过PreparedStatement 解决SQL注入]()

[六、DatabaseMetaData类 获得数据库表的相关信息]()

[七、利用反射及JDBC 元数据编写通用的查询方法]()

[八、使用beanutils 工具类操作JavaBean]()

[九、获取插入记录的主键值]()

[十、处理Blob]()

[十一、处理事务]()

[十二、事务的隔离级别]()

[十三、 批量处理]()

[十四、数据库连接池：DBCP、C3P0]()

[十五、使用DBUtils 查询、更新]()

## 一、通过Driver 接口获取数据库连接

#### 数据持久化

数据持久化，将内存中的数据存储在数据库中，包括和数据库相关的各种操作：

保存：把域对象永久保存到数据库

更新：更新数据中域对象的状态

删除：从数据库中删除一个域对象

加载：加载特定的OID，把一个域对象从数据库中加载到内存

查询：根据特定的查询条件，把符合查询条件的一个或多个域对象从数据库加载到内存中

![](https://upload-images.jianshu.io/upload_images/2765653-8090819ae8215d7d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在Java中，数据库存取技术分为基类：JDBC、JDO、第三方O/R工具，如Hibernate，ibatis等；
这些里面，JDBC是Java访问数据库的基石，JDO，Hibernate对JDBC的封装。

#### JDBC的基本介绍

1. JDBC是一个独立于特定数据库管理系统，通用的SQL数据库存取和操作的公共接口（一组API），定义了用来访问数据库的标准Java类库

2. JDBC为访问不同的数据库提供了一种统一的途径，为开发者屏蔽了一些细节问题

3. Java程序使用JDBC可以连接任何提供了JDBC驱动的程序的数据库系统

#### JDBC连接数据库进行查询步骤

第一，连接数据库

第二、执行SQL

第三，处理返回结果

![](https://upload-images.jianshu.io/upload_images/2765653-dde7adb6f771a40e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### JDBC URL

JDBC URL标识注册的驱动程序，驱动程序管理器通过URL找到对应的驱动程序，建立数据库连接

常见的JDBC URL：

Oracle数据库(jdbc:oracle:thin:@localhost:1521:sid)

MySQL数据库连接(jdbc:mysql://localhost:3306/sid)

### 通过Driver建立连接

```
// 使用前增加mysql的驱动 mysql-connector
public Connection myTest() thorws SQLException{
    // 1.创建一个Driver实现类的对象
    Driver driver = new com.mysql.jdbc.Driver(); // 根据JDBC规范，采用都是java.sql包下的内容
    // 2. 准备连接数据库的基本信息：url，user，password
    String url = "jdbc://mysql://localhost:3306/test";
    Properies info = new Properties();
    info.put("user","root");  
    info.put("password","root");
    // 3. 调用Driver接口的connection(url,info)获取数据连接
    Connection connection = driver.connection(url,info);
    return connection;
}
```

```
// 优化增加配置文件jdbc.properties
// 将数据库相关的url、user、password、mysql的驱动放到一个配置文件中
// 通过修改配置文件的方式实现和具体的数据库解耦。
public Connection myTest01() throws Exception{
    
    String driverClass = null;
    String jdbcUrl = null;
    String user = null;
    String password = null;
    // 读取类路径下的jdbc.properties 文件
    InputStream in = getClass().getClassLoader().getResourceAsStream("jdbc.properties")
    Properties properties = new Properties();
    properties.load(in);
    driverClass = properties.getProperty("driver");
    jdbcUrl = properties.getProperty("jdbcUrl");
    user = properties.getProperty("user");
    password = properties.getProperty("password");
    // 通过反射创建Driver对象
    Driver driver = (Driver) Class.forName(driverClass).newInstance();
    // 通过Driver的connect方法获取数据库连接
    Connection connection = driver.connect(jdbcUrl,info);
    return connection;
}
```
## 二、通过DriverManager 接口获取数据库连接

JDBC接口（API）提供了一套纯碎的JAVA API给应用程序开发者，应用程序开发者借助于API用于开发可以访问数据库的程序、提供了一套低级别的JDBC dirver API 给数据库驱动开发者，驱动开发者借助于API提供服务到JDBC

提供给数据库驱动开发者的API正好是为了实现提供给应用程序开发者的这套API。这是因为JDBC是对数据库操作访问的薄层封装，应用程序开发者借助于JDBC可以实现
对数据库的操作访问，但是，最终提供的服务仍旧是数据库实现了具体SQL的执行

所以JDBC提供给应用程序开发者的API就是开发者使用JDBC数据库的接口而提供给数据库驱动开发者
的API则恰恰是为了让数据库驱动开发者来提供服务


```
public Connection myTest01() throws Exception{
    // 1.准备连接数据库的4个字符串
    // 驱动的全类名
    String driverClass = null;
    // JDBC URL
    String jdbcUrl = null;
    // user
    String user = null;
    // password
    String password = null;
    // 读取类路径下的jdbc.properties 文件
    InputStream in = getClass().getClassLoader().getResourceAsStream("jdbc.properties");
    Properties properties = new Properties();
    properties.load(in);
    driverClass = properties.getProperty("driver");
    jdbcUrl = properties.getProperty("jdbcUrl");
    user = properties.getProperty("user");
    password = properties.getProperty("password");
    // 2. 加载数据库驱动程序
    Class.forName(driverClass);
    // 3. 通过DriverManager 的getConnection()方法获取数据库连接
    Connection connection = DriverManager.getConnection(jdbcUrl,user,password);
    return connection;
}

```

注册驱动的两种写法


第一种写法：DriverManager.registerDriver(Class.forName(driverClass).newInstance);



第二种写法: Class.forName(driverClass); 

在加载驱动的时，com.mysql.cj.jdbc.Driver中有静态代码块会被执行，静态代码块创建了当前类的实例，注册到了DriverManager
```
public class Driver extends NonRegisteringDriver implements java.sql.Driver {
    public Driver() throws SQLException {
    }
    static {
        try {
            DriverManager.registerDriver(new Driver());
        } catch (SQLException var1) {
            throw new RuntimeException("Can't register driver!");
        }
    }
} 
```

## 三、通过Statement 执行更新操作

```
// 通过Statement 向表中插入一条记录（update、delete可以通过调用Statement对象的executeUpdate()方法来执行对应的删除和更新操作）
class MyTest{
     // 获取数据库连接
    public Connection myConnection() throws Exception{
        String driverClass = "com.mysql.jdbc.Driver";
        String jdbcUrl = "jdbc:mysql://localhost:3306/mydb";
        String user = "user";
        String password = "password";

        Class.forName(driverClass);
        Connection connection= DriverManager.getConnection(jdbcUrl,user,password);
        return connection;
     }     
    public void myStatement() throws SQLException{
        Connection conn = null;
        Statement statement = null;
        try{
            // 1. 获取数据库连接
            conn = myConnection();
            // 2. 准备执行的SQL
            String sql = "Insert into table(name,email,birth) values('xyz','xyz@123.com','xxxx-xx-xx')";
            // 3. 执行SQL（注意执行的SQL可以是INSERT、UPDATE或DELETE。但不能是SELECT）
            // 1）获取操作SQL语句的Statement对象
            // 通过调用Connection的createStatement()方法来获取
            statement = conn.createStatement()'
            // 2）调用Statement对象的executeUpdate(sql)执行SQL语句进行插入
            statement.executeUpdate(sql);
        }catch(Exception e){
             e.printStackTrace();
        }finally{
              // 关闭Statement对象
              if(statement != null){
                  try{
                      statement.close()
                  }catch(Exception e2){
                      e2.printStackTrace();
                  }
              }
              // 关闭连接
              if(conn != null){
                  try{
                      conn.close()
                  }catch(Exception e2){
                      e2.printStackTrace();
                  }
              }        
        }
    }
}    
```

## 四、通过ResultSet 执行查询操作

对数据库的查询操作，一般需要返回查询结果，在程序中，JDBC为我们提供了ResultSet接口来专门处理查询结果集

使用ResultSet的步骤：

1. 加载数据库驱动程序：Class.forName(驱动程序类)

2. 通过用户名密码和连接地址获取数据库连接对象：DriverManager.getConnection(连接地址,用户名,密码)

3. 构造查询SQL语句

4. 调用Statement 对象的executeQuery(sql) 可以得到结果集

5. resultSet 实际上返回的就是一张数据表。有一个指针指向数据表的第一行的前面,调用next()方法检测下一行是够有效。若有效该方法返回true，且指针下移。相当于Interator对象的hasNext()和next()方法的结合体;
当指针定位到一行时，可以通过getXxx(index)或getXxx(columnName) 获得每一列的值。例如：getInt(1),getString("name");

6. 处理结果

7. ResultSet 也需要关闭资源

```
// 表结构
create database mydb; # 创建数据库

use mydb；#使用数据库

create table customer_table( #创建分类表
id int PRIMARY KEY AUTO_INCREMENT,  
name varchar(100),
age varchar(100),
birth DATE
);
```

```
class MyTest {
    // 关闭数据库资源(注意关闭要从里到外)
    public void releaseDB(ResultSet resultSet, Statement statement, Connection connection) {
        if (resultSet != null) {
            try {
                resultSet.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        if (statement != null) {
            try {
                statement.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
        if (connection != null) {
            try {
                connection.close();
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }

    // 获取数据库连接
    public Connection myConnection() throws Exception {
        String driverClass = "com.mysql.jdbc.Driver";
        String jdbcUrl = "jdbc:mysql://localhost:3306/mydb";
        String user = "user";
        String password = "password";

        Class.forName(driverClass);
        Connection connection = DriverManager.getConnection(jdbcUrl, user, password);
        return connection;
    }
    public void  testResultSet(){
        Connection conn = null;
        Statement statement = null;
        ResultSet rs = null;
        try{
            // 1. 获得Connection
            conn = myConnection();
            // 2. 获取Statement
            statement = conn.createStatement();
            // 3. 准备SQL
            String sql = "select id,name,email,birth from customers where id = 4";
            // 4. 执行查询，得到ResultSet
            rs = statement.executeQuery(sql);
            // 5. 处理ResultSet
            while(rs.next()){
                int id = rs.getInt(1);
                String name = rs.getString("name");
                String email = rs.getString(3);
                Date birth = rs.getData(4);
                System.out.println(id);
                System.out.println(name);
                System.out.println(email);
                System.out.println(birth);
            }
        }catch(Exception e){
            e.printStackTrace();
        }finally{
            releaseDB.release(rs,statement,conn);
        }
    }

    // 可以执行的sql：update、insert、delete
    public void myStatement() throws SQLException {
        Connection conn = null;
        Statement statement = null;
        try {
            // 1. 获取数据库连接
            conn = myConnection();
            // 2. 准备执行的SQL
            String sql = "Insert into table(name,email,birth) values('xyz','xyz@123.com','xxxx-xx-xx')";
            // 3. 执行SQL（注意执行的SQL可以是INSERT、UPDATE或DELETE。但不能是SELECT）
            // 1）获取操作SQL语句的Statement对象
            // 通过调用Connection的createStatement()方法来获取
            statement = conn.createStatement();
            // 2）调用Statement对象的executeUpdate(sql)执行SQL语句进行插入
            statement.executeUpdate(sql);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            if (statement != null) {
                try {
                    statement.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

### ResultSetMetaData类

利用ResultSet的getMetaData的方法可以获得ResultSetMetaData对象，ResultSetMetaData存储了 ResultSet对象中列的类型和属性信息的对象。

常见API

```
// 方法说明：获取指定列的名称
getColumnName(int column)：
// 方法说明：返回当前ResultSet对象中的列数
getColumnCount()：
// 获取用于打印输出和显示的指定列的建议标题。
String getColumnLabel(int column)
```

```
public void myTest01() throws ClassNotFoundException, SQLException {
    String driverClass = "com.mysql.jdbc.Driver";
    String jdbcUrl = null;
    String user = null;
    String password = null;
    Class.forName(driverClass);
    Connection connection = DriverManager.getConnection(jdbcUrl, user, password);
    String sql = "SELECT flow_id flowId, type, id_card idCard, "
                + "exam_card examCard, student_name studentName, "
                + "location, grade " + "FROM examstudent WHERE flow_id = ?";
    PreparedStatement preparedStatement = null;
    ResultSet resultSet = null;
    preparedStatement = connection.prepareStatement(sql);
    preparedStatement.setInt(1, 5);
    resultSet = preparedStatement.executeQuery();
    ResultSetMetaData rsmd = resultSet.getMetaData();
    String columnName = rsmd.getColumnName(1); // 获取指定列的名称
    int columCount = rsmd.getColumnCount();// 返回当前ResultSet对象中的列数
    String columnLabel= rsmd.getColumnLabel(1);//获取用于打印输出和显示的指定列的建议标题。
    }

```

## 五、通过PreparedStatement 解决SQL注入

### 常见的SQL注入

1. 数字注入

在浏览器地址栏输入：test.com/sql/article.php?id=1，这是请求方式为get的接口，发送这个请求相当于调用一个查询语句

```$sql = "select * from article where id = ",$id```

正常情况下，应该返回id=1的文章信息，但是，如果在浏览器地址栏输入test.com/sql/article.php?id=-1 OR 1 = 1，这就是一个SQL注入攻击了，可能会返回所有文章的相关信息。产生这种情况的原因是，id=-1 永远是false，1=1永远是true，所以整个where语句永远是true，相当于没有加where条件，所以查询的条件相当于是整张表的内容

2. 字符串注入

常见的用户登录场景：输入用户名和密码，提交。

这是一个post请求，登录时调用接口test.com/sql/login.html，sql的查询过程：首先连接数据库，然后后台对post请求参数中的用户名、密码进行参数校验。假如此时输入用户名和密码为user和123456，提交，相当于调用了以下的SQL语句：

```select * from user where username = 'user' and password = '123456'```

1）用户名输入：```user'#```，密码随意输入，如：111，然后提交。此时SQL语句是：

```select * from user where username = 'user'#' and assword = '111'```

```#```后面被注释了，实际执行的sql是：

```select * from user where username = 'user'```

2）用户名输入：```user'--```，密码随意输入，如：111

```select * from user where username = 'user'--' and assword = '111'```

```--```后面被注释了，实际执行的sql是：

```select * from user where username = 'user'```

### PreparedStatement 防止SQL注入

1. PreparedStatement是Statement的子接口，可以传入带占位符的SQL语句，并且提供了补充占位符变量的方法。

2. PreparedStatement能最大可能提高性能：**DBServer会对预编译语句提供性能优化。因为预编译语句有可能被重复调用，所以语句在被DBServer的编译器编译后的执行代码被缓存下来，那么下次调用时，只要是相同的预编译语句就不需要编译，只要将参数直接传入编译过的语句执行代码中就会得到执行。**但在Statement语句中，即使是相同操作但因为数据内容不一样，所以整个语句本身不能匹配，没有缓存语句的意义，实事实是没有数据库会对普通语句编译后的执行代码缓存，这样每执行一次都要对传入的语句编译一次。

```
class MyTest{
    // 更新 删除 添加
    public void testPreparedStatement(){
        Class.forName("com.mysql.jdbc.Driver");
        String url = "jdbc:mysql://localhost:3306/mydb";
        Connection connection = null;
        PreparedStatement preparedStatement = null;
        try{
            connection = DriverManager.getConnection(url,"root", "root");
            String sql = "Insert into customers(name,email,birth) values(?,?,?)"
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setString(1,"test");
            preparedStatement.setString(2,"test@qq.com");
            preparedStatement.setString(2,"test@qq.com");
            preparedStatement.setDate(3,new Date(new java.util.Date().getTime()));
            preparedStatement.executeUpdate();
        }catch(Exception e){
            e.printStackTrace();
        }finally{
            preparedStatement.close();
            connection.close();
        }
    }
    // 查询
    public void testPreparedStatement01(){
        Class.forName("com.mysql.jdbc.Driver");
        String url = "jdbc:mysql://localhost:3306/mydb";
        String username = "user";
        String password = "123456"
        String sql = "select * from users where username = ?" + "and password = ?"
        Connection connection = null;
        PreparedStatement preparesStatement = null;
        ResultSet resultSet = null;
        try{
            conncection = DriverManager.getConnection(url,"root", "root");
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.setString(1,username);
            preparedStatement.setString(2,password);
            resultSet = preparedStatement.executeQuery();
            if(resultSet.next()){
              System.out.println("success");
            }else{
              System.out.println("fail");
            }
        }catch(Exception e){
            e.printStackTrace();
        }finally{
            resultSet.close();
            preparedStatement.close();
            connection.close();
        }
    }
}
```

## 六、DatabaseMetaData类 获得数据库表的相关信息

Java 通过JDBC获取连接以后，得到一个Connection对象，可以从这个对象获取有关数据库管理系统的各种信息，包括数据库中的各个表，表中的各个列，数据类型，触发器，存储过程等各方面的信息。获取这些信息的方法都是在DatabaseMetaData类的对象上实现的，而且DatabaseMetaData对象是在Connection对象上获得的

**DatabaseMetaData类API**

```
getURL()：返回一个String对象，代表数据库的URL
getUserName()：返回连接当前数据库管理系统的用户名
isReadOnly()：返回一个boolean，指示数据库是否只允许读操作
getDatabaseProductName()：返回数据库的产品名称
getDatabaseProductVersion()：返回数据库的版本号
getDriverName()：返回驱动程序的名称
getDriverVersion()：返回驱动程序的版本号
```
```
public void myTest() throws ClassNotFoundException, SQLException {
    String driverClass = "com.mysql.jdbc.Driver";
    String jdbcUrl = null;
    String user = null;
    String password = null;
    Class.forName(driverClass);
    Connection connection = DriverManager.getConnection(jdbcUrl, user, password);
    DatabaseMetaData databaseMetaData = connection.getMetaData();
    // 代表数据库的URL
    String url = databaseMetaData.getURL();
    System.out.println(url);
    //返回连接当前数据库管理系统的用户名
    String userName = databaseMetaData.getUserName();
    System.out.println(userName);
    // 返回一个boolean，指示数据库是否只允许读操作
    Boolean isRead = databaseMetaData.isReadOnly();
    System.out.println(isRead);        
    // 返回数据库的产品名称
    String productName = databaseMetaData.getDatabaseProductName();
    System.out.println(productName);
    // 返回数据库的版本号
    String productVersion = databaseMetaData.getDatabaseProductVersion();
    System.out.println(productVersion);        
    // 返回驱动程序的名称
    String driverName = databaseMetaData.getDriverName();
    System.out.println(driverName);
    // 返回驱动程序的版本号
    String driverVersion = databaseMetaData.getDriverVersion();
    System.out.println(driverVersion);
}
```


## 七、利用反射及JDBC 元数据编写通用的查询方法

```
public class MyTest {
    public static void test01() throws ClassNotFoundException, SQLException, IllegalAccessException, InstantiationException {
        String driverClass = "com.mysql.jdbc.Driver";
        String jdbcUrl = "jdbc:mysql://localhost:3306/myemployees?useUnicode=true&useSSL=false";
        String user = "root";
        String password = "abcd123456";

        ResultSet resultSet = null;
        Class.forName(driverClass);
        Connection connection = DriverManager.getConnection(jdbcUrl,user,password);
        String sql = "SELECT flow_id flowId, type, id_card idCard, "
                + "exam_card examCard, student_name studentName, "
                + "location, grade " + "FROM examstudent WHERE flow_id = ?";

        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        preparedStatement.setInt(1,3);
        resultSet = preparedStatement.executeQuery();
        Map<String,Object> values = new HashMap<>();

        ResultSetMetaData rsmd = resultSet.getMetaData();
        while (resultSet.next()){
            for(int i = 0; i < rsmd.getColumnCount();i++){
                String columnLabel = rsmd.getColumnLabel(i+1);
                Object columnValue = resultSet.getObject(columnLabel);
                values.put(columnLabel,columnValue);
            }
        }

        Class clazz = Student.class;
        Object object = clazz.newInstance();
        for(Map.Entry<String,Object> entry : values.entrySet()){
            String fieldName = entry.getKey();
            Object fieldValue = entry.getValue();
            ReflectionUtils.setFieldValue(object,fieldName,fieldValue);
        }

        System.out.println(object);
        resultSet.close();
        preparedStatement.close();
        connection.close();
    }

    public static void main(String[] args) {
        try {
            test01();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InstantiationException e) {
            e.printStackTrace();
        }
    }
}
```

```
//Student类
public class Student {
    private long flowId;
    private Integer type;
    private String idCard;
    private String examCard;
    private String studentName;
    private String location;
    private Integer grade;

    public long getFlowId() {
        return flowId;
    }

    public int getGrade() {
        return grade;
    }

    public int getType() {
        return type;
    }

    public String getExamCard() {
        return examCard;
    }

    public String getLocation() {
        return location;
    }

    public String getIdCard() {
        return idCard;
    }

    public String getStudentName() {
        return studentName;
    }

    public void setExamCard(String examCard) {
        this.examCard = examCard;
    }

    public void setFlowId(int flowId) {
        this.flowId = flowId;
    }

    public void setIdCard(String idCard) {
        this.idCard = idCard;
    }

    public void setGrade(int grade) {
        this.grade = grade;
    }

    public void setLocation(String location) {
        this.location = location;
    }

    public void setStudentName(String studentName) {
        this.studentName = studentName;
    }

    public void setType(int type) {
        this.type = type;
    }

    @Override
    public String toString() {
        return "Student{" +
                "flowId=" + flowId +
                ", type=" + type +
                ", idCard='" + idCard + '\'' +
                ", examCard='" + examCard + '\'' +
                ", studentName='" + studentName + '\'' +
                ", location='" + location + '\'' +
                ", grade=" + grade +
                '}';
    }

    public Student(int flowId, int type, String idCard, String examCard,
                   String studentName, String location, int grade) {
        super();
        this.flowId = flowId;
        this.type = type;
        this.idCard = idCard;
        this.examCard = examCard;
        this.studentName = studentName;
        this.location = location;
        this.grade = grade;
    }
    public Student() {
    }
}
```

```
CREATE TABLE IF NOT EXISTS `examstudent`(`flow_id` INT UNSIGNED AUTO_INCREMENT,    `type` INT NOT NULL,    `id_card` VARCHAR(40) NOT NULL,    `exam_card` VARCHAR(40) NOT NULL,    `student_name` VARCHAR(40) NOT NULL,    `location` VARCHAR(40) NOT NULL,    `grade` INT NOT NULL,    PRIMARY KEY ( `flow_id` ) )ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
```
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
import java.lang.reflect.ParameterizedType;
import java.lang.reflect.Type;

/**
 * 反射的 Utils 函数集合
 * 提供访问私有变量, 获取泛型类型 Class, 提取集合中元素属性等 Utils 函数
 * @author Administrator
 *
 */
public class ReflectionUtils {


    /**
     * 通过反射, 获得定义 Class 时声明的父类的泛型参数的类型
     * 如: public EmployeeDao extends BaseDao<Employee, String>
     * @param clazz
     * @param index
     * @return
     */
    @SuppressWarnings("unchecked")
    public static Class getSuperClassGenricType(Class clazz, int index){
        Type genType = clazz.getGenericSuperclass();

        if(!(genType instanceof ParameterizedType)){
            return Object.class;
        }

        Type [] params = ((ParameterizedType)genType).getActualTypeArguments();

        if(index >= params.length || index < 0){
            return Object.class;
        }

        if(!(params[index] instanceof Class)){
            return Object.class;
        }

        return (Class) params[index];
    }

    /**
     * 通过反射, 获得 Class 定义中声明的父类的泛型参数类型
     * 如: public EmployeeDao extends BaseDao<Employee, String>
     * @param <T>
     * @param clazz
     * @return
     */
    @SuppressWarnings("unchecked")
    public static<T> Class<T> getSuperGenericType(Class clazz){
        return getSuperClassGenricType(clazz, 0);
    }

    /**
     * 循环向上转型, 获取对象的 DeclaredMethod
     * @param object
     * @param methodName
     * @param parameterTypes
     * @return
     */
    public static Method getDeclaredMethod(Object object, String methodName, Class<?>[] parameterTypes){

        for(Class<?> superClass = object.getClass(); superClass != Object.class; superClass = superClass.getSuperclass()){
            try {
                //superClass.getMethod(methodName, parameterTypes);
                return superClass.getDeclaredMethod(methodName, parameterTypes);
            } catch (NoSuchMethodException e) {
                //Method 不在当前类定义, 继续向上转型
            }
            //..
        }

        return null;
    }

    /**
     * 使 filed 变为可访问
     * @param field
     */
    public static void makeAccessible(Field field){
        if(!Modifier.isPublic(field.getModifiers())){
            field.setAccessible(true);
        }
    }

    /**
     * 循环向上转型, 获取对象的 DeclaredField
     * @param object
     * @param filedName
     * @return
     */
    public static Field getDeclaredField(Object object, String filedName){

        for(Class<?> superClass = object.getClass(); superClass != Object.class; superClass = superClass.getSuperclass()){
            try {
                return superClass.getDeclaredField(filedName);
            } catch (NoSuchFieldException e) {
                //Field 不在当前类定义, 继续向上转型
            }
        }
        return null;
    }

    /**
     * 直接调用对象方法, 而忽略修饰符(private, protected)
     * @param object
     * @param methodName
     * @param parameterTypes
     * @param parameters
     * @return
     * @throws InvocationTargetException
     * @throws IllegalArgumentException
     */
    public static Object invokeMethod(Object object, String methodName, Class<?> [] parameterTypes,
                                      Object [] parameters) throws InvocationTargetException{

        Method method = getDeclaredMethod(object, methodName, parameterTypes);

        if(method == null){
            throw new IllegalArgumentException("Could not find method [" + methodName + "] on target [" + object + "]");
        }

        method.setAccessible(true);

        try {
            return method.invoke(object, parameters);
        } catch(IllegalAccessException e) {
            System.out.println("不可能抛出的异常");
        }

        return null;
    }

    /**
     * 直接设置对象属性值, 忽略 private/protected 修饰符, 也不经过 setter
     * @param object
     * @param fieldName
     * @param value
     */
    public static void setFieldValue(Object object, String fieldName, Object value){
        Field field = getDeclaredField(object, fieldName);

        if (field == null)
            throw new IllegalArgumentException("Could not find field [" + fieldName + "] on target [" + object + "]");

        makeAccessible(field);

        try {
            field.set(object, value);
        } catch (IllegalAccessException e) {
            System.out.println("不可能抛出的异常");
        } catch (Exception e){
            System.out.println(e);
        }
    }

    /**
     * 直接读取对象的属性值, 忽略 private/protected 修饰符, 也不经过 getter
     * @param object
     * @param fieldName
     * @return
     */
    public static Object getFieldValue(Object object, String fieldName){
        Field field = getDeclaredField(object, fieldName);

        if (field == null)
            throw new IllegalArgumentException("Could not find field [" + fieldName + "] on target [" + object + "]");

        makeAccessible(field);

        Object result = null;

        try {
            result = field.get(object);
        } catch (IllegalAccessException e) {
            System.out.println("不可能抛出的异常");
        }

        return result;
    }
}
```

## 八、使用beanutils 工具类操作JavaBean

有两种对象赋值的方式：一种是使用反射为对象赋值， **另一种通过beanutils方式赋值**

在JavaEE中，Java类的属性的通过getter，setter来定义；get（或set）方法，去除get（或set）后，后字母小写即为Java类的成员变量或字段。

操作Java类的属性有一个工具包：beanutils

```
setProperty();// 给对象的成员变量赋值
getProperty();// 获取对象成员变量的值
```
例子
```
import org.apache.commons.beanutils.BeanUtils;
import java.lang.reflect.InvocationTargetException;

public class BeanUtilsTest {
    public static void testGetProperty() throws IllegalAccessException, InvocationTargetException, NoSuchMethodException{
        Object object = new Student();
        BeanUtils.setProperty(object, "idCard", "211121196509091876");
        System.out.println(object);
        Object val = BeanUtils.getProperty(object, "idCard");
        System.out.println(val);
    }
    public static void testSetProperty() throws IllegalAccessException, InvocationTargetException {
        Object object = new Student();
        BeanUtils.setProperty(object, "idCard", "211121196509091879");
        System.out.println(object);
    }

    public static void main(String[] args){
        try {
            testGetProperty();
            testSetProperty();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        }
    }
}
```

## 九、获取插入记录的主键值

```java
import java.sql.*;

public class JDBCTest03 {
    public static void testGetKeyValue() throws ClassNotFoundException, SQLException, SQLException {
        String sql = "INSERT INTO examstudent(type,id_card, exam_card, student_name,location,grade)"
                + "VALUES(?,?,?,?,?,?)";
        String driverClass = "com.mysql.jdbc.Driver";
        String jdbcUrl = "jdbc:mysql://localhost:3306/myemployees?useUnicode=true&useSSL=false";
        String user = "root";
        String password = "abcd123456";
        Class.forName(driverClass);
        Connection connection = DriverManager.getConnection(jdbcUrl,user,password);
        // 返回主键核心代码，preparedStatement(）重载方法
        PreparedStatement preparedStatement = connection.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);
        preparedStatement.setInt(1,5);
        preparedStatement.setString(2,"1234567890");
        preparedStatement.setString(3,"12345");
        preparedStatement.setString(4,"ee");
        preparedStatement.setString(5,"SH");
        preparedStatement.setInt(6,10);
        preparedStatement.executeUpdate();
        // 通过getGeneratedKeys()获取包含了新恒诚的主键的ResultSet对象
        // 在ResultSet中只有1列 GENERATED_KEY，用于存放新生成的主键值
        ResultSet rs = preparedStatement.getGeneratedKeys();
        if(rs.next()){
            System.out.println(rs.getObject(1));
        }
        ResultSetMetaData rsmd = rs.getMetaData();
        for(int i = 0; i < rsmd.getColumnCount();i++){
            System.out.println(rsmd.getColumnName(i + 1));
        }
        rs.close();
        preparedStatement.close();
        connection.close();
    }

    public static void main(String[] args) throws SQLException, ClassNotFoundException {
        testGetKeyValue();
    }
}
```

## 十、处理Blob

Mysql中，Blob是一个二进制大型对象，是一个可以存储大量数据的容器，它能容纳不同大小的数据

MySQL 的四种Blob类型：(除了在存储的最大信息量上不同外，它们是等同的，如果存储的文件过大，数据库的性能会下降)
|类型|大小(单位：字节)|
|------|-------------|
|TinyBlob|最大 255byte|
|Blob|最大 65k|
|MediumBlob|最大 16M|
|LongBlob|最大 4G|

```
public class JDBCTest03 {
    // 插入图片，在数据库设置对应图片字段的Blob类型
    // 插入Blob类型的数据必须使用PreparedStatement，因为Blob类型的数据无法使用字符串拼写
    public void testInsertBlob() throws ClassNotFoundException, SQLException, FileNotFoundException {
        String sql = "INSERT INTO customers(name, email, birth, picture)"
                + "VALUES(?,?,?,?)";
        String driverClass = "com.mysql.jdbc.Driver";
        String jdbcurl = "";
        Class.forName(driverClass);
        Connection connection = DriverManager.getConnection(jdbcurl,"user","password");
        PreparedStatement preparedStatement = connection.prepareStatement(sql);

        InputStream inputStream = new FileInputStream("picture.jpg");
        preparedStatement.setBlob(4,inputStream);
        preparedStatement.executeUpdate();

        preparedStatement.close();
        connection.close();
    }

    // 读取图片
    // 读取blob数据：
    // 1. 使用getBlob方法读取到Blob对象
    // 2.调用Blob的getBinaryStream()方法得到输入流。再使用IO操作即可
    public void readBlob() throws ClassNotFoundException, SQLException, IOException {
        String sql = "SELECT id, name customerName, email, birth, picture "
                + "FROM customers WHERE id = 13";
        String driverClass = "com.mysql.jdbc.Driver";
        String jdbcurl = "";
        Class.forName(driverClass);
        Connection connection = DriverManager.getConnection(jdbcurl,"user","password");
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        ResultSet resultSet = preparedStatement.executeQuery();
        if(resultSet.next()){
            int id = resultSet.getInt(1);
            String name = resultSet.getString(2);
            String email = resultSet.getString(3);
            Blob picture = resultSet.getBlob(5);

            InputStream in = picture.getBinaryStream();

            OutputStream out = new FileOutputStream("newPicture.jpg");
            byte[] buffer = new byte[1024];
            int len = 0;
            while ((len = in.read(buffer)) != -1){
                out.write(buffer,0,len);
            }
            in.close();
            out.close();
        }
        resultSet.close();
        preparedStatement.close();
        connection.close();
    }    
}
```

## 十一、处理事务

### 数据库事务

1）在数据库中，所谓事务是指一组逻辑操作单元，使数据从一种状态变换到另一种状态。

2）为确保数据库中数据的一致性，数据的操纵应该是离散的成组的逻辑单元：当它全部完成时，数据的一致性可以保持，而当这个单元中的一部分操作失败，整个事务应全部视为错误，所有从起始点以后的操作应全部回退到开始状态

3）事务的操作：先定义开始一个事务，然后对数据做修改操作，这时如果提交(COMMIT)，这些修改就永久地保存下来，如果回退(ROLLBACK)，数据库管理系统将放弃所做的所有修改而回到开始事务时的状态。

4）事务的ACID(acid)属性
**原子性：**原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。
**一致性：**事务必须使数据库从一个一致性状态变换到另外一个一致性状态
**隔离性：**事务的隔离性是指一个事务的执行不能被其他事务干扰，即一个事务内部的操作及使用的数据对兵法的其他事务是隔离的，并发执行的各个事务之间不能互相干扰
**持久性：**持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来的其他操作和数据库故障不应该对其有任何影响

### JDBC 事务处理

1）事务：指构成单个逻辑工作单元的操作集合
2）事务处理：保证所有事务都作为一个工作单元来执行，即使出现了故障，都不能改变这种执行方式。当在一个事务中执行多个操作时，要么所有的事务都被提交(commit)，要么整个事务回滚(rollback)到最初状态
3）当一个连接对象被创建时，默认情况下是自动提交事务：每次执行一个SQL语句时，如果执行成功，就会向数据库自动提交，而不能回滚
4）为了让多个SQL语句作为一个事务执行：
    - 调用Connection对象的setAutoCommit(false)；以取消自动提交事务
    - 在所有的SQL语句都成功执行后，调用commit()方法提交事务
    - 在出现异常时，调用rollback()方法回滚事务

**举个例子**
```
public class JDBCTest04 {
    /**
     * 违反事务一致性
     * A 给 B 汇款 500 元
     */   
    public void testTransaction() throws SQLException, ClassNotFoundException {
        String driverClass = "com.mysql.jdbc.Driver";
        String jdbcurl = "";
        Connection connection = null;
        Class.forName(driverClass);
        connection = DriverManager.getConnection(jdbcurl,"user","password");
        PreparedStatement preparedStatement = null;
        String sql = "UPDATE users SET balance = " + "balance - 500 WHERE id = 1"; // A 账号 - 500
        preparedStatement =  connection.prepareStatement(sql);
        preparedStatement.executeUpdate();
        int i = 10 / 0; // 第一条sql执行完成A账号-500后，执行到这里报错导致第二条sql没有执行，从而违反了数据的一致性
        System.out.println(i);
        sql = "UPDATE users SET balance = " + "balance + 500 WHERE id = 2";// B 账号 + 500
        connection = DriverManager.getConnection(jdbcurl,"user","password");
        preparedStatement = connection.prepareStatement(sql);
        preparedStatement.executeUpdate();
    }
}
```

```
public class JDBCTest04 {   
    /**
     * 保证事务一致性
     * A 给 B 汇款 500 元
     * 1. 如果多个操作，每个操作使用的是自己的单独的连接，则无法保证事务
     * 2. 具体步骤：
     * 1）事务操作开始前，开始事务：取消connection的默认提交行为
     * connection.setAutoCommit(false)
     * 2）如果事务的操作都成功，则提交：connection.commit();
     * 3）回滚事务：若出现异常，则在catch块中回滚事务
     */
    public void testTransaction01() throws SQLException {
        String driverClass = "com.mysql.jdbc.Driver";
        String jdbcurl = "";

        PreparedStatement preparedStatement = null;
        Connection connection = null;
        try {
            Class.forName(driverClass);
            connection = DriverManager.getConnection(jdbcurl,"user","password");
            connection.setAutoCommit(false);
            String sql = "UPDATE users SET balance = " + "balance - 500 WHERE id = 1";
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.executeUpdate();
            int i = 10 / 0;
            sql = "UPDATE users SET balance = " + "balance + 500 WHERE id = 2";
            preparedStatement = connection.prepareStatement(sql);
            preparedStatement.executeUpdate();
            connection.commit();
        }catch (Exception e){
            e.printStackTrace();
            try {
                connection.rollback();
            }catch (Exception e1){
                e.printStackTrace();
            }
        }finally {
            preparedStatement.close();
            connection.close();
        }
    }
}
```

## 十二、事务的隔离级别

### 数据库的隔离级别

**1.**  对于同时运行的多个事务，当这些事务访问数据库中相同的数据时，如果没有采取必要的隔离机制，就会导致各种并发问题

  1）脏读：对于两个事务T1,T2，T1读取了已经被T2更新但还没有被提交的字段之后，若T2回滚，T1读取的内容就是临时且无效的

  2）不可重复度：对于两个事务T1,T2，T1读取了一个字段，然后T2更新了该字段，之后，T1再次读取同一个字段，值就不同了

  3）幻读：对于两个事务T1,T2，T1从一个表中读取了一个读取一个字段，然后T2在该表中插入了一些新的行，之后，如果T1再次读取同一个表，就会多出几行。

**2.** 数据库事务的隔离性：数据库系统必须具有隔离并发运行各个事务的能力，使它们不会相互影响，避免各种并发问题

**3.** 一个事务与其他事务隔离的程度称为隔离级别。数据库规定了多种事务隔离级别，不同隔离级别对应不同的干扰程度，隔离级别越高，数据一致性就越好，但并发性越弱

**4.** 数据库提供的4种事务隔离级别：

|  隔离级别| 描述|
| ------| -----|
| READ UNCOMMITED(读未提交数据)| 允许事务读取未被其他事务提交的变更，脏读，不可重复读和幻读的问题都会出现|
| READ COMMITED(读已提交数据)| 只允许事务读取已经被其它事务提交的变更，可以避免脏读，但不可重复读和幻读问题仍然可能出现|
| REPEATABLE READ(可重复读)| 确保事务可以多次从一个字段中读取相同的值，在这个事务持续期间，禁止其它事务对这个字段进行更新，可以避免脏读和不可重复读，但幻读的问题仍然存在|
|SERIALIZABLE(串行化)| 确保事务可以从一个表中读取相同的行，在这个事务持续期间，禁止其它事务对该表执行插入，更新和删除操作，所有并发问题都可以避免，但性能十分低下|

**5.** MySql支持4种事务隔离级别，Mysql默认的事务隔离级别：REPEATABLE READ

### 在程序中设置隔离级别

```
import java.sql.*;

public class JDBCTest05 {
    public void myTest() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.jdbc.Driver");
        String url = "jdbc:mysql://localhost:3306/mydb";
        String sql = "SELECT balance FROM users WHERE id = ?";
        Connection connection = DriverManager.getConnection(url,"user","password");
        connection.setTransactionIsolation(Connection.TRANSACTION_READ_UNCOMMITTED);// 设置隔离级别
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        preparedStatement.setInt(1,1);
        ResultSet resultSet = preparedStatement.executeQuery();
        System.out.println(resultSet);
    }
}
```

### 在Mysql中设置隔离级别
1）每启动一个mysql程序，就会获得一个单独的数据库连接，每个数据库连接都有一个全局变量
```@@tx_isolation``` 表示当前的事务隔离级别

2）查看当前的隔离级别：```SELECT @@tx_isolation``` 

3）设置当前mySQL连接的隔离级别：```set transaction isolation level read committed``` 

4）设置数据库系统的全局的隔离级别：```set global transaction isolation level read committed``` 

## 十三、 批量处理

1）当需要成批插入或者更新记录时，可以采用Java的批量更新机制，这一机制允许多条语句一次性提交给数据批量处理。通常情况下比单独提交处理更有效率

2）JDBC的批量处理语句包括下面两个方法：
```addBatch(String)```添加需要批量处理的SQL语句或参数
```executeBatch()```执行批量处理语句
```clearBatch()``` 清空SQL

3）通常我们会遇到两种批量执行SQL语句的情况：多条SQL语句的批量处理、️一个SQL语句的批量传参

### 多条SQL语句的批量处理
```
public class JDBCTest05 {

    // 使用Statement的addBatch()批处理
    public void testBatchWithStatement() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.jdbc.Driver");
        String url = "jdbc:mysql://localhost:3306/mydb";
        String sql = null;
        Connection connection = DriverManager.getConnection(url,"user","password");
        Statement statement = connection.createStatement();
        long begin = System.currentTimeMillis();
        for(int i = 0;i < 100000;i++){
            sql = "INSERT INTO customers VALUES(" + (i + 1)
                    + ", ' name_" + i + "', '2010-Ô1-13')";
            statement.addBatch(sql); // statement的批量处理
        }
        long end = System.currentTimeMillis();
        System.out.println("Time: " + (end - begin));
        statement.executeUpdate(sql);
        statement.close();
        connection.close();
    }

    // PreparedStatement()的executeUpdate分条处理
    public void testBatchWithPreparedStatement() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.jdbc.Driver");
        String url = "jdbc:mysql://localhost:3306/mydb";
        String sql = "INSERT INTO customers VALUES(?,?,?)";
        Connection connection = DriverManager.getConnection(url,"user","password");
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        Date date = new Date(new java.util.Date().getTime());

        long begin = System.currentTimeMillis();
        for(int i = 0;i < 100000;i++){
            preparedStatement.setInt(1,i+1);
            preparedStatement.setString(2,"name_" + i);
            preparedStatement.setDate(3,date);
            preparedStatement.executeUpdate();
        }
        long end = System.currentTimeMillis();
        System.out.println("Time: " + (end - begin));
        preparedStatement.close();
        connection.close();
    }
    

    // PreparedStatement()的executeBatch批量处理
    public void testBatch() throws ClassNotFoundException, SQLException {
        Class.forName("com.mysql.jdbc.Driver");
        String url = "jdbc:mysql://localhost:3306/mydb";
        String sql = "INSERT INTO customers VALUES(?,?,?)";
        Connection connection = DriverManager.getConnection(url,"user","password");
        PreparedStatement preparedStatement = connection.prepareStatement(sql);
        Date date = new Date(new java.util.Date().getTime());

        long begin = System.currentTimeMillis();
        for(int i = 0;i < 100000;i++){
            preparedStatement.setInt(1,i+1);
            preparedStatement.setString(2,"name_ " + i);
            preparedStatement.setDate(3,date);
            preparedStatement.addBatch();
            
            if((i + 1) % 300 == 0){
                preparedStatement.executeBatch();
                preparedStatement.clearBatch();
            }
        }
        
        if(100000 % 300 != 0){
            preparedStatement.executeBatch();
            preparedStatement.clearBatch();
        }

        long end = System.currentTimeMillis();
        System.out.println("Time: " + (end - begin));
        preparedStatement.close();
        connection.close();
    }
}
```

## 十四、数据库连接池：DBCP、C3P0

### 数据库连接池的必要性

1. 在使用开发基于数据库的wen程序时，传统的模式基本是按以下步骤：
1）在主程序(如servlet、beans)中建立数据库连接
2）进行sql操作
3）断开数据连接

2. 使用这种模式开发，存在的问题：
1）普通的JDBC数据库连接使用DriverManager来说去，每次向数据库建立连接的时候都要将Connection加载到内存中，再验证用户名和密码（需要花费0.05s-1s的时间）。需要数据库连接的时候，就向数据库要求一个，执行完后断开连接。这样的方式将会消耗大量的资源和时间。数据库的连接资源并没有得到很好的重复利用。若溶蚀有几百人甚至几千人在线，频繁的进行数据库连接操作将占用很多的系统资源，严重的甚至会造成服务器的崩溃。
2）对于每一次数据库连接，使用完后都得断开。否则，如果程序出现异常而未能关闭，将会导致数据库系统中的内存泄露，最终将导致重启数据库
3）这种开发不能控制被创建的连接对象数，系统资源会被毫无顾忌的分配出去，如连接过多，也可能导致内存泄漏，服务器崩溃

### 数据库连接池

1. 为解决传统开发中的数据库连接问题，可以采用数据库连接池技术

2. 数据库连接池的基本思想就是为数据库连接建立一个“缓冲池”。预先在缓冲池中放入一定数量的连接，当需要建立数据库连接时，只需从“缓冲池”中取出一个，使用完毕后再放回去

3. 数据库连接池负责分配、管理和释放数据库连接，它允许引用程序重复使用一个现有的数据连接，而不是重新建立一个

4. 数据库连接池在初始化时将创建一定数量的数据库连接放到连接池中，这些数据库连接的数量是由最小数据库连接数来设定的。无论这些数据库连接是否被使用，连接池都将一直保证至少拥有这么多的连接数量。连接池的最大数据库连接数量限定了这个连接池能占有的最大连接数，当应用程序向连接池请求的连接数超过最大连接数量时，这些请求将被加入到等待队列中

![](https://upload-images.jianshu.io/upload_images/2765653-66dbf1176dae86b9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 两种开源的数据库连接池

1）JDBC的数据库连接池使用javax.sql.DataSource来表示，DataSource只是一个接口，该接口通常由服务器提供实现，也有一些开源组织提供实现：DBCP数据库连接池、C3P0数据库连接池

2）DataSource通常被称为数据源，它包含连接池和连接池管理两个部分，习惯上也经常把DataSource称为连接池

### DBCP数据源

1）DBCP是Apache软件基金组织下的开源连接池实现，该连接池依赖该组织下的另一个开源系统，如需使用该连接池实现，应在系统增加两个jar包的依赖：commons-dpcp.jar(连接池的实现)、commons-pool.jar(连接池实现的依赖库)

2）Tomcat的连接池正是采用该连接池来实现的。该数据库连接池既可以与应用服务器整合使用，也可由应用程序独立使用

### DBCP数据源使用范例

1）数据源和数据连接不同，数据源无需创建多个，它是产生数据库连接的工厂，因此整个应用只需要一个数据源即可

2）当数据库访问结束后，程序还是像以前一样关闭数据库连接：conn.close()；但上面的代码并没有关闭数据库的物理连接，它仅仅把数据库连接释放，归还给了数据库连接池

```
// 使用DBCP数据库连接池
// 1. 加入jar包依赖
// 2. 创建数据库连接池
// 3. 为数据源实例指定必须的属性
// 4. 从数据源中获取数据库连接
public void testDBCP throws SQLException{
    BasicDataSource dataSource = null;
    // 1. 创建DBCP 数据源实例
    dataSource = new BasicDataSource();
    // 2. 为数据源实例指定必须的属性
    dataSource.setUsername("root");
    dataSource.setPassword("1230");
    dataSource.setUrl("");
    dataSource.setDriverClassName("");
    // 3. 指定数据源的一些可选的属性
    // 1）指定数据库连接池中初始化连接数的个数
    dataSource.setInitialSize(10);
    // 2）指定最大的连接数：同一时刻可以同时向数据库申请的连接数
    dataSource.setMaxActive(20);
    // 3）指定最小连接数：在数据库连接池中保存的最少的空闲连接的数量
    dataSource.setMinIdle(5);
    // 4）等待数据库连接池分配连接的最长时间。单位为毫秒。超出该时间将抛出异常
    dataSource.setMaxWaitMillis(1000*5);
    // 4. 从数据源中获取数据库连接
    Connection connection = dataSource.getConnection()

    BasicDataSource basicDataSource = (BasicDataSource) dataSource;
    basicDataSource.getMaxWaitMillis(); // 获取配置内容
}
```
使用配置文件

```
// dbcp.properties 创建配置文件
username=root
password=1230
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql:///atguigu

initialSize=10
maxActive=50
minIdle=5
maxWait=5000
```

```

public void testDBCPWithDataSourceFactory() throws Exception{		
    Properties properties = new Properties();
    InputStream inStream = JDBCTest.class.getClassLoader()
				.getResourceAsStream("dbcp.properties");
    properties.load(inStream);
		
    DataSource dataSource = BasicDataSourceFactory.createDataSource(properties);
    dataSource.getConnection(); // 获取连接 
		
    BasicDataSource basicDataSource = (BasicDataSource) dataSource; 
    basicDataSource.getMaxWait(); // 获取配置内容 
}
```

### C3P0
```
// 创建c3p0-config.xml 文件
<?xml version="1.0" encoding="UTF-8"?>
<c3p0-config>      
    <named-config name="helloc3p0">
        <!-- 指定连接数据源的基本属性-->  
        <!--user是数据库的用户，password是数据库的密码，driverClass是mysql的数据库驱动，jdbcUrl是连接数据库的url -->       
        <property name="user">root</property>
        <property name="password">123456</property>
        <property name="driverClass">com.mysql.jdbc.Driver</property>
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/java?useUnicode=true&amp;serverTimezone=UTC&amp;characterEncoding=UTF-8</property>

        <!--当连接池中的连接耗尽的时候c3p0一次同时获取的连接数 -->     
        <property name="acquireIncrement">5</property>
                
        <!--初始化时获取十个连接，取值应在minPoolSize与maxPoolSize之间 -->        
        <property name="initialPoolSize">10</property>
        
        <!--连接池中保留的最小连接数 -->        
        <property name="minPoolSize">10</property>
        
        <!--连接池中保留的最大连接数 -->        
        <property name="maxPoolSize">50</property>  
           
         <!--JDBC的标准参数，用以控制数据源内加载的PreparedStatements数量。但由于预缓存的statements属于单个connection而不是整个连接池。所以设置这个参数需要考虑到多方面的因素。如果maxStatements与maxStatementsPerConnection均为0，则缓存被关闭。Default: 0-->
        <property name="maxStatements">20</property>
        
        <!--maxStatementsPerConnection定义了连接池内单个连接所拥有的最大缓存statements数。Default: 0 -->
        <property name="maxStatementsPerConnection">5</property> 
    </named-config>
</c3p0-config>
```

```
// pom.xml 中增加c3p0的依赖
<dependency>
    <groupId>c3p0</groupId>
    <artifactId>c3p0</artifactId>
    <version>0.9.1.2</version>
</dependency>
```

```
public void testC3p0WithCongigFile() throws Exception{
    DataSource dataSource = new ComboPooledDataSource("helloc3p0");
    dataSource.getConnection(); // 在连接池获取连接
    ComboPooledDataSource comboPooledDataSource = (ComboPooledDataSource) dataSource; 
    comboPooledDataSource.getMaxStatements();// 获取配置文件中的getMaxStatements内容
}
```

不使用配置文件

```
// 直接使用c3p0，不使用c3p0-config.xml 文件
public void testC3p0() throws Exception{
    ComboPooledDataSource cpds = new ComboPooledDataSource();
    cpds.setDriverClass("com.mysql.jdbc.Driver");
    cpds.setJdbcUrl("jdbc:mysql:///test");
    cpds.setUser("root");
    cpds.setPassword("1230");
    cpbs.getConnection(); // 获取连接
}
```

## 十五、使用DBUtils 查询、更新

### DBUtils 基本介绍

commons-dbutils是Apache组织提供的一个开源JDBC工具类库，它是对JDBC的简单封装。简化了jdbc编码的工作量

### API介绍

org.apache.commons.dbutils.QueryRunner
org.apache.commons.dbutils.ResultSetHandler
工具类：org.apache.commons.dbutils.DbUtils


### 举例

update()方法可用于Insert、update、delete

```
public class JDBCTest06 {
    // 删除delete
    public JDBCTest06() throws SQLException {
        // 1. 创建QueryRunner 的实现类
        QueryRunner queryRunner = new QueryRunner();
        // 2. 使用其update 方法
        String sql = "DELETE FROM customers " + "WHERE id IN(?,>)";
        DataSource dataSource = new ComboPooledDataSource("helloc3p0");
        // 3. 在连接池获取连接
        Connection connection =  dataSource.getConnection();
        queryRunner.update(connection,sql,12,13); // update方法可用于删除、更新、添加
        connection.close();
    }
}
```
通过实现ResultSetHandler接口实现查询，创建ResultSetHandler接口的实现类，实现handle方法，queryRunner.query()的返回值取决于handle的返回值

```
public class DBUtilsTest {
    QueryRunner queryRunner = new QueryRunner();
    // 1. 创建 ResultSetHandler接口 的实现类，实现handle方法，queryRunner.query()的返回值取决于handle的返回值
    class MyResultSetHandler implements ResultSetHandler{
        @Override
        public Object handle(ResultSet rs) throws SQLException {
            List<Customer> customers = new ArrayList<>();
            
            while (rs.next()){
                Integer id = rs.getInt(1);
                String name = rs.getString(2);
                String email = rs.getString(3);
                Date birth = rs.getDate(4);
                Customer customer = new Customer(id,name,email,birth);
                customers.add(customer);
            }
            return customers;
        }
    }
    public void testQuery() throws SQLException {
        Connection connection = null;
        String sql = "select id,name,email,birth" + "from customers";
        Object object = queryRunner.query(connection, sql, new MyResultSetHandler());
        System.out.println(object);
        connection.close();
    }
}
```

queryRunner.query()源码分析

```
//1. QueryRunner 类的query()方法
public <T> T query(Connection conn, String sql, ResultSetHandler<T> rsh, Object... params) throws SQLException {
        return this.<T>query(conn, false, sql, rsh, params);// 返回值是调用当前的类query的重载方法
    }
// 2.当前的类query的重载方法
private <T> T query(Connection conn, boolean closeConn, String sql, ResultSetHandler<T> rsh, Object... params)
            throws SQLException {        
        PreparedStatement stmt = null;
        ResultSet rs = null;
        T result = null;

        try {
            stmt = this.prepareStatement(conn, sql);
            this.fillStatement(stmt, params);
            rs = this.wrap(stmt.executeQuery()); // wrap() 返回的是ResultSet
            result = rsh.handle(rs); //  handle()是ResultSetHandler接口定义的方法

        } catch (SQLException e) {
            this.rethrow(e, sql, params);

        } finally {
            try {
                close(rs);
            } finally {
                close(stmt);
                if (closeConn) {
                    close(conn);
                }
            }
        }
        return result;
    }
```

通过BeanHandler类实现查询，把结果集的第一条记录转为创建BeanHandler对象时传入的class参数对应的对象

```
    public void testBeanHandler() throws SQLException {
        QueryRunner queryRunner = new QueryRunner();
        Connection connection = null;
        String sql = "select id,name,email,birth" + "from customers where id >= ?";
        Object object = queryRunner.query(connection, sql, new BeanHandler(Customer.class),5);
        System.out.println(object);
        connection.close();
    }
```
通过BeanListHandler类实现查询，把结果集转为一个List，该List不为null，但可能为空集合（size()方法返回为0），若SQL语句有查询记录，List中存放创建BeanListHandler转入Class对象对应的对象

```
    public void testBeanListHandler() throws SQLException {
        QueryRunner queryRunner = new QueryRunner();
        Connection connection = null;
        String sql = "select id,name,email,birth" + "from customers";
        List<Customer> customers = queryRunner.query(connection,sql,new BeanListHandler<Customer>(Customer.class));
        Object object = queryRunner.query(connection, sql, new BeanHandler(Customer.class),5);
        System.out.println(object);
        connection.close();
    }
```

通过MapHandler类实现查询，返回SQL对应的第一条记录对应的Map对象，键值对：键SQL查询的列名(不是别名)，列的值

```
public void testMapHandler() throws SQLException {
        QueryRunner queryRunner = new QueryRunner();
        Connection connection = null;
        String sql = "select id,name,email,birth" + "from customers";
        Map<String,Object> customers = queryRunner.query(connection,sql,new MapHandler());
        Object object = queryRunner.query(connection, sql, new BeanHandler(Customer.class),5);
        System.out.println(object);
        connection.close();
    }
```

通过MapListHandler类实现查询，将结果集转为一个Map的List，Map对应查询的一条记录：键值堆：键SQL查询的列名（不是列的别名），值：列的值，而MapListHandler：返回的多条记录对应的Map的集合

```
    public void testMapListHandler() throws SQLException {
        QueryRunner queryRunner = new QueryRunner();
        Connection connection = null;
        String sql = "select id,name,email,birth" + "from customers";
        List<Map<String,Object>> result = queryRunner.query(connection,sql,new MapListHandler());
        Object object = queryRunner.query(connection, sql, new BeanHandler(Customer.class),5);
        System.out.println(object);
        connection.close();
    }
```
ScalarHandler：把结果集转为一个数值（可以是任意基本数据类型和字符串，Date等）返回

```
public void ScalarHandler() throws SQLException {
        QueryRunner queryRunner = new QueryRunner();
        Connection connection = null;
        String sql = "select name" + "from customers"; // 如果是两列的情况返回一列
        List<Map<String,Object>> result = queryRunner.query(connection,sql,new MapListHandler());
        Object object = queryRunner.query(connection, sql, new ScalarHandler<>(),5);
        System.out.println(object);
        connection.close();
    }
```

