# 前言
- 索引

## 索引的基本原理
- 索引用来`快速地寻找那些具有特定值`的记录。如果`没有索引`，一般来说执行查询时`遍历整张表`。
> 索引的原理：就是把无序的数据变成有序的查询 -- 哈希索引,BTree-平衡树
 - 1. 把创建了索引的列的内容进行排序
 - 2. 对排序结果生成倒排表
 - 3. 在倒排表内容上拼上数据地址链
 - 4. 在查询的时候，先拿到倒排表内容，再取出数据地址链，从而拿到具体数据




## mysql聚簇和非聚簇索引的区别
> 都是B+树的数据结构
- 聚簇索引：`将数据存储与索引放到了一块`、并且是按照一定的顺序组织的，找到索引也就找到了数
  据，数据的物理存放顺序与索引顺序是一致的，
  即：只要索引是相邻的，那么对应的数据一定也是相邻地存放在磁盘上的----范围查询
- zjz说:key-value是放一起的,找到的是一个Entry....  

- 非聚簇索引：`叶子节点不存储数据、存储的是数据行地址`，也就是说根据索引查找到数据行的位置
  再取磁盘查找数据，这个就有点类似一本树的目录，比如我们要找第三章第一节，那我们先在这个
  目录里面找，找到对应的页码后再去对应的页码看文章。
- zjz说:先找key,然后再去找value


## 数据库中的null和空
- null和提前预定一个位置一样,表示未知的
- 空就没分配内存地址,不存在

## 快排临界值问题
> 快排练习时，对于part部分的左小右大的比较过程。
- 情况是：快排part左小右大，但是需要比较，也需要区间，也就是执行结束的标志。
  - ```java

        int left = L;
        int right = R-1;  // 错误的R-1.
        // 如果这时直接right = R - 1;  当一直从左往右走，而不走大于的交换的时候，那就会导致下面循环部分是L<R-1,直接少两个长度，而我们不计算的只有R
          // 临界线要考虑好！。
        while (left<right){
            if (arr[left]<=arr[R]){
                left++;
            }else if (arr[left]>arr[R]){
                swap(arr,left,right);
                right--;
            }
        }
  ```
- 推荐先直接L,R,下面操作时直接先减减再操作，保证数据全面性。  
  - ```java
        int left = L;
        int right = R;  
        while (left<right){
            if (arr[left]<=arr[R]){
                left++;
            }else if (arr[left]>arr[R]){
                right--;  // 或者下面括号里--right
                swap(arr,left,right);
                
            }
        }

```

