Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件

1、使用docker安装redis

```
docker pull redis // 拉取镜像

docker ps // 列出所有的容器

docker run -d -p 6379:6379 --name myredis redis:latest // 使用docker镜像redis:latest以后台模式启动一个容器,并将容器命名为myredis，容器的 6379 端口映射到主机的 6379 端口

docker rmi <Image-Id> // 使用rmi 删除容器时提示错误
Error response from daemon: conflict: unable to delete <Image-ID> (must be forced) - image is being used by stopped container xxxxxxxxxxx
// 可强制删除
docker rmi -f <image_id>  
```
2、pom.xml 注入redis依赖

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

3、测试Redis

```
@RunWith(SpringRunner.class)
@SpringBootTest
public class MySpringBootRedisApplicationTests {
    @Autowired
    EmployeeMapper employeeMapper;

    @Autowired
    StringRedisTemplate stringRedisTemplate;  //操作k-v都是字符串的

    @Autowired
    RedisTemplate redisTemplate;  //k-v都是对象的

    /**
     * Redis常见的五大数据类型
     *  String（字符串）、List（列表）、Set（集合）、Hash（散列）、ZSet（有序集合）
     *  stringRedisTemplate.opsForValue()[String（字符串）]
     *  stringRedisTemplate.opsForList()[List（列表）]
     *  stringRedisTemplate.opsForSet()[Set（集合）]
     *  stringRedisTemplate.opsForHash()[Hash（散列）]
     *  stringRedisTemplate.opsForZSet()[ZSet（有序集合）]
     */
    @Test
    public void test01(){
        //给redis中保存数据
        //stringRedisTemplate.opsForValue().append("msg","hello");
		String msg = stringRedisTemplate.opsForValue().get("msg"); // 保存字符串
		System.out.println(msg);

		stringRedisTemplate.opsForList().leftPush("mylist","1"); // 保存列表
		stringRedisTemplate.opsForList().leftPush("mylist","2");
    }
   //测试保存对象
    @Test
    public void test02(){
        Employee empById = employeeMapper.getEmpById(1);
        //如果保存对象，默认使用jdk序列化机制，序列化后的数据保存到redis中
        redisTemplate.opsForValue().set("emp-01",empById); // Employee bean实现Serializable
    }
}
```

4、RedisConfig

```
@Configuration
public class MyRedisConfig {
    // 改变默认的序列化规则
    @Bean
    public RedisTemplate<Object, Employee> empRedisTemplate(
            RedisConnectionFactory redisConnectionFactory)
            throws UnknownHostException {
        RedisTemplate<Object, Employee> template = new RedisTemplate<Object, Employee>();
        template.setConnectionFactory(redisConnectionFactory);
        Jackson2JsonRedisSerializer<Employee> ser = new Jackson2JsonRedisSerializer<Employee>(Employee.class); // Jackson2JsonRedisSerializer redis的序列化器
        template.setDefaultSerializer(ser); // 切换到redis序列化器
        return template;
    }
}
```

测试
```
@RunWith(SpringRunner.class)
@SpringBootTest
public class MySpringBootRedisApplicationTests {
    @Autowired
    EmployeeMapper employeeMapper;

    @Autowired
    RedisTemplate<Object, Employee> empRedisTemplate;

   //测试保存对象
    @Test
    public void test02(){
        Employee empById = employeeMapper.getEmpById(1);
        //1、将数据以json的方式保存
        //(1)自己将对象转为json
        //(2)redisTemplate默认的序列化规则；可以转为json
        empRedisTemplate.opsForValue().set("emp-01",empById);
    }
}
```

5、CacheManager

```
@Configuration
public class MyRedisConfig {
    @Bean
    public CacheManager cacheManager(RedisConnectionFactory factory) {
        //初始化一个RedisCacheWriter
        RedisCacheWriter redisCacheWriter = RedisCacheWriter.nonLockingRedisCacheWriter(factory);
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);

        //重写objectMapper
        MyObjectMapper objectMapper = new MyObjectMapper();
        objectMapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);

        //设置序列化器
        RedisSerializationContext.SerializationPair<Object> pair = RedisSerializationContext.SerializationPair.fromSerializer(jackson2JsonRedisSerializer);
        RedisCacheConfiguration defaultCacheConfig = RedisCacheConfiguration.defaultCacheConfig().serializeValuesWith(pair);
        return new RedisCacheManager(redisCacheWriter, defaultCacheConfig);
    }

    public class MyObjectMapper extends ObjectMapper {
        private static final long serialVersionUID = 1L;

        public MyObjectMapper() {
            super();
            // 去掉各种@JsonSerialize注解的解析
            this.configure(MapperFeature.USE_ANNOTATIONS, false);
            // 只针对非空的值进行序列化
            this.setSerializationInclusion(JsonInclude.Include.NON_NULL);
            // 对于找不到匹配属性的时候忽略报错
            this.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false);
            // 不包含任何属性的bean也不报错
            this.configure(SerializationFeature.FAIL_ON_EMPTY_BEANS, false);
        }
    }
}

```

```
public class Department  {
	
	private Integer id;
	private String departmentName;
	
	public Department() {
		super();
		// TODO Auto-generated constructor stub
	}
	public Department(Integer id, String departmentName) {
		super();
		this.id = id;
		this.departmentName = departmentName;
	}
	public Integer getId() {
		return id;
	}
	public void setId(Integer id) {
		this.id = id;
	}
	public String getDepartmentName() {
		return departmentName;
	}
	public void setDepartmentName(String departmentName) {
		this.departmentName = departmentName;
	}
	@Override
	public String toString() {
		return "Department [id=" + id + ", departmentName=" + departmentName + "]";
	}
}
```

```
@Mapper
public interface DepartmentMapper {
    @Select("SELECT * FROM department WHERE id = #{id}")
    Department getDeptById(Integer id);
}
```

```
@RestController
public class DeptController {

    @Autowired
    DeptService deptService;

    @GetMapping("/dept/{id}")
    public Department getDept(@PathVariable("id") Integer id){
        return deptService.getDeptById(id);
    }
}
```

```
// 缓存：缓存中存在从缓存返回，缓存中没有查DB返回并更新缓存
// 使用缓存，方式一，使用注解
@Service
public class DeptService {
    @Autowired
    DepartmentMapper departmentMapper;
    // 使用缓存管理器得到缓存，进行api调用
    @Cacheable(cacheNames = {"dept"},key = "#id")
    public Department getDeptById(Integer id) {
        Department department = departmentMapper.getDeptById(id);
        return department;
    }
}

// 使用缓存，方式二，编码
@Service
public class DeptService {
    @Autowired
    DepartmentMapper departmentMapper;
    @Autowired
    CacheManager cacheManager;
    public Department getDeptById(Integer id) {
        //获取某个缓存
        Cache dept = cacheManager.getCache("dept");
        if (dept != null) {
            Department department1 = dept.get(id, Department.class);
            if (department1 != null) {
                return department1;
            }
        }
        Department department = departmentMapper.getDeptById(id);
        dept.put(id, department);
        return department;
    }
}
```