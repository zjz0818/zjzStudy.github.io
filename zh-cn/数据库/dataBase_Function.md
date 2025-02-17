# 数据库的函数

## SQL
- DATABASE 自动生成本数据库名,使用数据库里的函数DATABASE()--直接写在values中...
    - 用于微服务,因为要找到对应的库---微服务--一个服务对应一个数据库,同一个信息可能存在不同的数据库
    
- ABS(N) 绝对值
- RAND() 0-1之间的随机数
- CEILING(N) 向上取整
- FLOOR(N) 向下取整
- SIGN(N)  判断一个数的符号,负数-1,正数1

- 字符串函数
  - CHAR_LENGTH('XXX') 字符串长度
  - CONCAT('A','B','C')--- 拼接字符串
  - INSERT('被插入的对象',首位置,截至位置,'插入的字')---从某个位置替换某个长度
  - LOWER(XX) ---转小写
  - UPPER(XX) -- 转大写
  - REPLACE('主字符串','要替换的','替换内容') --- 替换指定的字符串
  - SUBSTR('主字符串',开始位置,长度)   ---截取字符串,
  
- 聚合函数
  - COUNT('字段')  --忽略所有的null
  - COUNT(*)  --- 不会忽略null,本质计算行数
  - COUNT(1) ---本质计算行名
  
  - SUM()  总和
  - AVG()   平均
  - MAX()   最大
  - MIN()   最小 
  

- MD5
> 注意:得设置长度50以上
  - update改的密码:::password = MD5(password)
  - 插入加密:  insert into testmd5(`name`,`password`) values('zjz',MD5('123456'));
  - 都可以嵌套好几层...
## ORACLE





