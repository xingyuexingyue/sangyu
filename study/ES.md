ElasticSearch是目前全文搜索引擎的首选，可以快速的存储、搜索和分析数据，并且ES是一个分布式搜索服务，提供Restful API，底层基于Lucene，采用多shard（分片）的方式保证数据安全，并且提供自动resharding的功能，github等大型的站点也是采用了ES作为其搜索服务

#### docker安装ES

```
$ docker pull elasticsearch // 拉取镜像
Using default tag: latest
latest: Pulling from library/elasticsearch
[DEPRECATION NOTICE] registry v2 schema1 support will be removed in an upcoming release. Please contact admins of the docker.io registry NOW to avoid future disruption.
05d1a5232b46: Pull complete 
5cee356eda6b: Pull complete 
89d3385f0fd3: Pull complete 
65dd87f6620b: Pull complete 
78a183a01190: Pull complete 
1a4499c85f97: Pull complete 
2c9d39b4bfc1: Pull complete 
1b1cec2222c9: Pull complete 
59ff4ce9df68: Pull complete 
1976bc3ee432: Pull complete 
5af49e8af381: Pull complete 
42c8b75ff7af: Pull complete 
7e6902915254: Pull complete 
99853874fa54: Pull complete 
596fbad6fcff: Pull complete 
Digest: sha256:6133081706cedbb5f486a510482c285d8cd54820411bd916d965c7a9b1969d24
Status: Downloaded newer image for elasticsearch:latest
docker.io/library/elasticsearch:latest
```
```
$ docker images // 安装的镜像
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
elasticsearch       latest              5acf0e8da90b        17 months ago       486MB
```
```
$ docker run -e ES_JAVA_OPTS="-Xms256m -Xmx256m" -d -p 9200:9200 -p 9300:9300 --name ES01 5acf0e8da90b // 初始化容器
8ed13535108a1bd611f0ce53aea3548494d9956f777c526ea10aaf95ec404683
```

```
$ docker ps  // 正常运行的容器
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                                                                                                      NAMES
8ed13535108a        5acf0e8da90b          "/docker-entrypoint.…"   33 seconds ago      Up 29 seconds       0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp                                                                             ES01
```

验证ES安装成功，[访问此url](http://localhost:9200/)

![](https://upload-images.jianshu.io/upload_images/2765653-7479295546e9d570.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

#### ES基础入门

ES使用JavaScript Object Notation 或者JSON作为文档的序列化格式。JSON序列化被大多数变成语言所支持，并且已经成为NoSQL领域的标准格式。

以下使用JSON文档来表示一个用户对象：

```
{
    "email": "john@smith.com",
    "first_name": "John",
    "last_name": "Smith",
    "info": {
        "bio": "Eco-warrior and defender of the weak",
        "age": 25,
        "interests": [ "dolphins", "whales" ]
    },
    "join_date": "2014/05/01"
}
```

ES集群可以包含多个索引(indices)（数据库），每一个索引可以包含多个类型(types)（表），每一个类型包含多个文档(documents)（行），然后每个文档包含多个字段(Fields)（列）

通过对比图来类比传统关系型数据库：

```
Relational DB -> Databases -> Tables -> Rows -> Columns
Elasticsearch -> Indices   -> Types  -> Documents -> Fields
```

假使现在Animal公司，需要创建一个员工目录，为此我们将进行如下操作

1. 为每个员工的文档(document)建立索引，每个文档包含了相应员工的所有信息。
2. 每个文档的类型为employee。
3. employee类型归属于索引megacorp。
4. megacorp索引存储在Elasticsearch集群中。

而上述这些步骤，通过一条命令就能完成所有这些动作：

```
PUT /animal/employee/1
{
    "first_name" : "John",
    "last_name" : "Smith",
    "age" : 25,
    "about" : "I love to go rock climbing",
    "interests" : ["sports","music"]
}
```

实际操作，借助Postman

![添加员工1](https://upload-images.jianshu.io/upload_images/2765653-a531722138c244ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![返回结果](https://upload-images.jianshu.io/upload_images/2765653-a19858e5b0389d49.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![继续按照相同的步骤添加员工2](https://upload-images.jianshu.io/upload_images/2765653-576f171788cdeb4d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![继续按照相同的步骤添加员工3](https://upload-images.jianshu.io/upload_images/2765653-a9c2a2d0cf7bfa00.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

检索文档，通过执行一个HTTP GET请求并指定文档的地址--索引库、类型和ID。使用这三个信息可以返回原始的JSON文档

``` 
GET /animal/employee/1
```

![GET](https://upload-images.jianshu.io/upload_images/2765653-cb80d3541782add2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![HEAD](https://upload-images.jianshu.io/upload_images/2765653-8340ded58a01fe50.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![DELETE](https://upload-images.jianshu.io/upload_images/2765653-af71717ef1298b56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



我们尝试一个最简单的搜索全部员工的请求：

```
GET /megacorp/employee/_search
```

![展示了刚刚添加的3个员工，默认情况下搜索会返回前10个结果](https://upload-images.jianshu.io/upload_images/2765653-a3e1bac68cc35da6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

搜索姓氏中包含“Smith”的员工，使用轻量级的搜索方法。这种方法常被称作查询字符串(query string)搜索

```
GET /megacorp/employee/_search?q=last_name:Smith
```

![查询结果](https://upload-images.jianshu.io/upload_images/2765653-6049f9ac5bc0566b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

使用DSL语句查询，DSL(Domain Specific Language特定领域语言)以JSON请求体的形式出现。我们可以这样表示之前关于“Smith”的查询:

```
GET /megacorp/employee/_search
{
    "query" : {
        "match" : {
            "last_name" : "Smith"
        }
    }
}
```
比刚才更复杂的搜索，要查找姓氏为“Smith”的员工并且年龄大于30岁的员工。此时需要使用过滤器(filter)

```
GET /megacorp/employee/_search
{
    "query" : {
        "filtered" : {
            "filter" : {
                "range" : {
                    "age" : { "gt" : 30 } <1> // <1> 这部分查询属于区间过滤器(range filter),它用于查找所有年龄大于30岁的数据
                }
            },
            "query" : {
                "match" : {
                    "last_name" : "smith" <2> // <2> 这部分查询与之前的match语句(query)一致
                }
            }
        }
    }
}
```

全文搜索

```
// 所有喜欢“rock climbing”的员工
GET /megacorp/employee/_search
{
    "query" : {
        "match" : {
            "about" : "rock climbing"
        }
    }
}
// <1><2> 结果相关性评分。
默认情况下，ES根据结果相关性评分来对结果集进行排序，所谓的「结果相关性评分」就是文档与查询条件的匹配程度。很显然，排名第一的John Smith的about字段明确的写到“rock climbing”。
但是为什么Jane Smith也会出现在结果里呢？原因是“rock”在她的abuot字段中被提及了。因为只有“rock”被提及而“climbing”没有，所以她的_score要低于John。
这个例子很好的解释了Elasticsearch如何在各种文本字段中进行全文搜索，并且返回相关性最大的结果集。相关性(relevance)的概念在Elasticsearch中非常重要，而这个概念在传统关系型数据库中是不可想象的，因为传统数据库对记录的查询只有匹配或者不匹配。
```

短语搜索

目前我们可以在字段中搜索单独的一个词，这挺好的，但是有时候你想要确切的匹配若干个单词或者短语(phrases)。例如我们想要查询同时包含"rock"和"climbing"（并且是相邻的）的员工记录。

```
GET /megacorp/employee/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "rock climbing"
        }
    }
}
```

高亮我们的搜索

很多应用喜欢从每个搜索结果中高亮(highlight)匹配到的关键字，这样用户可以知道为什么这些文档和查询相匹配。在Elasticsearch中高亮片段是非常容易的。

```
GET /megacorp/employee/_search
{
    "query" : {
        "match_phrase" : {
            "about" : "rock climbing"
        }
    },
    "highlight": {
        "fields" : {
            "about" : {}
        }
    }
}
```

#### SpringBoot 整合ES

通过向导快速创建SpringBoot，其他步骤可参考之前的文章
![](https://upload-images.jianshu.io/upload_images/2765653-d30b076ae636ef57.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

springboot默认支持两种技术来和ES交互

1. JEST（默认不生效）

```
// pom.xml注入依赖
<dependency>
    <groupId>io.searchbox</groupId>
    <artifactId>jest</artifactId>
    <version>5.3.3</version>
</dependency>
```

```
//application.properties
spring.elasticsearch.rest.uris=http://127.0.0.1:9200
```
```
public class Article {
    @JestId
    private Integer id;
    private String author;
    private String title;
    private String content;
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getAuthor() {
        return author;
    }
    public void setAuthor(String author) {
        this.author = author;
    }
    public String getContent() {
        return content;
    }
    public void setContent(String content) {
        this.content = content;
    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
    @Override
    public String toString() {
        return "Article{" +
                "id=" + id +
                ", author='" + author + '\'' +
                ", title='" + title + '\'' +
                ", content='" + content + '\'' +
                '}';
    }
}
```

```
@SpringBootTest
class MySpringBootEsApplicationTests {

    @Autowired
    JestClient jestClient;

    @Test
    void contextLoads() {
        // 给ES中索引保存一个文档
        Article article = new Article();
        article.setId(1);
        article.setTitle("AA");
        article.setTitle("11");
        article.setContent("good");

        // 构建一个所以对象
        Index index = new Index.Builder(article).index("sangyu").type("news").build();

        try{
            // 执行
            jestClient.execute(index);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // 测试搜索
    @Test
    public void search(){
        // 查询搜索
        String json = "{\n" +
                "    \"query\" : {\n" +
                "        \"match\" : {\n" +
                "            \"content\" : \"good\"\n" +
                "        }\n" +
                "    }\n" +
                "}";

        // 构建搜索功能
        Search search = new Search.Builder(json).addIndex("sangyu").addType("news").build();

        // 执行
        try{
            SearchResult result = jestClient.execute(search);
            System.out.println(result.getJsonString());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

2. 使用springboot 整合elasticsearch

环境

SpringBoot: 2.2.4.RELEASE
Elasticsearch: 6.7.2
JDK: 1.8

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:6.7.2
```

```
$ docker run -e ES_JAVA_OPTS="-Xms256m -Xmx256m" -d -p 9202:9200 -p 9302:9300 -e "discovery.type=single-node" --name ES03 2982ba071059 
9a0f07c705abf00f7faaefbbd4478aeb8fc49f0c40346ca8e2f028ca39d82a34
```

```
// 为了版本统一，修改pom.xml一览
<dependencies>
        <dependency>
            <groupId>org.elasticsearch</groupId>
            <artifactId>elasticsearch</artifactId>
            <version>6.7.2</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-elasticsearch</artifactId>
            <version>3.2.0.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.elasticsearch.client</groupId>
            <artifactId>elasticsearch-rest-high-level-client</artifactId>
            <version>6.7.2</version>
        </dependency>
        <dependency>
            <groupId>io.searchbox</groupId>
            <artifactId>jest</artifactId>
            <version>5.3.3</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.elasticsearch.client</groupId>
            <artifactId>x-pack-transport</artifactId>
            <version>6.7.2</version>
        </dependency>
    </dependencies>
```

```
// application.properties
elastic.host=127.0.0.1
elastic.port=9202
```

```
public class Article {
    @JestId
    private Integer id;
    private String author;
    private String title;
    private String content;
    public Integer getId() {
        return id;
    }
    public void setId(Integer id) {
        this.id = id;
    }
    public String getAuthor() {
        return author;
    }
    public void setAuthor(String author) {
        this.author = author;
    }
    public String getContent() {
        return content;
    }
    public void setContent(String content) {
        this.content = content;
    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }
    @Override
    public String toString() {
        return "Article{" +
                "id=" + id +
                ", author='" + author + '\'' +
                ", title='" + title + '\'' +
                ", content='" + content + '\'' +
                '}';
    }
}
```

```
@Configuration
public class EsConf {

    @Value("${elastic.host}")
    private String host;

    @Value("${elastic.port}")
    private int port;


    @Bean
    public RestHighLevelClient elasticsearchClient() {
        RestClientBuilder builder = RestClient.builder(new HttpHost(host, port));
        return new RestHighLevelClient(builder);
    }

    @Bean
    public ElasticsearchRestTemplate elasticsearchTemplate() {
        return new ElasticsearchRestTemplate(elasticsearchClient());
    }
```

```
public interface StudentRepository extends ElasticsearchRepository<Student, Long> {
    List<Student> findByName(String name);
}
```
```
@SpringBootTest
class MySpringBootEsApplicationTests {
    @Autowired
    private StudentRepository studentRepository;
    Student stu = new Student();
    @Test
    public void save() {
        stu.setId(4L);
        stu.setName("Bob");
        stu.setHobby("biu biu biu~~");
        stu.setBirthday(new Date());
        studentRepository.save(stu);
    }

    @Test
    public void findById() {
        Student stu = studentRepository.findById(3L).orElse(null);
        System.out.println(stu);
    }

    @Test
    public void findByName() {
        List<Student> bob = studentRepository.findByName("Bob");
        bob.forEach(System.out::println);
    }

    @Test
    public void delete() {
        studentRepository.deleteById(3L);
    }
}
```