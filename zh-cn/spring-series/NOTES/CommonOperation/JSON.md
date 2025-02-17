# json
> jackson，fastjson
> 

## 前后端分离：
- JSON(JavaScript Object Notation, JS 对象标记) 是一种轻量级的数据交换格式，目前使用特别广泛。
   - 采用完全独立于编程语言的文本格式来存储和表示数据。
   - 简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。
   - 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。
    

- 在 JavaScript 语言中，一切都是对象。因此，任何JavaScript 支持的类型都可以通过 JSON 来表示，
  例如字符串、数字、对象、数组等。看看他的要求和语法格式：
  - 对象表示为键值对，数据由逗号分隔
  - 花括号保存对象
  - 方括号保存数组


- JSON 键值对是用来保存 JavaScript 对象的一种方式，和 JavaScript 对象的写法也大同小异，
  - 键/值对组合中的键名写在前面并用双引号 "" 包裹，使用冒号 : 分隔，然后紧接着值：
  - {"name": "zjz"} {"age": "22"} {"sex": "男"}  
    
- 很多人搞不清楚 JSON 和 JavaScript 对象的关系，甚至连谁是谁都不清楚。其实，可以这么理解：
  JSON 是 JavaScript 对象的**字符串表示法**，它使用文本表示一个 JS 对象的信息，
  **本质是一个字符串**。
  
- var obj = {a: 'Hello', b: 'World'}; //这是一个对象，注意键名也是可以使用引号包裹的
- var json = '{"a": "Hello", "b": "World"}'; //这是一个 JSON 字符串，本质是一个 字符串


- JSON 和 JavaScript 对象互转
    - 1.要实现从JSON字符串转换为JavaScript 对象，使用 JSON.parse() 方法：
      - var obj = JSON.parse('{"a": "Hello", "b": "World"}'); //结果是 {a: 'Hello', b: 'World'}
    - 2.要实现从JavaScript 对象转换为JSON字符串，使用 JSON.stringify() 方法
      - var json = JSON.stringify({a: 'Hello', b: 'World'}); //结果是 '{"a": "Hello", "b": "World"}'
    


## 两种方式，jackson，fastjson

- java中对象转换为json
- 1.导包
  
  ```
  
          <!-- https://mvnrepository.com/artifact/com.fasterxml.jackson.core/jackson-databind -->
          <dependency>
              <groupId>com.fasterxml.jackson.core</groupId>
              <artifactId>jackson-databind</artifactId>
              <version>2.12.3</version>
          </dependency>
  
      
  
  ```
- 2.java中
  - 关键是：ObjectMapper mapper = new ObjectMapper();  mapper.writeValueAsString(user); 转换为字符串
    ```
          @Controller
          public class UserController {
              @RequestMapping("/j1")
              @ResponseBody  // 只要加了ResponseBody 就不会走视图解析器，会直接返回一个字符串
              public String json1() throws JsonProcessingException {
          
                  User user = new User("zjz", 3, "nan");
          
                  ObjectMapper mapper = new ObjectMapper();
          
                  String s = mapper.writeValueAsString(user);
                  return s;
              }
          }
    
    ```



- 3.解决乱码，似乎SpringMVC已经解决了？
  
  ```
      <mvc:annotation-driven>
          <mvc:message-converters register-defaults="true">
              <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                  <constructor-arg value="UTF-8"/>
              </bean>
              <bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageCon verter">
                  <property name="objectMapper">
                      <bean class="org.springframework.http.converter.json.Jackson2ObjectMapperFactoryBe an">
                          <property name="failOnEmptyBeans" value="false"/>
                      </bean>
                  </property>
              </bean>
          </mvc:message-converters>
      </mvc:annotation-driven>
  
  ```




- fastJson
  - fastjson.jar是阿里开发的一款专门用于Java开发的包，可以方便的实现json对象与JavaBean对象的转
    换，实现JavaBean对象与json字符串的转换，实现json对象与json字符串的转换。实现json的转换方法
    很多，最后的实现结果都是一样的。
    
    ```
    
        <dependency> 
            <groupId>com.alibaba</groupId> 
            <artifactId>fastjson</artifactId> 
            <version>1.2.60</version> 
        </dependency>
    
    ```
    



