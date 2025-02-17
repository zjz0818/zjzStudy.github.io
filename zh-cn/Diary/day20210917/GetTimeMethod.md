# GetTime
> 获取时间的方式
> 
> new Date();  ---- Calendar
> 
> 
> 强大的SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");//设置日期格式 df.format();
> 
> simpleDateFormat.parse(字符串);
> 
> java，sql互转
> 



## java Date 
- java.util.Date日期格式为：年月日时分秒



## Mysql Date
- MySQL 日期类型：日期格式
-       datetime ------ YYYY-MM-DD HH:MM:SS   存储：8bytes
-       timestamp------  YYYY-MM-DD HH:MM:SS 存储：4bytes
-       date    -----YYYY-MM-DD              存储：3bytes
  - 1. timestamp容易所支持的范围比timedate要小。 并且容易出现超出的情况
  - 2.timestamp比较受时区timezone的影响以及MYSQL版本和服务器的SQL MODE的影响.

## Calendar的方式
- `public abstract class Calendar extends Objectimplements Serializable, Cloneable, Comparable<Calendar>
- 抽象类，不能new一个
- Calendar提供了一个类方法getInstance，以获得此类型的一个通用的对象，
  **getInstance方法返回一个Calendar对象**（该对象为Calendar的子类对象），其日历字段已由当前日期和时间初始化
  
- 关键：getinstance(); 获取一个对象
  - set 操作 
    - 多个;cal.set(year, month, date, hourOfDay, minute, second);
    - 单个：
      - cal.set(Calendar.YEAR, 2018);
      - cal.set(Calendar.MONTH, Calendar.FEBRUARY);
      - cal.set(Calendar.DAY_OF_MONTH, 15);
      - cal.set(Calendar.HOUR_OF_DAY, 23);
      - cal.set(Calendar.MINUTE, 59);
      - cal.set(Calendar.SECOND, 59);
    
  - get 操作
    - calendar.get(Calendar.YEAR);
    - calendar.get(Calendar.MONTH) + 1;  // 获取当前月，特例！
    
  - 时间计算：add 操作
    -  cal.add(Calendar.SECOND, 1); // 加一秒
  

```
    Calendar instance = Calendar.getInstance();
    Date time = instance.getTime(); // Fri Sep 17 14:20:47 CST 2021
    
    
    	// 获取年
        int year = calendar.get(Calendar.YEAR);

        // 获取月，这里需要需要月份的范围为0~11，因此获取月份的时候需要+1才是当前月份值
        int month = calendar.get(Calendar.MONTH) + 1;

        // 获取日
        int day = calendar.get(Calendar.DAY_OF_MONTH);

        // 获取时
        int hour = calendar.get(Calendar.HOUR);
        // int hour = calendar.get(Calendar.HOUR_OF_DAY); // 24小时表示

        // 获取分
        int minute = calendar.get(Calendar.MINUTE);

        // 获取秒
        int second = calendar.get(Calendar.SECOND);

        // 星期，英语国家星期从星期日开始计算
        int weekday = calendar.get(Calendar.DAY_OF_WEEK);
        
        
        // 同理换成下个月的今天calendar.add(Calendar.MONTH, 1);
           calendar.add(Calendar.YEAR, 1);
    
    
    

```
  
        



# java，sql互转----记住getTime()方法    
> XXX x = new XXX（z.getTime()）;**核心**！



- java.sql.Date转为java.util.Date
  - java.sql.Date date=new java.sql.Date();
  - java.util.Date d=new java.util.Date (date.getTime());
  
- java.util.Date转为java.sql.Date
  - java.util.Date utilDate=new Date();
- Date类型    
  - java.sql.Date sqlDate=new java.sql.Date(utilDate.getTime());
- Time类型
  - java.sql.Time sTime=new java.sql.Time(utilDate.getTime());
- Timestamp类型    
  - java.sql.Timestamp stp=new java.sql.Timestamp(utilDate.getTime());







