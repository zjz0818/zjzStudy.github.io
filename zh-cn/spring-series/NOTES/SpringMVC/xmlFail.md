# 。xml加载失败
- 1.先正常操作
- 2.试一下  --- 每次试的时候，删除target和对应的out clean mav compiler mvn
- pom加
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


- 3.试一下 --- 每次试的时候，删除target和对应的out clean mav compiler mvn

- pom 加
```
    <!--在build中配置resources，来防止我们资源导致失败问题-->
    <build>
        <resources>
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