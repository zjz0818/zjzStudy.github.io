## c
- 原因，更换版本后出现的
- 需要设置MySQL的配置文件
- 进入管理员cmd
 ```
  进入mysql
  PS C:\Windows\system32> mysql -u root -p
   Enter password: ******
  mysql> show variables like '%time_zone%';
  +------------------+--------+
  | Variable_name    | Value  |
  +------------------+--------+
  | system_time_zone |        |
  | time_zone        | SYSTEM |
  +------------------+--------+
  mysql> set global time_zone='+8:00';
  Query OK, 0 rows affected (0.00 sec)

 
 ```


- 高版本数据库解决方式

```
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/mybatis?useUnicode=true&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC
username=root
password=123456




```

