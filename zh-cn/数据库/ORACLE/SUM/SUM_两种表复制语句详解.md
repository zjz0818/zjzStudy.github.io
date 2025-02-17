- 我们经常会遇到需要表复制的情况，
    - 如将一个table1的数据的**部分字段**复制到table2中，
    - 或者将整个table1复制到table2中，
    - 这时候我们就要使用SELECT INTO 和 INSERT INTO SELECT 表复制语句了。

## 1.INSERT INTO SELECT语句
    ```
    Insert into Table2(field1,field2,...)
    select value1,value2,... from Table1
    ```
- 注意：
    - （1）要求目标表Table2必须存在，并且字段field,field2...也必须存在
    - （2）注意Table2的主键约束，如果Table2有主键而且不为空，则 field1， field2...中必须包括主键
    - （3）注意语法，不要加values，和插入一条数据的sql混了，不要写成:
Insert into Table2(field1,field2,...) **values** (select value1,value2,... from Table1)


## 2.SELECT INTO FROM语句
- 语句形式为：
    ```
    SELECT vale1, value2 
    into Table2 
    from Table1
    ```
- 要求目标表**Table2不存在**，因为在插入时会自动创建表Table2，并将Table1中指定字段数据复制到Table2中。

## create table table名 as select -----
    ```
     create table test1 as select * from s_dept;  //建立一张表和s_dept一模一样，s_dept的表结构和表中的数据全部复制过来
     create table test2 as select * from s_dept where 1=2;//建立一张表和s_dept一模一样，只拿来s_dept的表结构，没有数据
     create table test3 as select id,last_name,salary from s_emp; //建立一张表和s_dept一模一样，只复制表中某几个指定列的数据
    
    ```
 






