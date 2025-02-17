## 1.软件开发
```
    软件开发流程，其实就是软件的设计思路和方法的一般过程，其实包括
    分析
    设计
    编码
    测试
    部署
    上线
    运维

```
## 2.数据建模
- 主要是要抽象出系统中所涉及到的实体，以及它们之间的关系。
- 此过程一般需要经过三个阶段：
    - 概念建模:是一个迭代的过程，需要反复多次的和客户沟通、理解和确认。(客户交流 理解需求 **形成实体**)
    - 逻辑建模:形成具体的E-R图（实体关系图），这张关系图中详细记录了**实体信息**，同时展示了**实体与实体之间的关系**。
    - 物理建模:逻辑建模阶段创建的实体关系图，根据选择使用的数据库，转为相应的 **SQL代码**


## 构成ER图的三大要素有：
   - 实体
   - 属性
   - 关系



# 数据库设计
- 数据建模完成之后，可以把E-R图转换成数据库中的表：
    - 实体的名字转换为表的名字
    - 实体的属性转换为表中的列 
    - 具有唯一特点的属性设置为表中的主键(主键的作用，就是用来唯一标识一行数据的)
    - 根据实体之间的关系，设置表中某列为外键列（主外键关联）
- 外键
    - 外键的作用，就是用来标识这个类中的数据，是引用另一种表的一个字段值

## 范式
- 第一范式 一个表中，每个列里面的值是**不能再分割**的。
- 第二范式 是在满足第一范式的基础上，表中的**非主键列都必须依赖于主键列**
- 第三范式 在满足第二范式的基础上，表中的非主键列都必须直接依赖于主键列，而**不能间接的依赖**，也就是不**能出现依赖传递**

## 建表：
- 建表过程中，需要以下几种东西: 
   - 1. 关键字
   - 2. 表名
   - 3. 列名
   - 4. 数据类型
   - 5. 约束
   - 6. 固定格式
    
    ```
    create table 表名( 
    字段名 数据类型 [列约束类型], id number  primary key, //主键
    字段名 数据类型 [列约束类型], name varchar2(200) not null, // 一般判断null，不加就是可null
    字段名 数据类型 [列约束类型], unique, // 唯一
    字段名 数据类型 [列约束类型], gender char(1) check(gender in('f','m')), //check 约束
    字段名 数据类型 [列约束类型],table1_id number references table2_名称(id) //外键
    对于外键 删除外键的表时  drop table table2_名称 cascade constraints; //cascade 级联删除与表相关的约束
    [表级约束], [表级约束] );primary key(id),foreign key(table1_id) references table2_名称(id)
    ```
  
### 数据类型 
- 1. char **varchar** varchar2 都是存储字符串
    - char 存储数据的长度是固定的。
    - varchar2 存储数据的长度是可变的。
    - char 效率比 varchar2效率高。 
    - varchar是数据库标准类型，varchar2类型是oracle数据库中特有的
    - varchar2不能存空字符串，可以存null。varchar可以存空字符串
    - Oracle建议使用VARCHAR2 
- 2. number(p,s) p 表示最大位数（整数位+小数位）， s表示保留的小数位（四舍五入），也可以为负数。
    ```
    例如，number(5,2)
    存进去123.456，取出来为123.46
    存进去12345.456，运行报错：值大于为此列指定的允许精度
    ```
    - 注意1，其实这时候整数位最大只能有3位，因为要留俩位给小数位
    - 注意2，可以直接使用number，不加参数，描述没有默认没限制
- 3. **date**   
    - 一般TO_DATE('2021-04-15 00:00:00', 'YYYY-MM-DD HH24:MI:SS')（非常常用）
    - 日期类型
- 4. blob
   - 存二进制对象，例如视频，音频，图片等
- 5. clob
   - 存储大文本，例如很多很多文字

### 约束
- 列的约束，就是对这个列中的值的要求（限制）：
    - 1. 主键约束 PRIMARY KEY primary key
    - 2. 外键约束 FOREIGN KEY foreign key
    - 3. 唯一约束 UNIQUE unique
    - 4. 非空约束 NOT NULL not null
    - 5. check约束 CHECK check

- unique(class,name)
    - 注意，学生的班级和学生的名字，联合起来必须是唯一的(联合唯一)
    - 注意，联合唯一约束必须使用**表级约束**来声明

## 表级约束和列级约束对比：

- 1. 表级约束和列级约束所写的位置不一样
- 2. not null约束不能用表级约束来声明
- 3. 表级约束和列级约束声明语法稍有所不同
- 4. 如果要声明的约束为联合主键、联合外键、联合唯一的时候，就一定要用表级约束


## constraint 关键字：
- 1. constraint是约束的意思
- 2. 建表的时候可以给约束起一个名字，这个名字起的规律一般会是：表名_列名_约束类型
- 3. 如果没有给约束起名字，那么系统也会给这个约束起一个默认的名字
- 4. 将来我们可以根据之前给约束起好的名字，而找到这个约束，然后进行修改获取其他操作


```

```


## 改表：
alter 属于DDL语句，会自动当前事务

在表中添加一个新的列
```
alter table t_user 
add birthday date;
```

删除表的某列
```
alter table t_user 
drop column birthday;
```


给表中的列添加约束'
```
alter table t_user 
add constraint user_name_un 
unique(name);
```


删除表中的约束
```
alter table t_user 
drop constraint user_name_un;
```



修改表的名字
```
rename t_user to mytest;
rename mytest to t_user;
```


让约束失效
```
alter table t_user 
disable constraint user_id_pk cascade;
```

注意，必须知道约束的名字


让失效的约束再次生效
```
alter table t_user 
enable constraint user_id_pk;

```


截断表中的数据(删除)
```
truncate table t_user;
-- 相当于: 
delete from t_user; commit;
```
truncate操作，不需要提交，默认已经提交，并且不能回滚，因为truncate属于DDL操作



## 注释
表已经创建完成之后，可以使用 comment 关键字，给表或者列添加注释


## 序列
序列（Sequence），它也是一种数据库对象。

它作用主要用来帮助表去创建自动增长的主键。
序列是oracle数据库所特有的对象，其他数据库中是没有的。

