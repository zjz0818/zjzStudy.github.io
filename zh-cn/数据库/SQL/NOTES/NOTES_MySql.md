# MySql




## 创建Mysql表的两个引擎:
- 数据表的类型:
 - INNODB 默认使用:--行锁
 - MYISAM 早些年---表锁

|              | MYISAM | INNODB       |
| ------------ | ------ | ------------ |
| 事务支持     | 不支持 | 支持         |
| 数据行锁定   | 不支持 | 支持         |
| 外键约束     | 不支持 | 支持         |
| 全文索引     | 支持   | 不支持(现在支持)       |
| 表空间的大小 | 较小   | 较大,约为2倍 |

- 常规使用操作
  - MYISAM 节约空间,速度快
  - INNODB 安全高,事务处理,多表多用户操作

> 在物理空间上存在的位置
- 所有的数据库文件都存在data目录下
- 本质还是文件的存储
- MySql引擎在物理文件上的区别
 - innoDB 在数据库表中中有一个*.frm文件,以及上级目录的ibdata1文件
 - MYISAM 对应文件
    - *.frm -表结构的定义文件
    - *.MYD 数据文件(data)
    - *.MYI 索引文件
    

> 设置数据库表的字符集编码   
- CHARSET=utf8
- 默认Latin1,不支持中文的




### 数据库函数
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
- 时间函数
  - current_timestamp()

- MD5
> 注意:得设置长度50以上
- update改的密码:::password = MD5(password)
- 插入加密:  insert into testmd5(`name`,`password`) values('zjz',MD5('123456'));
- 都可以嵌套好几层...




### 数据库索引:
- 定义:索引(Index)是帮助`MySQL高效获取数据的数据结构`.提取句子主干,就可以得到索引的本质:`索引就是数据结构`

> 索引分类;
> 
> 在一个表中,主键索引可能只有一个,唯一索引可能有多个
- 主键索引:primary
  - 唯一的标识,不可重复,只能有一个列作为主键
- 唯一索引:unique
  - 避免重复的列出现,唯一索引可以重复,多个列都可以标成唯一索引
- 常规索引:(key/Index)
  - 默认的,index或key设置
- 全文索引:FUllText
  - 特定的数据库才有,MyISAM
  - 快速定位数据
    

### 索引的使用:
- 1.创建表的时候给字段增加索引
- 2.创建完毕后alert增加..
 - ALTER TABLE mybatis.`blog` ADD FULLTEXT INDEX `title`(`title`)
- CREATE INDEX id_blog_title ON blog(`title`); // 创建索引

- 查看:show index from 表
- EXPLAIN 分析SQL的执行状况


### 测试索引
- 插入100万条数据
  
  ``` 
    DELIMITER $$
    CREATE FUNCTION XX()  
    RETURNS INT  DETERMINISTIC
    BEGIN
        DECLARE num INT DEFAULT 1000000;
        DECLARE i INT DEFAULT 10;
        WHILE i<num DO
            INSERT INTO blog(`id`,`title`,`author`,`views`) VALUES(i,CONCAT('zjz',i),CONCAT('zjz',i),i);
            SET i = i+1;  
        END WHILE;
        return i;  
    END;


    SELECT XX();
   
   ```
  
- 测试索引::::

    ```
           DELIMITER $$
           CREATE FUNCTION XX()  
           RETURNS INT  DETERMINISTIC
           BEGIN
             DECLARE num INT DEFAULT 1000000;
             DECLARE i INT DEFAULT 10;
             WHILE i<num DO
               INSERT INTO blog(`id`,`title`,`author`,`views`) VALUES(i,CONCAT('zjz',i),CONCAT('zjz',i),i);
                 SET i = i+1;  
               END WHILE;
               return i;  
           END;
         
         
         SELECT XX();
         
         INSERT INTO blog(`id`,`title`,`author`,`views`) VALUES(1111,CONCAT('zjz',1),CONCAT('zjz',1),1)
         
         
         SELECT * FROM blog WHERE `title`  = 'zjz9999'
         
         
        EXPLAIN  SELECT * FROM blog WHERE `title`  = 'zjz9999'
         
        CREATE INDEX id_blog_title ON blog(`title`); 
    
    ```

## 索引原则
- 1.索引不是越多越好
- 2.不要对进程变动数据加索引
- 3.小数据量的表不需要加索引
- 4.索引加在常用来查询的字段上

> 索引的数据结构
- BTREE--INNODB,默认的数据结构
