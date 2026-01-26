# Java Basics - Array

## Creating and Assignment
- array is a container with a `fixed length`
- element value can be modified
- can only store `identical data type`
- declaring an array
    ```java
    public class Declare{
        public static void main(String[] args){
            // declare the reference a
            // [] indicates this is an array
            // int indicates all elements in array is Integer
            int[] a;
            int a[]; // same
        }
    }
    ```
- creating an array
    - need to point out the `length` of the array
    - reference 
        - is an **identifier** that `points to the memory address` of data
        - does not store the data content itself
    ```java
    public class Declare{
        public static void main(String[] args){
            // declare an reference a
            int[] a;
            // create an array with the length of 5
            // and make a reference point to the array
            a = new int[5];

            // create and declare an array at the same time
            int[] b = new int[5];
        }
    }    
    ```
- length of an array
    - use `.length` to access the length of an array
    - with the range 0 to -1
    - `but Java cannot use negative suffix to get access to elements in array`
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            int[] a; 
            a = new int[5];
            
            System.out.println(a.length); //打印数组的长度 5
            
            a[4]=100; //下标4，实质上是“第5个”，即最后一个 
            a[5]=101; //下标5，实质上是“第6个”，超出范围 ,产生数组下标越界异常
            // java.lang.ArrayIndexOutofBoundsException
        }
    }
    ```
- assignment
    - Allocate space and initialize values simultaneously
    - Allocate space and assign values step by step(2 methods)
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            //写法一： 分配空间同时赋值
            int[] a = new int[]{100,102,444,836,3236};

            //写法二： 省略了new int[],效果一样
            int[] b = {100,102,444,836,3236};
            
            //写法三：同时分配空间，和指定内容
            //在这个例子里，长度是3，内容是5个，产生矛盾了
            //所以如果指定了数组的内容，就不能同时设置数组的长度
            int[] c = new int[5]{100,102,444,836,3236}; //error
        }
    }
    ```
## Sort
- selection sort
    - `compare the first element` with all the other elements. Whenever an element is `smaller than the first one`, `swap it to the first position`
    - then second position and so on
    
        ![selectionSort](..\image\javaArray1.png)
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            int a [] = new int[]{18,62,68,82,65,9};
            //排序前，先把内容打印出来
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");
            //选择法排序
        
            //第一步： 把第一位和其他所有位进行比较
            //如果发现其他位置的数据比第一位小，就进行交换
            
            for (int i = 1; i < a.length; i++) {
                if(a[i]<a[0]){   
                    int temp = a[0];
                    a[0] = a[i];
                    a[i] = temp;
                }
            }
            //把内容打印出来
            //可以发现，最小的一个数，到了最前面
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");
            
            //第二步： 把第二位的和剩下的所有位进行比较
            for (int i = 2; i < a.length; i++) {
                if(a[i]<a[1]){   
                    int temp = a[1];
                    a[1] = a[i];
                    a[i] = temp;
                }
            }
            //把内容打印出来
            //可以发现，倒数第二小的数，到了第二个位置
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");	
            System.out.println("dash");	
            
            //可以发现一个规律
            //移动的位置是从0 逐渐增加的
            //所以可以在外面套一层循环
            
            for (int j = 0; j < a.length-1; j++) {
                for (int i = j+1; i < a.length; i++) {
                    if(a[i]<a[j]){   
                        int temp = a[j];
                        a[j] = a[i];
                        a[i] = temp;
                    }
                }
            }
            
            //把内容打印出来
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");		
        }
    }
    ```
- bubble sort
    - start `from the first element` and compare each pair of `adjacent elements`. If the `former element` is found to be `larger than the latter` one, `swap` the larger element to the latter position
    - repeat
    
        ![selectionSort](..\image\javaArray2.png)
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            int a [] = new int[]{18,62,68,82,65,9};
            //排序前，先把内容打印出来
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");
            //冒泡法排序
        
            //第一步：从第一位开始，把相邻两位进行比较
            //如果发现前面的比后面的大，就把大的数据交换在后面
            
            for (int i = 0; i < a.length-1; i++) {
                if(a[i]>a[i+1]){  
                    int temp = a[i];
                    a[i] = a[i+1];
                    a[i+1] = temp;
                }
            }
            //把内容打印出来
            //可以发现，最大的到了最后面
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");
            
            //第二步： 再来一次，只不过不用比较最后一位
            for (int i = 0; i < a.length-2; i++) {
                if(a[i]>a[i+1]){  
                    int temp = a[i];
                    a[i] = a[i+1];
                    a[i+1] = temp;
                }
            }
            //把内容打印出来
            //可以发现，倒数第二大的到了倒数第二个位置
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");       
            
            //可以发现一个规律
            //后边界在收缩
            //所以可以在外面套一层循环
            
            for (int j = 0; j < a.length; j++) {
                for (int i = 0; i < a.length-j-1; i++) {
                    if(a[i]>a[i+1]){  
                        int temp = a[i];
                        a[i] = a[i+1];
                        a[i+1] = temp;
                    }
                }
            }
            
            //把内容打印出来
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");       
        }
    }
    ```
- exercise
    > First, create an array with a length of 5 and fill it with random integers. 

    > First, sort it in ascending order using Selection Sort, and then sort it in descending order using Bubble Sort.
    ```java
    public class Range{
        public static void main(String[] args) {
            double[] a = new double[5];
            for (int i = 0; i < 5; i++){
                a[i] = Math.random()*100;
            }
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");
            
            System.out.println();

    //        selection sort
            for (int j = 0; j < a.length - 1; j++) {
                for (int i = j + 1; i < a.length; i++) {
                    if (a[j] > a[i]) {
                        double temp = a[j];
                        a[j] = a[i];
                        a[i] = temp;
                    }
                }
            }
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");

    //        bubble sort
            for (int j = 0; j < a.length - 1; j++) {
                for (int i = 0; i < a.length - 1 - j; i++) {
                    if (a[i] < a[i+1]) {
                        double temp = a[i];
                        a[i] = a[i + 1];
                        a[i + 1] = temp;
                    }
                }
            }
            for (int i = 0; i < a.length; i++) {
                System.out.print(a[i] + " ");
            }
            System.out.println(" ");
        }
    }
    ```
## Enhanced for Loop
- a syntax to simplify the traversal of arrays/collections, `without manually controlling the index` (e.g. i)
- syntax: `for (elementType tempVariable : targetArray/collection) { operate on tempVariable };`
- In each loop, the JVM automatically assigns the next element of values to each until all elements are traversed
```java
public class HelloWorld {
    public static void main(String[] args) {
        int values [] = new int[]{18,62,68,82,65,9};
        //常规遍历
        for (int i = 0; i < values.length; i++) {
            int each = values[i];
            System.out.println(each);
        }
         
        //增强型for循环遍历
        // int 匹配数组values的元素类型
        // each是遍历中当前元素的临时变量
        // values是目标数组
        // 
        for (int each : values) {
            System.out.println(each);
        }
    }
}
```
## Copy Array
- System.arraycopy(src,arcPos,dest,destPos,length)
    - `src`: `Source array` (the array to copy elements from)
    - `srcPos`: `Starting position` (index, 0-based) in the source array for copying
    - `dest`: `Destination array` (the array to paste elements to)
    - `destPos`: `Starting position` (index, 0-based) in the destination array for pasting
    - `length`: Number of elements to copy
- notes
    - Source/destination `array types` must be compatible (e.g., int[] copied to int[], not to String[])
    - The destination array must have `sufficient capacity` (otherwise ArrayIndexOutOfBoundsException is thrown)
    - `NullPointerException` is thrown if the array is null
- System.arraycopy() 
    - is a `static` `native` method provided by Java
        - Static
            - Belongs to the `class` (not objects), can `be called directly` via the class name without creating an instance of the class (e.g., System.arraycopy() is called through the System class, `no need to use new System()`)
            - Stored in the method area, initialized when the class is loaded, and `globally unique`
        - Native
            - The method body is not written in Java, but implemented in low-level languages such as C/C++
    - used to copy arrays efficiently (`faster than manual for-loop`copying)
    - supporting partial or full element copying of arrays
```java
public class HelloWorld {
	public static void main(String[] args) {
        int a [] = new int[]{18,62,68,82,65,9};
        
        int b[] = new int[3];//分配了长度是3的空间，但是没有赋值
        
        //通过数组赋值把，a数组的前3位赋值到b数组
        
        //方法一： for循环
        
        for (int i = 0; i < b.length; i++) {
			b[i] = a[i];
		}
       
        //方法二: System.arraycopy(src, srcPos, dest, destPos, length)
        //src: 源数组
        //srcPos: 从源数组复制数据的起始位置
        //dest: 目标数组
        //destPos: 复制到目标数组的启始位置
        //length: 复制的长度        
        System.arraycopy(a, 0, b, 0, 3);
        
        //把内容打印出来
        for (int i = 0; i < b.length; i++) {
            System.out.print(b[i] + " ");
        }

    }
}
```
## 2 Dimensional Array
- initialization
    ```java
    public class HelloWorld {
        public static void main(String[] args) {
            //初始化二维数组
            int[][] a = new int[2][3]; //有两个一维数组，每个一维数组的长度是3
            a[1][2] = 5;  //可以直接访问一维数组，因为已经分配了空间
                
            //只分配了二维数组
            int[][] b = new int[2][]; //有两个一维数组，每个一维数组的长度暂未分配
            b[0]  =new int[3]; //必须事先分配长度，才可以访问
            b[0][2] = 5;
            
            //指定内容的同时，分配空间
            int[][] c = new int[][]{
                    {1,2,4},
                    {4,5},
                    {6,7,8,9}
            };
        }
    }
    ```
- get the length of rows/columns
    - `length of columns`: arrayName`[rowIndex]`.length 
        - e.g. a[i].length
    - `length of rows`: arrayName.length
        - e.g. a.length
## Exercise
> First, define a 5×8 2D array and then fill it with random numbers. Sort the 2D array with the help of methods from the Arrays class.

> Reference Approach:
> 1. First, copy the 2D array to a one-dimensional array using System.arraycopy;
> 2. Then sort the one-dimensional array with the sort method;
> 3. Finally, copy the sorted one-dimensional array back to the original 2D array.
```java
public class TwoDimensionalArray {
    public static void main(String[] args) {
        // create an 2D array a
        int[][] a = new int[5][8];
        for (int i = 0; i < a.length; i++){
            for (int j = 0; j < a[i].length; j++){
                a[i][j] = (int)(Math.random() * 100);
                System.out.printf("%3d", a[i][j]);
            }
            System.out.println();
        }
        // transfer 2D array a to 1D array b
        int[] b = new int[5*8];
        for (int i = 0; i < a.length; i++){
            System.arraycopy(a[i],0,b,i*8,a[i].length);
        }
        // print the 1D array b
        System.out.println(Arrays.toString(b));
        // sort the 1D array b
        Arrays.sort(b);
        // print the 1D array b after sort
        System.out.println(Arrays.toString(b));
        // transfer sorted b to original 2D array a
        for (int i = 0; i < 5; i++){
            System.arraycopy(b,i*8,a[i],0,8);
        }
        System.out.println(Arrays.deepToString(a));
    }
}
```
- takeaways
    - System.out.printf("%nd", )
        - a formatted output statement(`printf = print format`)
        - `does not wrap the line` automatically after printing
        - is `right-aligned by default`; use `negative sign` to make it `left-aligned`
        - `%`: The `starting marker` of the format specifier, telling the program that the subsequent characters are format rules
            - `n`: Specify the output width as `n characters`
            - `d`: Restrict the `output data type to integer` (decimal integer[byte/short/int/long])
            - `s`: Restrict the `output data type to String`
            - `t`: Restrict the `output data type to time`(Date/Calendar/LocalDateTime)
            - `b`: Restrict the `output data type to Boolean`
            - `%`: Restrict the `output % itself`("%%")
        - `Precision`: only valid for `floating-point` numbers/`strings`. %.2f retains 2 decimal places, and %.3s truncates to the first 3 characters.
        