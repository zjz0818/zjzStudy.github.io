## DML用于改变数据库中的数据，主要是包括：
- INSERT 
- UPDATE 
- DELETE

## insert
- 向表中插入数据
    ``` 
    insert into 表名(列1,列2,..) values(值1,值2,...);
    ```

- 默认是向表中的每一个列中【依次】插入数据，需要和**列声明的顺序一致**

- insert语句中，最后面的那个关键字是 values ，而不是 value
    ```
       insert into表名(列1,列2,列3,列XX....) values(X,X,X,X,...)
       //多行插入
       insert into users(id,name,password,email,birthday)
       values(2,'李四','123456','zjz02@qq.com','2020-08-29'),
             (3,'王五','123456','zjz03@qq.com','2019-08-29'),
             (4,'赵六','123456','zjz04@qq.com','2018-08-29'),
             (5,'田七','123456','zjz05@qq.com','2017-08-29');
    ```

## update 
    ```
    update 表名 set 列1=值1,列2=值2,.... where 条件;
    ```

## delete
    ```
    delete from 表名 where 条件;
    ```
- 注意，如果不加条件，就表示把表中所有数据删除


## on delete
- 在外键约束后面加
    ```
    create table t_order( 
    id number, 
    price number, 
    customer_id number, 
    constraint order_id_pk primary key(id), 
    constraint order_cid_fk foreign key(customer_id) references t_customer(id) 
    on delete set null );
    ```
- 用户在删除A表中的一条数据，而这条数据被B表中的外键列所引用了，这个时候 on delete xxx 语句的设置可以告诉oracle这个时候该如何处理
    - 1. on delete no action 删除时报错：ORA-02292: 违反完整约束条件 - 已找到子记录
    - 2. on delete cascade   删除操作成功时，同时级联(cascade)删除了，t_order表中所关联的那条数据
    - 3. on delete set null  删除操作成功时，同时把t_order表中所关联的那条数据的外键设置为了null
    - 例如，如果在建外键的时候，不加on delete语句，默认就是 on delete no action

