# Java Basics - common utility class

## common utility class
### Scanner
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
### `M`ath (must be uppercase)
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