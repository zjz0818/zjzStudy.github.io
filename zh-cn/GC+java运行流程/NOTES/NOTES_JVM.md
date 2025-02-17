## JVM
- 在java目录下

## java栈的参数
- -Xss 设置栈大小，通常几百K就够用了。


## java堆的参数
| 参数                            | 描述                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| -Xms                            | 堆内存初始大小                                               |
| -Xmx（MaxHeapSize）             | 堆内存最大允许大小，一般不要大于物理内存的80%                |
| -XX:NewSize（-Xns）             | 年轻代内存初始大小                                           |
| -XX:MaxNewSize（-Xmn）          | 年轻代内存最大允许大小，也可以缩写                           |
| -XX:NewRatio                    | 新生代和老年代的比值<br/>值为4 表示 新生代:老年代=1:4，即年轻代占堆的1/5 |
| -XX:SurvivorRatio=8             | 年轻代中Eden区与Survivor区的容量比例值,默认为8<br />表示两个Survivor :eden=2:8，即一个Survivor占年轻代的1/10 |
| -XX:+HeapDumpOnOutOfMemoryError | 内存溢出时，导出堆信息到文件                                 |
| -XX:+HeapDumpPath               | 堆Dump路径<br />-Xmx20m -Xms5m<br />-XX:+HeapDumpOnOutOfMemoryError<br />-XX:HeapDumpPath=d:/a.dump |
| -XX:OnOutOfMemoryError          | 当发生OOM内存溢出时，执行一个脚本<br />-XX:OnOutOfMemoryError=D:/tools/jdk1.7_40/bin/printstack.bat %p<br />%p表示线程的id pid |
| -XX:MaxTenuringThreshold=7      | 表示如果在幸存区移动多少次没有被垃圾回收，进入老年代         |



