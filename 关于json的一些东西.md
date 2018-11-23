##json的序列化和反序列化

#### 问题描述：

这边一个接口是读取文件中的内容，通过json格式读取，然后增加一些数据，以json格式存储到文件中

#### 问题解决：

1.采用jackson方式来实现字符串的序列化和反序列化

* 需要的环境
* 组件：com.fasterxml.jackson
* pom文件：

</html>

	<logback.version>1.0.13</logback.version>
	<jackson.version>2.3.1</jackson.version>  
	<dependency>  
    	<groupId>ch.qos.logback</groupId>  
    	<artifactId>logback-classic</artifactId>  <version>${logback.version}</version>  
	</dependency>  
  
	<dependency>  
    	<groupId>com.fasterxml.jackson.core</groupId>  
    	<artifactId>jackson-databind</artifactId>  
    	<version>${jackson.version}</version>  
	</dependency>  

* 具体的文件代码

</html>

	import java.io.IOException;  
	import java.io.StringWriter;  
	import java.io.Writer;  
	import java.util.Map;  
  
	import org.slf4j.LoggerFactory;  
  
	import ch.qos.logback.classic.Logger;  
  
	import com.fasterxml.jackson.core.JsonGenerationException;  
	import com.fasterxml.jackson.core.JsonParseException;  
	import com.fasterxml.jackson.core.type.TypeReference;  
	import com.fasterxml.jackson.databind.JsonMappingException;  
	import com.fasterxml.jackson.databind.ObjectMapper;  
	import com.fasterxml.jackson.databind.type.TypeFactory;  
  
	/** 
	Json序列化工具 
	@author http://blog.csdn.net/xxd851116 
	@date 2014年3月26日 下午1:21:59 
	/  
	public class JsonUtils {  
    private static final Logger logger = (Logger) LoggerFactory.getLogger(JsonUtils.class);  
  
    private static ObjectMapper objectMapper = new ObjectMapper();  
  
    /** 
      将对象序列化为JSON字符串   
     @param object 
     @return JSON字符串 
     */  
    public static String serialize(Object object) {  
        Writer write = new StringWriter();  
        try {  
            objectMapper.writeValue(write, object);  
        } catch (JsonGenerationException e) {  
            logger.error("JsonGenerationException when serialize object to json", e);  
        } catch (JsonMappingException e) {  
            logger.error("JsonMappingException when serialize object to json", e);  
        } catch (IOException e) {  
            logger.error("IOException when serialize object to json", e);  
        }  
        return write.toString();  
    }  
  
    /** 
     将JSON字符串反序列化为对象   
      @param object 
      @return JSON字符串 
     */  
    public static <T> T deserialize(String json, Class<T> clazz) {  
        Object object = null;  
        try {  
            object = objectMapper.readValue(json, TypeFactory.rawClass(clazz));  
        } catch (JsonParseException e) {  
            logger.error("JsonParseException when serialize object to json", e);  
        } catch (JsonMappingException e) {  
            logger.error("JsonMappingException when serialize object to json", e);  
        } catch (IOException e) {  
            logger.error("IOException when serialize object to json", e);  
        }  
        return (T) object;  
    }  
  
    /** 
     将JSON字符串反序列化为对象   
     @param object 
      @return JSON字符串 
     */  
    public static <T> T deserialize(String json, TypeReference<T> typeRef) {  
        try {  
            return (T) objectMapper.readValue(json, typeRef);  
        } catch (JsonParseException e) {  
            logger.error("JsonParseException when deserialize json", e);  
        } catch (JsonMappingException e) {  
            logger.error("JsonMappingException when deserialize json", e);  
        } catch (IOException e) {  
            logger.error("IOException when deserialize json", e);  
        }  
        return null;  
    }  
	}  

2.采用Gson方式

* 基本方法toJson()，以及fromJson()
* 创建方式一：直接new Gson对象。

<html/>

	// 使用new方法
	Gson gson = new Gson();

	// toJson 将bean对象转换为json字符串
	String jsonStr = gson.toJson(user, User.class);

	// fromJson 将json字符串转为bean对象
	Student user= gson.fromJson(jsonStr, User.class);

	// **序列化List**
	String jsonStr2 = gson.toJson(list);

	// **反序列化成List时需要使用到TypeToken getType()**
	List<User> retList = gson.fromJson(jsonStr2,new TypeToken<List<User>>(){}.getType());

* 创建方式二：使用GsonBuilder
* 使用GsonBuilder使用new Gson()，此时会创建一个带有默认配置选项的Gson实例，如果不想使用默认配置，那么就可以使用GsonBuilder。

<html/>

	//serializeNulls()是GsonBuilder提供的一种配置，当字段值为空或null时，依然对该字段进行转换
	Gson gson = new GsonBuilder().serializeNulls().create(); 

* 使用GsonBuilder创建Gson实例的步骤：首先创建GsonBuilder,然后调用GsonBuilder提供的各种配置方法进行配置，最后调用GsonBuilder的create方法，将基于当前的配置创建一个Gson实例。
* GsonBuilder的一些配置 	

<html/>

	Gson gson = new GsonBuilder()
         .excludeFieldsWithoutExposeAnnotation() //不对没有用@Expose注解的属性进行操作
         .enableComplexMapKeySerialization() //当Map的key为复杂对象时,需要开启该方法
         .serializeNulls() //当字段值为空或null时，依然对该字段进行转换
         .setDateFormat("yyyy-MM-dd HH:mm:ss:SSS") //时间转化为特定格式
         .setPrettyPrinting() //对结果进行格式化，增加换行
         .disableHtmlEscaping() //防止特殊字符出现乱码
         .registerTypeAdapter(User.class,new UserAdapter()) //为某特定对象设置固定的序列或反序列方式，自定义Adapter需实现JsonSerializer或者JsonDeserializer接口
         .create();

* 例如：Gosn对复杂Map的处理时需要用到其中的enableComplexMapKeySerialization() 配置：

<html/>

	Gson gson = new GsonBuilder().enableComplexMapKeySerialization().create(); //开启复杂处理Map方法
	Map<List<User>, String> map = new HashMap<List<User>, String>();
	// TODO 向map中添加数据
	String jsonStr = gson.toJson(map);  //toJson
	Map<List<User>, String> resultMap = gson.fromJson(jsonStr,new TypeToken<Map<List<User>, String>>() {}.getType()); //fromJson

* 注意：如果Map的key为String，则可以不使用GsonBuilder的enableComplexMapKeySerialization()方法，或者直接new Gson();

3.Gson的注解
* @Expose注解

<html/>

	public class User {
	@Expose
	private String firstName;

	@Expose(serialize = false)
	private String lastName;

	@Expose(deserialize = false)
	private String emailAddress;

	private String password;
	}

* @Expose中serialize和deserialize属性是可选的，默认两个都为true。如果serialize为true，调用toJson时会序列化该属性，
如果deserialize为true，调用fromJson生成Java对象时不会进行反序列化。
* 注意：如果采用new Gson()方式创建Gson，@Expose没有任何效果。需要使用 gsonBuilder.excludeFieldsWithoutExposeAnnotation()方法。
 
* @SerializedName注解:能指定该字段在序列化成json时的名称

<html/>

	@SerializedName("w")
	private int width;