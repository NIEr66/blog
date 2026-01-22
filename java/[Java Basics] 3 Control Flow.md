# Java Basics - 3 Control Flow

## 3 Control Flow
### Sequential Structure
- no specific syntax keywords
- the default execution logic of Java programs
### Branching Structure
- `if else`
    ```java
        if(condition1){
            // todo
        } else{
            //todo
        }
    ```
- `else if`
    - the code block of **the first satisfied condition is executed**
    - the **remaining branches are no longer judged**
    ```java
    if(condition1){
        // todo
    }
    else if(condition2){
        // todo
    }
    else if(condition3){
        // todo
    }
    ```
- `switch`
    - should use **break** after each expression finished
    ```java
    switch(expression){
        case constantValue1:  // excute when "expression == constantValue1"
            executeCode1;
            break;
        case constantValue2:
            executeCode2;
            break;
        default:
            defaultExecuteCode;
            break;
    }
    ```
    ```java
    import java.util.Scanner;

    public class Season {
        public static void main(String[] args) {
            Scanner s = new Scanner(System.in);
            System.out.println("please type in month:");
            int month = s.nextInt();
            switch (month){
                case 12:
                case 1:
                case 2:     // when many cases need to execute the same code, can "case fall-through"(case贯穿) [donnot need to use "break;"]
                    System.out.println("spring");
                    break;
                case 3:
                case 4:
                case 5:
                    System.out.println("summer");
                    break;
                case 6:
                case 7:
                case 8:
                    System.out.println("autumn");
                    break;
                case 9:
                case 10:
                case 11:
                    System.out.println("winter");
                    break;
            }
            s.close(); // releases resources occupied by Scanner
        }
    }
    ```
### Loop Structure
- 3 Core control statement
    - `while`
        - will continuously execute if only the expression is true
        ```java
        // print 0 to 4
        public class WhileDo {
        public static void main(String[] args) {
            int i = 0;
            while(i < 5){
                System.out.println(i);
                i++;
                }
            }
        }
        ```
    - `do-while`
        - execute first then determine whether the conditions are met(if meet then execute)
        ```java
        public class DoWhile {
        public static void main(String[] args) {
                // print 0 to 4
                int i = 0;
                do{
                    System.out.println(i);
                    i++;           
                } while(i<5);
            }
        }
        ```
    - `for`
        - as same as while()
        ```java
        /** 
        for (initialization expression; loop condition expression; update expression) {
        // Loop body: code executed when the condition is true
        } **/
        // print 0 to 4
        public class for1{
            public static void main(String[] args) {
                for(int i = 0; i < 5; i++){
                    System.out.println(i);
                }
            }
        }
        ```
- 2 Auxiliary control statement
    - `continue`
        - **skips** the following code block
        - directly **turn to the next iteration of the loop**
        - `without terminating the entire loop`
        ```java
        // print the odd
        public class Odd {
            public static void main(String[] args) {
                for(int i = 0; i < 10; i++){
                    if(0 == i % 2){continue;}
                    System.out.println(i);
                }
            }
        }
        ```
    - `break`
        - **terminates** the entire loop
        - can only terminates the `current loop` 
        - if want to terminate `outside's loop`
            - use `while and boolean`
                ```java
                public class HelloWorld {
                    public static void main(String[] args) {
                        boolean breakout = false; //是否终止外部循环的标记
                        for (int i = 0; i < 10; i++) {
                            for (int j = 0; j < 10; j++) {
                                System.out.println(i + ":" + j);
                                if (0 != j % 2) {
                                    breakout = true; //终止外部循环的标记设置为true
                                    break;
                                }
                            }
                            if (breakout) //判断是否终止外部循环
                                break;
                        }
                    }
                }
                // 0:0
                // 0:1
                ```
            - use `label`
                ```java
                public class HelloWorld {
                    public static void main(String[] args) {
                        outloop: //outloop这个标示是可以自定义的比如outloop1,ol2,out5
                        for (int i = 0; i < 10; i++) {
                            for (int j = 0; j < 10; j++) {
                                System.out.println(i + ":" + j);
                                if (0 == j % 2) {
                                    break outloop;
                                }
                            }
                        }
                    }
                }
                ```
        ```java
        /**
        假设你月收入是3000，除开平时花销，每个月留下1000块钱进行投资。
        然后你认真的钻研了 《股票和基金 21天从入门到精通》，达到了每年20%的投资回报率。
        那么问题来了，以每个月投资1000块钱的节奏，持续投资多少年，总收入达到100万
        （复利计算按照每年12000投入计算，不按照每月计息）
        */

        public class Millionaire{
            public static void main(String[] args) {
                int p = 12000;
                double r = 0.2;
                double totalF = 1000000;
                double totalNow = 0;
                for (int n = 1; n < 100; n++){
                    totalNow += p*Math.pow(1+r,n);
                    if (totalF >= totalNow) {
                        continue;
                    }
                    System.out.println("Year " + n + " income is " + totalNow + ", which is more than one million.");
                    break;
                }
            }
        }

        // or use while which is more flexible

        While(True){
            n++;
            totalNow += p*Math.pow(1+r,n);

            if (totalF <= totalNow) {
                System.out.println("Year " + n + " income is " + totalNow + ", which is more than one million.");
                break;
            }
        }
        ```
## Exercise
### Golden Ratio
> Find two numbers whose quotient is closest to the golden ratio of 0.618.
> Requirements:  
> - The numerator and denominator cannot both be even numbers.
> - Both the numerator and denominator must be in the range [1-20].
```java
class ControlFlowPractice1 {
    public static void main(String[] args) {
        double result;
        double distance;
        double currentClosest = 400;
        int currentI = 0;
        int currentJ = 0;
        double point = 0.618;
        for (int i = 1; i <= 20; i++) {
            for (int j = 1; j <= 20; j++) {
                if (i % 2 == 0 && j % 2 == 0) {
                    continue;
                }
                // two integer's quotient must be integer
                // so, need a type conversion here
                result = (double) i / j;
                distance = Math.abs(point - result);
                if (currentClosest > distance) {
                    currentClosest = distance;
                    currentI = i;
                    currentJ = j;
                }
            }
        }
        System.out.println(currentI);
        System.out.println(currentJ);
    }
}
```
### Narcissistic Number (3-digit)
> Definition of 3-digit Narcissistic Number
> - It must be a 3-digit number (ranging from 100 to 999).
> - The sum of the cubes of its individual digits is exactly equal to the number itself. For example, 153 = 1³ + 5³ + 3³ (or 1×1×1 + 5×5×5 + 3×3×3).

> Find all 3-digit narcissistic numbers.
```java
class ControlFlowPractice2 {
    public static void main(String[] args) {
        int units;
        int tens;
        int hundreds;
        for (int i = 100; i < 1000; i++){
            hundreds = i / 100;
            tens = (i - hundreds * 100) / 10;
            units = i - hundreds * 100 - tens * 10;
            if (i == Math.pow(hundreds, 3) + Math.pow(tens, 3) + Math.pow(units, 3)){
                System.out.println(i);
            }
        }
    }
}
```
