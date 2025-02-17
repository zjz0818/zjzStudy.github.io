# 以后改变编码,提高性能
> Direction Matter
> 
- 2021.9.27以后:
- 1.三目:判断全用!!! 获取最大最小,与**值有关系的,字符串啥的**
    - x=x<y? exA:exB
  
- 2021.9.29以后
- 如果在for里有if判断,直接将判断语句写在for中
  - 如:for (int j = i; j > 0 && (arr[j]<arr[j-1]); j--)
- 如有指针，必定用while，因为while方便`控制指针的移动不移动`！！！ 

- throw new RuntimeException("..."); 一般自己手动抛异常用这个

> Math.abs(); 
- 绝对值用起来。。

> 元素的进出考虑队列和栈
> 为啥不用数组，因为对于一些链表，树来说，你都没法知道长度，没法定义长度的。

## 链表题
> 必备指针--每次操作都得遍历,都得next,所以必备当前cur指针(Node型)--链表指针都是Node型
- 链表题必备的**自己指针** Node cur = head; 执行体内`要做next或者其它操作进行找到下一个对象`..
- `涉及next` 必备 **next指针**  Node next = null; // 初始化next指针

## zjz以后的操作:-三部曲:编注释,编代码,核查
- 每次做题,正常编写--先写注释:输入,输出,正确性,健壮性-->高效率--五要素
- 最后满足条件再删除(核查)



- 口诀:常对幂指阶

## 自定义类和方法时
- 发现如果要满足一些实际要求,为了健壮性,必须得抛异常
- 要不你的整个程序还是会执行下去的
- 抛异常并结束
  
  ```
      if(Date1.length()!=8){
          try{
              throw new Exception(Date1+"日期错误");
          }catch (Exception e){
              System.out.println(Date1+"日期错误");
              System.exit(0);
          }
      }

  ```

- List.forEach(System.out::println); list的遍历(必须会)--Set也可以
  - set.forEach(System.out::println);
- Array.asList(1,2,3);  必须得了解到

- 虚假唤醒: 等待应该总存在循环中--->放在while()
- if判断,只会判断一次,while是总是会去判断

### 解决死锁
> 控制台
- 1.用`jps - l`定位进程号:
  - 有时候忘了关线程
- 2.使用`jstack进程号` 找到死锁问题



### 数据库MD5
> 注意:得设置长度50以上
- update改的密码:::password = MD5(password)
- 插入加密:  insert into testmd5(`name`,`password`) values('zjz',MD5('123456'));
- 都可以嵌套好几层...

### 偷懒创建数据库表
- show create table user;

### reids的使用
- 1.查看面板入口：/etc/init.d/bt default
- 我的服务器---39.105.113.11
- 查看进程- 查看端口：:ps -ef|grep redis

> 登录操作:
- 服务端启动::redis-server zjzconfig/redis.conf  ./redis-server   redis.conf
- 连接redis的客户端- redis-cli --raw -p 63799 ----之前6379改成现在的63799
- 进入redis:./redis-cli -h localhost -p 63799  
- config get requirepass  获取密码
- config set requirepass  设置密码  // 或者直接配置文件写
- 设置后,每次进去都得先auth 密码   ---登录

- 从机要配置文件masterauth 密码


- 我本来是使用的bind，但是无论我bind什么ip,localhost,本机的ip(47.xx.xx.xx)都不行
- 后来我才明白，应该绑定阿里云的内网ip。

### 判断
- 不满足的用 `||` 来进行   多条件`有一个触发就触发`
- 满足的用 `&&` 来进行 多条件`都满足才触发`
  
> if的使用
- 如果`前一个if`和`后一个if`有关系，那么`else if`连接起来。要不前一个`运行后的结果`，后一个`依据前一个的结果`走。

- 备注:PS



### LINUX
- grep mysql /root/install.log   查找 /root/install.log 文件中包含 mysql 字符串的行，并输出
- grep -iv "#" redis.conf   `不要#`的查询
- du -sh *  // 看文件磁盘内存  -- 一般是进程僵死（Stop停不来）使用
- df -h  // 看总的磁盘内存及其使用率
- free -m //free是显示的当前内存的使用
- rm -rf XXX* 删除XXX---，使用*来进行通配
- less -f 来查看文件不错。。可以/进行搜索
- netstat -nplp 查看启动得服务
- find / -name redis-server 查找文件
- find ./ -name "*" | xargs grep "寻找內容"  --- 找到有这些內容的文件
- sz 文件名 ---下载文件
- rz 上传文件
- grep mysql /root/install.log   查找 /root/install.log 文件中包含 mysql 字符串的行，并输出
- grep -iv "#" redis.conf   不要#的查询
- grep -rl "查询"

- CMD命令
- xcopy /e /y D:\tmp\sss\ D:\tmp\132\   ----将sss目录下的所有内容覆盖132目录



## 字符串使用
- 隔离::新的字符串数组 = 旧字符串.split(切割符); -- 切割符可以是任何字符
- 字符串反转:使用StringBuilder或者stringBuffer的reverse()方法。
- ss.charAt(i); 字符串切分,
- char[] chars = str.toCharArray();  // 直接转为字符数组
- str.lastIndexOf('a'); // 最后一个a的位置
- str.substring(起始,末尾);  // 输入一个X就是[X--尾),鸡头不鸡尾 
- String.split("\\\\") 


## 输入中断
> 关键while是一直运行的
- 1.肯定得有循环,以及判断,所以必须有while
- 2.肯定有输入
- 3.判断输入的是否为0,不是则继续..直接while(输入语句!=0)


## 统计,总数
- 考虑是不是 1 1 3 5 8
- 这样判断是不是`斐波那契数列`


## 算法中
- 无限迭代
- ```
      Scanner scanner = new Scanner(System.in);
        while (scanner.hasNext()){
           scanner.nextInt();
        }
  
  ```

## LinkedList
- peek()---获取但不移除此列表的头（第一个元素）。
- Deque<Integer> nums = new LinkedList<>(); // 先进去的先出来
  - push 头增 add尾增 pop 头弹 


## 要返回两个值怎么办?
- 正常类型:数组?
  
> 自定义类
- 如果是一个boolean,一个是数字? --- 自己定义一个Bean,里面构造两个值的返回
  - 此时这个Bean就是一个对象,属性也就是我们要的值..

## 算法
- 算法模板建设,不带模板上考场,就是和裸奔差不多!

## 使用set判断有没有这个元素
- set.contains(X);
- set本身就是判断重复的,利用while(!set.contains(X));可以操作一些想要的处理流程!!
> map也有  
- map.containsKey('1');
- map.containsValue("1");

## Stack的使用
- stack的peek,就是`看`下当前栈顶的节点---用于做判断!



## Integer
> 常用的
- Integer.MIN_VALUE; // -2147483648
- Integer.MAX_VALUE; // 2147483647
- Integer.toBinaryString(intTemp); // 10转2
- Integer.toHexString(intTemp); // 10转16
- Integer.toHexString(intTemp); // 10转8

## 判断是否是2的幂
- (n&(n-1))==0;
- 原理:减1后,就会和原本完全不一样.如2的10变为1的01,再&之后就会变为0

## 字母对应下标
- `index = chs[i]-'a';`
  - chs中的i指的是,可能是一个字符串,然后用for便可以一个个闹出来.
- String转字符数组
  -  `char[] chars = ss.toCharArray();`
- String的数组,每个都转字符串


## While和For
- 初始就是初始,里面的条件判断就是卡标!! 
  - 有等于就是按[]来,没就是按()来
  


## 比较器(排序)
> 一般常用数组排序(Arrays.sort()),集合排序(Collections.sort())
> Comparator接口(推荐)
> 需要两部，一是实现比较类，二是使用时后面加自定义类
### 1.代码,写自定义类。
- ```
       public static class MyCompare implements Comparator<ComPPP> {
  
          @Override
          public int compare(ComPPP o1, ComPPP o2) {
              return o1.getAge()- o2.getAge();
          }
  
      }
    
  ```

> 多条件，在重写时，可以添加判断
- `if(o1.tj1 == o2.tj1){return o1.tj2-o2.tj2;}`
- 字符串的比較`(o1).compareTo(o2);`

### 2.使用时:Arrays.sort(对象数组,MyCompare);
> 在后面的练习中发现, Arrays.sort(Object[],new MyComparator());比较的是对象,不能是基本类型
- 仅仅使用Arrays.sort(arr[]);时可以是基本类型




> Comparable
- 1.需要这个对象类implements Comparable
- 2.代码中编写
- ```
    public static class ComPPP implements Comparable<ComPPP> {
       @Override
        public int compareTo(对象 newTemp) {
            return 属性类型(Integer).compare(this.属性,newTemp.属性);
        }
    }  
  ```
- 3.Arrays.sort(对象数组); // 比的时候只在ComPPP起作用,其它的还是默认的.

> treeMap比较器，用于不创建java类，直接使用map来进行
- 一个map是用来存之前的，然后treemap使用时，需要把之前的map导入到treemap
- ```
    static class StudentGradeCompare implements Comparator<String>{

        Map<String, StudentGrade> base;
        //这里需要将要比较的map集合传进来
        public StudentGradeCompare(Map<String, StudentGrade> base) {
            this.base = base;
        }
        public int compare(String o1, String o2) {
            if (base.get(o1).getGS() == base.get(o2).getGS()){
                return (o1).compareTo(o2);
            }else {
                return -(int)(base.get(o1).getGS()-base.get(o2).getGS());
            }
        }
    }
  ```
  
- ```
     for (Map.Entry<String, StudentGrade> entry : map.entrySet()) {
            String mapKey = entry.getKey();
            StudentGrade mapValue = entry.getValue();
            treemap.put(entry.getKey(),entry.getValue());
        }
  
  
  ```



> 逆序Sort
- 实现方法Arrays.sort(Object[],Collections.reverseOrder());
- 只能是对象类型的.....




## MYSQL
- 不等于 --使用`<>`

## Math
- Math.sqrt()//计算平方根
- Math.cbrt()//计算立方根
- Math.pow(a, b)//计算a的b次方


## 整数
- 判断除以一个数后是不是整数((double)a)/b==a/b
- 对于整数除法,,除了直接切掉后面的,比如9/2直接就是4--老是忘...




## 二维数组
- `arr[行数][列数]`
- 对于数组,以后直接精确使用`[]`,,不再使用<..要直接使用能等于的,方便思考


## 输出数字格式
- 使用DecimalFormat方法
  - ` DecimalFormat df = new DecimalFormat("#0.00");`
- 它的使用是截取数,后面几位数如果大于500,则入,如5.55501它会5.56  

- System.out.format("%.1f",PI); 会四舍五入

## 不重复且排序
- 要注意的是hashSet在一些情况下是会自动排序的,但是数据量大的情况下是不会排序的
- 要使用的话,最好直接使用treeSet
- 要明白的是set只能foreach,不能根据下标进行输出,很恶心...需要进行转换toArray或者其它


## Character的大小写转换
- char s = Character.toLowerCase(c);大转小
- char S = Character.toUpperCase(c);小转大


## 最大公约数
> 辗转相除法
- 用前一个被余数,再取余--余数
- ```
      public static int gcd(int q,int p){
        if (p == 0){
            return q;
        }

        int r = q % p ;
        return gcd(p,r);
    }
  
  ```

## 链式编程
> 在set时候直接`return this`；
- ```
  
    public StudentGrade setGP(int GP) {
                this.GP = GP;
                return this;
            }
  ```

## 测试总结
- 对于一些测试来说,我仅仅需要看到某一部分的结果.直接针对这一部分进行功能测试就行.比如直接运行它.


## 异常的一些总结
- 对于未进行try/catch的异常，会直接中断整个程序
- 对于有try/catch的异常，我们可以捕获到输出异常，下面的程序正常执行


## 对于是不是数字的判定
- Character.isDigit('只能一位'); 返回一个boolean

## 解读一个代码
> 解读代码的流程:
- 1.主函数调用哪几个函数
- 2.进入调用的函数,先看入参,出参,(明白大概要干个啥),观看涉及,以及逻辑---注意return...
- 3.循环第二步,注意之前调入函数的入参是否已经是处理过的,最好的方法就是弄个例子一走


## 关于for
- for (初始表达式; 条件表达式;迭代表达式)
- 初始表达式，得赋值，要不null
- 得变化或者赋值，要不null

## 递归
> 过程型的东西，或者说单个元素走向就该考虑递归了
- 递归里不要使用flag进行标记true,false,如果false要return就直接return,要不下波数据进来就不一定是想要的结果了



## 关于++和+1
- 在一些判断中只允许使用x+1,不允许x++,进行x++后，接下来的x就已经是加1之后的x了



## ORACLE
-  多个like
- ```
    SELECT * FROM ENSEMBLE.FM_CHECK_CHANNEL_TRANINFO
    WHERE regexp_like (PROGRAM_ID,'^(PT|5210)')
    ORDER BY PROGRAM_ID;
    
    1.查询 md003 包含 LT或C或ST的数据
    select * from sys_ggbom
    where regexp_like (md003,'(LT|C|ST)')
    
    
    2.查询 md003 以 HT 开头的数据
    select * from sys_ggbom
    where regexp_like (md003,'^(HT)')
    
    
    3.查询 md003 以 HT 结尾的数据
    select * from sys_ggbom
    where regexp_like (md003,'(HT)$')
  
  
  ```

## GIT 
> git终止
- git merge --abort

## Linux定時任務
- crontab -u //设定特定用户的定时服务
- crontab -l //列出当前用户定时服务内容
- crontab -r //删除当前用户的定时服务
- crontab -e //编辑当前用户的定时服务


## IO
- DIR *.* /S/ON/B>LIST.TXT 用bat执行可导出当前目录下的文件的全路径
