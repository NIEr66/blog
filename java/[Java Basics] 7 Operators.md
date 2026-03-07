# Java Basics - 7 Operators

## 7 Operators
### Arithmetic Operators
- modulus(%)
    - calculates the `remainder` of the division of two integers
    - the sign is the same as the dividend
    ```java
    int i = 5;
    int j = 2;
    System.out.println(i%j); // output is 1
    ```
### Relational Operations
- bigger than >
- smaller than <
- equal to ==
- not euqal to !=
### Assignment Operators
- =
- +=
- -=
### Logical Operations
- logical not !
- Short-circuit And &&
    - if the left expression is false then `don't need` to execute the  `right one`
- Short-circuit Or ||
```java
public class HelloWorld {
    public static void main(String[] args) {
        //长路或
        int i = 2;
        System.out.println( i== 1 | i++ ==2  ); //无论如何i++都会被执行，所以i的值变成了3
        System.out.println(i);
         
        //短路或
        int j = 2;
        System.out.println( j== 2 || j++ ==2  );  //因为j==2返回true,所以右边的j++就没有执行了，所以j的值，还是2
        System.out.println(j);         
    }
}
```
### Bitwise Operators
- `Long-circuit` is specially for `logical condition judgment` while Short-circuit is for `handling binary values`
- Long-circuit Or |
    - First `convert to binary`, then `calculate bit by bit`
    - need to `execute both sides`
    - have one bit is 1 then 1
- Long-circuit And &
    - need to `execute both sides`
    - First `convert to binary`, then `calculate bit by bit`
    - only if both bits are 1 then 1
- Exclusive OR / XOR  (^)
    - two binary bits are the `same`, the result is `0`
    - two binary bits are the `different`, the result is `1`
- Bitwise NOT ~
    - flip binary bits (0↔1), `complete inversion`
    ```java
    public class HelloWorld {
	public static void main(String[] args) {
		byte i  =5;
		
		System.out.println(Integer.toBinaryString(i)); //5的二进制是00000101,所以取非即为11111010,即为-6
		
		System.out.println(~i);
		}
	    }
    ```
- Right Shift >>
    - shift each of its bits to the right
    - signed right shift >>
        - will preserve the sign
        - for `positive` numbers, shifts all bits to the right and `pads 0 to the leading position`
        - for `negative` numbers, shifts all bits to the right and `pads 1 to the leading position`
    - unsigned right shift >>>
        - results in the `first bit becoming 0` after shifting
        - causes a negative number to `become a positive number` after unsigned right shift
- Left Shift <<
    - shift each of its bits to the left, and **fill the rightmost bit with 0**
    - General rule for `shifting left by n bits`: `Result = Original number × Baseⁿ`
    ```java
    // how to calculate 2*16 without using multiple sign
    public class ScannerPractise {
        public static void main(String[] args) {
            int a = 2;
            // the binary string of a
            System.out.println(Integer.toBinaryString(a));
            System.out.println(a<<4);
        }
    }
    ```
```java
public class HelloWorld {
	public static void main(String[] args) {
		byte i  =6;
		
		//6的二进制是110
		System.out.println(Integer.toBinaryString(i)); 
		//6向左移1位后，变成1100，对应的10进制是12
		System.out.println(i<<1);
		//6向右移1位后，变成11，对应的10进制是3
		System.out.println(i>>1);
	}	
}
```
```java
int i = 1;
boolean b = !(i++ == 3) ^ (i++ == 2) && (i++ == 3);
System.out.println(b);
System.out.println(i);
/**
i == 3 false
!(i++ == 3)               true     i=2
i == 2                    true
(i++ ==2)                 true     i=3
!(i++ == 3) ^ (i++ ==2)   false

short-circuit and && only execute the left side when the result of left side is false
so the output is:
false
3
**/
```
### Ternary Operator (Conditional Operator)
- `expression ? value1 : value2`
- if expression is `ture` then return `value1`
- if expression is `false` then return `value2`
```java
public class Exercise{
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        System.out.println("今天是周几?");
        int i = s.nextInt();
        String day = (1 <= i && i <= 5) ? "今天是工作日" : "今天是周末";
        System.out.println(day);

        /**相当于
        if (1 <= i && i <= 5){
            day = "今天是工作日";
        } else{
            day = "今天是周末";
        }
         */
    }
}
```
### Others
- increment(++)
    - value first, then calculation
        ```java
        int i = 5;
        System.out.println(i++); //output is 5
        System.out.println(i); //output is 6
        ```
    - calculation first, then value
        ```java
        int i = 5;
        System.out.println(++j); //output is 6
        System.out.println(j); //output is 6
        ```
- decrement(--)
- instanceof
    - check whether the `object on the left` is an **`instance`** of the `class/interface on the right`
    - return a `boolean` value (true/flase)
    ```java
    String str = "Hello";
    boolean d = str instanceof String; // true
    ```