# Java Basics - common utility class

## Scanner
- read data entered from the console
- ```import java.util.Scanner;```
- read Integer - ```nextInt()```
    ```java
    import java.util.Scanner;

    public class HelloInteger{
        public static void main(String[] args){
            Scanner s = new Scanner(System.in);
            int a = s.nextInt();
            System.out.println("the first number is: " + a);
            int b = s.nextInt();
            System.out.println("the second number is: " + b);
        }
    }
    ```
- read Floating-point - ```nextFloat()```
    ```java
    import java.util.Scanner;

    public class HelloFloat{
        public static void main(String[] args){
            Scanner s = new Scanner(System.in);
            float a = s.newFloat();
            System.out.println("the float is: " + a);
        }
    }
    ```
- read String - ```nextLine()```
    ```java
    import java.util.Scanner;

    public class HelloString{
        public static void main(String[] args){
            Scanner s = new Scanner(System.in);
            String a = s.nextLine();
            System.out.println("the String is: " + a);
        }
    }
    ```
- *read String after Integer*
    - need to **execute netLine() twice**
    - the first time is get the return-linefeed "\r\n"
    ```java
    import java.util.Scanner;

    public class IntegerString{
        public static void main(String[] args){
            Scanner s = new Scanner(System.in);
            int a = s.nextInt();
            System.out.println("the integer is: " + a);
            String b1 = s.nextLine();
            String b2 = s.nextLine();
            System.out.println("the string is: " + b2);
        }
    }
    ```

## `M`ath (must be uppercase)
- `no need to manually import any class`, because the Math class is in the java.lang package, which is automatically imported by JVM
- Basic Numeric Operations
    - `Math.abs(number)`: Calculates the absolute value (supports int/double/long)
    - `Math.max(a, b)`: Returns the maximum value of two numbers
    - `Math.min(a, b)`: Returns the minimum value of two numbers
- Rounding-Related Methods
    - `Math.round(number)`: Rounds to the nearest integer (double→long, float→int)
    - `Math.ceil(number)`: Rounds up (ceiling rounding, returns double)
    - `Math.floor(number)`: Rounds down (floor rounding, returns double)
- Random Number Generation
    - `Math.random()`: Generates a random double number in [0.0, 1.0`)`
    - **Generate random integer** in range (e.g., 1~100): `(int)(Math.random() * 100) + 1`
- Square Root/Exponent/Logarithm
    - `Math.sqrt(number)`: Calculates the positive square root (returns double)
    - `Math.cbrt(number)`: Calculates the cube root (returns double)
    - `Math.log10(number)`: Calculates logarithm with base 10
    - `Math.pow(double base, double exponent)`: Calculates the base^exponent (returns double)
- Common Constants
    - `Math.PI`: Pi (≈3.1415926)
        - a built-in `static final constant` in Java
        - an `immutable` **double-type** value

## Arrays
- `Arrays.copyOfRange(original_array, start_index (inclusive), end_index (exclusive))`
    - like `System.arraycopy()`
    - copies elements of an array in a specified range to generate a new array
    ```java
    int[] a = new int[]{23,45,2,5,63};
    int[] b = Arrays.copyOfRange(a,1,4); // b is [45,2,5]
    ```
- `Arrays.toString(array)`
    - prints a `one-dimensional array` quickly 
    - with the `format [element1, element2, ...]`
    ```java
    String content = Arrays.toString(b);
    System.out.pritln(content); // [45,2,5]
    ```
- `Arrays.deepToString(array)`
    - prints multi-dimensional arrays (2D/3D, etc.) 
    - with the output format `[[element1,element2], [element3,element4], ...]`
    ```java
    int[][] c = int[][]{
            {1,2,3},
            {4,5,6},
            {7,8,9}
        };
    String content = Arrays.deepToString(c)
    System.out.println(content); // [[1,2,3],[4,5,6],[7,8,9]]
    ```
- `Arrays.sort(array)`
    - sorts an array in `ascending order`
    - `modifies the original array` directly
    ```java
    // int[] a = new int[]{23,45,2,5,63};
    Arrays.sort(a);
    System.out.println(Arrays.toString(a));  // [2,5,23,45,63]
    ```
- `Arrays.binarySearch(sorted_array,target_element)`
    - performs binary search `on a sorted array` and `returns the index` of the target element
    - using it on unsorted arrays will return wrong results
    ```java
    // int[] a = new int[]{23,45,2,5,63};
    Arrays.sort(a); // a changes to [2,5,23,45,63]
    location = Arrays.binarySearch(a,45);
    System.out.println(location); // 3
    ```
- `Arrays.equals(arrayA,arrayB)`
    - compares two `one-dimensional` arrays
    - same `length` + all corresponding `elements` are equal
    ```java
    int a[] = new int[] { 18, 62, 68, 82, 65, 9 };
    int b[] = new int[] { 18, 62, 68, 82, 65, 8 };
 
    System.out.println(Arrays.equals(a, b)); // false
    ```
- `Arrays.deepEquals(arrayA,arrayB)`
    - compares `multi-dimensional` arrays (2D/3D, etc.) 
    ```java
    int a[][] = new int[][] {
            {1,2,6},
            {3,4,5}
        };

    int b[][] = new int[][] {
            {1,2,6},
            {3,4,5}
        };
    System.out.println(Arrays.equals(a,b)); // true
    ```
- `Arrays.fill(array,value)`
    - fills an array with `a specified value`
    - `modifies the original array` directly
    ```java
    int[] a = new int[10];
    Arrays.fill(a,5);
    System.out.println(Arrays.toString(a)); // [5,5,5,5,5,5,5,5,5,5]
    ```

## Date
- `java.util.Date;`
    - Time Origin
        - The time origin of the Date class in Java is January 1, 1970 00:00:00 GMT (Greenwich Mean Time), also known as "Unix Epoch Time"
        - The time of all Date objects is based on this origin, `expressed in milliseconds (ms)`: the origin is 0 ms, positive after the origin, negative before
    - Create Date Object
        - `new Date()`: Create a Date object representing the `current system time`
        - `new Date(long millis)`: Create a Date object for a specified time based on `"milliseconds since the time origin"`
        - the no-arg constructor of the Date class essentially calls `System.currentTimeMillis()` to get the current milliseconds
    ```java
    // 当前时间
            Date d1 = new Date();
            System.out.println("当前时间:");
            System.out.println(d1);
            System.out.println();
            // 从1970年1月1日 早上8点0分0秒 开始经历的毫秒数
            Date d2 = new Date(5000);
            System.out.println("从1970年1月1日 早上8点0分0秒 开始经历了5秒的时间");
            System.out.println(d2);
    ```
    - `getTime()`
        - Returns the number of milliseconds since the time origin (type long) 
        - `System.currentTimeMillis()`: Get current milliseconds directly (more efficient) without creating a Date instance
        ```java
        Date now= new Date();
        //打印当前时间
        System.out.println("当前时间:"+nowtoString());
        //getTime() 得到一个long型的整数
        //这个整数代表 1970.1.108:00:00:000，每经历一毫秒，增加1
        System.out.println("当前时间getTime()返回的值是："+now.getTime()); // 1773193351186
        System.currentTimeMillis(); // same results
        
        Date zero = new Date(0);
        System.out.println("用0作为构造方法，得到的日期是:"+zero); // Thu Jan 01 08:00:00 CST 1970
        ```
- `java.text.SimpleDateFormat;`
    - Date type convert to String type
        - `SimpleDateFormat()`
        - yyyy-MM-dd HH:mm:ss SSS (`H-24`;`h-12`)
        ```java
        import java.text.SimpleDateFormat;
        import java.util.Date;
        
        public class TestDate {
        
            public static void main(String[] args) {
                
                //y 代表年
                //M 代表月
                //d 代表日
                //H 代表24进制的小时
                //h 代表12进制的小时
                //m 代表分钟
                //s 代表秒
                //S 代表毫秒
                SimpleDateFormat sdf =new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SSS" );
                Date d= new Date();
                String str = sdf.format(d);
                System.out.println("当前时间通过 yyyy-MM-dd HH:mm:ss SSS 格式化后的输出: "+str);
                
                SimpleDateFormat sdf1 =new SimpleDateFormat("yyyy-MM-dd" );
                Date d1= new Date();
                String str1 = sdf1.format(d1);
                System.out.println("当前时间通过 yyyy-MM-dd 格式化后的输出: "+str1);
            }
        }
        ```
    - String type convert to Date type
        ```java
        import java.text.ParseException;
        import java.text.SimpleDateFormat;
        import java.util.Date;
        
        public class TestDate {
        
            public static void main(String[] args) {
                SimpleDateFormat sdf =new SimpleDateFormat("yyyy/MM/dd HH:mm:ss" );
        
                String str = "2026/1/5 12:12:12";
                
                try {
                    Date d = sdf.parse(str);
                    System.out.printf("字符串 %s 通过格式  yyyy/MM/dd HH:mm:ss %n转换为日期对象: %s",str,d.toString());
                } catch (ParseException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
                
            }
        }
        ```
  