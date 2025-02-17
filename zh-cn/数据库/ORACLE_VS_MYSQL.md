# select操作
- 很相似
- where的使用 groupby的使用 聚合函数的使用 
- 子查询页类似

  - 其中分页查询 oracle 用伪列 ROWNUM    SQL 用limit
    ```
    oracel 
    select t.row1,t.row2
    from(
     select row1,row2,ROWNUM rn
     from table1
     where ROWNUM >5
    )t
    where t.rn<10
    ```
    
    ```
    SQL
    select *
    from table1
    LIMIT 0,50;  ---没where……
    ```

- 字符串的模糊比较
    - MYSQL里用 字段名 like '%字符串%',
    - ORACLE里也可以用 字段名 like '%字符串%' 但这种方法不能使用索引, 速度不快，
    - 用字符串比较函数 **WHERE instr(字段名,'字符串')>0** 会得到更精确的查找结果。

    ```
    SELECT CLIENT_NO
    FROM CIF_CLIENT_DOCUMENT
    WHERE INSTR(CLIENT_NO,'10000001')>0
    
    ```

- 空字符的处理
    - **MYSQL**的**非空字段也有空的内容**，ORACLE里定义了非空字段就不容许有空的内容。
    - 按MYSQL的NOT NULL来定义ORACLE表结构, 导数据的时候会产生错误。
    - 因此导数据时要对空字符进行判断，如果为NULL或空字符，需要把它改成一个空格的字符串。

## 一、并发性

- 并发性是oltp数据库最重要的特性，但并发涉及到资源的获取、共享与锁定。

    - mysql:
    - mysql以表级锁为主，对资源锁定的粒度很大，如果一个session对一个表加锁时间过长，会让其他session无法更新此表中的数据。
    - 虽然InnoDB引擎的表可以用行级锁，但这个行级锁的机制依赖于表的索引，如果表没有索引，或者sql语句没有使用索引，那么仍然使用表级锁。
    
    - oracle:
    - oracle使用行级锁，对资源锁定的粒度要小很多，只是锁定sql需要的资源，并且加锁是在数据库中的数据行上，不依赖与索引。所以oracle对并发性的支持要好很多。

## 二、一致性
- oracle:
- oracle支持serializable的隔离级别，可以实现最高级别的读一致性。每个session提交后其他session才能看到提交的更改。oracle通过在undo表空间中构造多版本数据块来实现读一致性，
- 每个session查询时，如果对应的数据块发生变化，oracle会在undo表空间中为这个session构造它查询时的旧的数据块。
- mysql:
- mysql没有类似oracle的构造多版本数据块的机制，只支持read commited的隔离级别。一个session读取数据时，其他session不能更改数据，但可以在表最后插入数据。
- session更新数据时，要加上排它锁，其他session无法访问数据。

## 三、事务
- oracle很早就完全支持事务。
- mysql在innodb存储引擎的行级锁的情况下才支持事务。

## 四、数据持久性
- oracle
    - 保证提交的数据均可恢复，因为oracle把提交的sql操作线写入了在线联机日志文件中，保持到了磁盘上，
    - 如果出现数据库或主机异常重启，重启后oracle可以考联机在线日志恢复客户提交的数据。
- mysql:
    - 默认提交sql语句，但如果更新过程中出现db或主机重启的问题，也许会丢失数据。

## 五、分页查询

- MySQL是直接在SQL语句中写"select... from ...where...limit  x, y",有limit就可以实现分页;
- 而Oracle则是需要用到伪列ROWNUM和嵌套查询

## 六、提交方式
- oracle默认不自动提交，需要用户手动提交。
- mysql默认是自动提交。

## 七、逻辑备份

- oracle逻辑备份时不锁定数据，且备份的数据是一致的。
- mysql逻辑备份时要锁定数据，才能保证备份的数据是一致的，影响业务正常的dml使用。

## 八、热备份
- oracle
    - 有成熟的热备工具rman，热备时，不影响用户使用数据库。即使备份的数据库不一致，也可以在恢复时通过归档日志和联机重做日志进行一致的回复。
- mysql:
    - myisam的引擎，用mysql自带的mysqlhostcopy热备时，需要给表加读锁，影响dml操作。
    - innodb的引擎，它会备份innodb的表和索引，但是不会备份.frm文件。用ibbackup备份时，会有一个日志文件记录备份期间的数据变化，因此可以不用锁表，不影响其他用户使用数据库。但此工具是收费的。
    - innobackup是结合ibbackup使用的一个脚本，他会协助对.frm文件的备份。

## 九、sql语句的扩展和灵活性
- mysql对sql语句有很多非常实用而方便的扩展，比如limit功能，insert可以一次插入多行数据，select某些管理数据可以不加from。
- oracle在这方面感觉更加稳重传统一些。

## 十、复制
- oracle:既有推或拉式的传统数据复制，也有dataguard的双机或多机容灾机制，主库出现问题是，可以自动切换备库到主库，但配置管理较复杂。
- mysql:复制服务器配置简单，但主库出问题时，丛库有可能丢失一定的数据。且需要手工切换丛库到主库。


## 十一、权限与安全

- mysql的用户与主机有关，感觉没有什么意义，另外更容易被仿冒主机及ip有可乘之机。
- oracle的权限与安全概念比较传统，中规中矩。

## 十二、分区表和分区索引
- oracle的分区表和分区索引功能很成熟，可以提高用户访问db的体验。
- mysql的分区表还不太成熟稳定。

## 十三、管理工具
- oracle有多种成熟的命令行、图形界面、web管理工具，还有很多第三方的管理工具，管理极其方便高效。
- mysql管理工具较少，在linux下的管理工具的安装有时要安装额外的包（phpmyadmin， etc)，有一定复杂性。


## 十四、性能诊断
- oracle有各种成熟的性能诊断调优工具，能实现很多自动分析、诊断功能。比如awr、addm、sqltrace、tkproof等
- mysql的诊断调优方法较少，主要有慢查询日志。



# 建表的不同：

| 名称          | mysql                   | Oracle                         |
| ------------- | ----------------------- | ------------------------------ |
| 整数          | int（X），bigint（X）   | NUMBER（X）                    |
| 字符串        | varchar(X)              | VARCHAR2（X）                  |
| 浮点型        | decimal(20,2)           | NUMBER(20, 2)                  |
| 日期          | datetime                | DATE                           |
| 自动建ID      | AUTO_INCREMENT          | 没有，可使用创建SEQUENCE的方式 |
| 描述          | COMMENT---注释          | 只描述约束类型CONSTRAINT       |
| 可以NULl      | DEFAULT NULL            | 不写                           |
| 核对？        | COLLATE                 | 没有                           |
| 提交：ENGINE  | ENGINE=InnoDB           | 无                             |
| 提交：CHARSET | CHARSET=utf8            | 无                             |
| 提交；COLLATE | COLLATE=utf8_unicode_ci | 无                             |
|               |                         |                                |
|               |                         |                                |

## InnoDB和MyIASM的区别：



- InnoDB

- 它提供了事务控制能力功能，它确保一组命令全部执行成功，或者当任何一个命令出现错误时所有命令的结果都被回退，可以想像在电子银行中事务控制能力是非常重要的。支持COMMIT、ROLLBACK和其他事务特性。最新版本的Mysql已经计划移除对BDB的支持，转而全力发展InnoDB。

- MyIASM是IASM表的新版本，有如下扩展：
  二进制层次的可移植性。
  NULL列索引。
  对变长行比ISAM表有更少的碎片。
  支持大文件。
  更好的索引压缩。
  更好的键吗统计分布。
  更好和更快的auto_increment处理

- 总之;

  - MyISAM类型不支持事务处理等高级处理，而InnoDB类型支持。
    MyISAM类型的表强调的是性能，其执行数度比InnoDB类型更快，但是不提供事务支持，而InnoDB提供事务支持，外键等高级数据库功能。

- 两者直接的转换；

  - 修改表的引擎类型：

    ALTER
    TABLE tablename ENGINE = MyISAM ；

- 适用：

  - InnoDB INSERT或UPDATE    MyISAM Select

  - MyISAM
    优点：速度快，磁盘空间占用少；某个库或表的磁盘占用情况既可以通过操作系统查相应的文件（夹）的大小得知，也可以通过SQL语句SHOW TABLE STATUS查得
    缺点：没有数据完整性机制，即不支持事务和外键

    InnoDB
    优点：支持事务和外键，数据完整性机制比较完备；可以用SHOW TABLE STATUS查得某个库或表的磁盘占用
    缺点：速度超慢，磁盘空间占用多；所有库都存于一个（通常情况）或数个文件中，无法通过操作系统了解某个库或表的占用空间

    ## Oracle的 自动生成ID

    - 创建SEQUENCE，将列area_id 类ID化--*/

      - drop sequence SEQ_LT_AREA;

      - create sequence SEQ_LT_AREA increment by 1 /*该SEQUENCE以1的步长递增*/

      - start with 1 maxvalue 99999;         /*从1开始，最大增长到99999*/