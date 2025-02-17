# JavaBean
## 实体类
- javabean有特定的写法
    - 必须要有一个无参构造器
    - 属性必须私有化
    - 必须要有对应的get/set方法
- 一般用来和数据库的字段做映射 ORM
- ORM：对象关系映射
    - 表       --类
    - 字段    --属性
    - 行记录  --对象

| id   | name | age  | address |
| ---- | ---- | ---- | ------- |
| 1    | zjz1 | 3    | 山西    |
| 2    | zjz2 | 22   | 吕梁    |
| 3    | zjz3 | 100  | 西安    |



```
class people{
	private int id;
	private String name;
	private String age;
	private String address;
	
}
class A{
  new People(1,"zjz1","3","山西");
  new People(2,"zjz2","22","吕梁");
  new People(3,"zjz3","100","西安");
}

```

