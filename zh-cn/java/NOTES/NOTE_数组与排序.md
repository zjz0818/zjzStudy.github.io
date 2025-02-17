## 逆序输出
- 一种直接for里面逆序
- 一种是首尾互换（算法复杂度低）
```java
public class ReverseArray {
    //逆序输出
    public static void main(String[] args) {
        int[]   arr = new int[]{1,2,3,4,5,6,7,8};
        System.out.println(arr.length);
        for(int i = 0;i<arr.length/2;i++){
            int t = arr[arr.length-i-1];
            arr[arr.length-i-1] = arr[i];
            arr[i] = t;
        }
        for(Object o:arr){
            System.out.print(o+" ");
        }
    }

}
```

## 二维数组：
- 一维数组的数组
- 杨辉三角

```java
public class pascal_triangle {
    //杨辉三角：

/*                         
 请输入多少行杨辉三角：
10
1 
1 1 
1 2 1 
1 3 3 1 
1 4 6 4 1 
1 5 10 10 5 1 
1 6 15 20 15 6 1 
1 7 21 35 35 21 7 1 
1 8 28 56 70 56 28 8 1 
1 9 36 84 126 126 84 36 9 1 
*/


    public static void main(String[] args) {
        int[][] arr;
        System.out.println("请输入多少行杨辉三角：");
        Scanner sacnner = new Scanner(System.in);
        int n = sacnner.nextInt();
        arr = new int[n][n];

        int i;
        int j;
        for(i=0;i<arr.length;i++){
            for (j=0;j<=i;j++){
                if(j==0||j==i){
                   arr[i][j] = 1;
                }else{
                    arr[i][j] =arr[i-1][j-1]+arr[i-1][j];
                }
            }
        }
        
        for (int x=0;x<arr.length;x++){
            for(int y=0;y<=x;y++){
                System.out.print(arr[x][y] + " ");
            }
            System.out.println();
        }
    }
}


```

## 基本查找
```java
public class FindArray {
    public  static int [] arr = new int[]{1,2,3,4,5,6,7,8,9};
    public static void main(String[] args) {
        System.out.println("请输入一个数，将在数组中查找：");
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        find(n);
    }

    public static void find(int f){
        for(int i=0;i<arr.length;i++){
            if(i==arr.length-1){ //先判断结束标志
                if (arr[i] == f) {  
                    System.out.println("找到了，索引为：" + i);
                    break;
                }else{
                    System.out.println("没找到");
                    break;
                }
            }else{
                if(arr[i] == f){  //末尾之前的查找
                    System.out.println("找到了，索引为：" + i);
                    break;
                }
            }
        }
    }
}

```

## 二分查找
- 大的时候，左边赋值中间变量 + 1  ---》 left = middl + 1;
- 小的时候，右边赋值中间变量 - 1   ---》 right = middle - 1; 
- 为啥-1 +1 ，中间的肯定不是了啊，不需要它进行比较了（第一波就打掉了）


```java
//二分法查找
public class ErFenFind {
    public static void main(String[] args) {
        int [] arr = new int[]{1,2,3,4,5,6,70,80,90};
        System.out.println("请输入一个数，将在数组中查找：");
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();
        find(arr,n);
    }

    public static void find(int[] arr1, int f){

       int  left = 0;
       int  right = arr1.length-1;
        while(left<=right){
            int middle = (left + right)/2;
           if(f == arr1[middle]){
               System.out.println("找到了，索引为：" + middle);
               break;
           }else if(f < arr1[middle]){
               right = middle - 1;
           }else if(f > arr1[middle]){
               left = middle + 1;
            }
        }
        System.out.println("没找到");
    }
}


```