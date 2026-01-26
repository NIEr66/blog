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
