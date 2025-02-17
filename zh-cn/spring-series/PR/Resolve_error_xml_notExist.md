
# maven
> 明明文件存在， 却找不到文件
> 
> 原因：Maven的约定大于配置
> 
> 他可能就没配置

### Error building SqlSession.
### The error may exist in com/zjz/dao/UserMapper.xml


- 解决，pom中导一些东西（注意要知道在哪个pom下导）

```
      <!--在build中配置resources，来防止我们资源导致失败问题-->
        <build>
            <resources>
                <resource>
                    <directory>src/main/resource</directory>
                    <includes>
                        <include>**/*.properties</include>
                        <include>**/*.xml</include>
                    </includes>
                    <filtering>false</filtering>
                </resource>
                <resource>
                    <directory>src/main/java</directory>
                    <includes>
                        <include>**/*.properties</include>
                        <include>**/*.xml</include>
                    </includes>
                    <filtering>false</filtering>
                </resource>
            </resources>
        </build>
```


## com.sun.org.apache.xerces.internal.impl.io.MalformedByteSequenceException: 1 字节的 UTF-8 序列的字节 1 无效。
- 解决方法，将xml中的UTF-8 改为UTF8


## Invalid bound statement (not found): com.zjz.dao.UserMapper.getUserList
- select id="getUserList"   ---- id和Mapper的方法一致
