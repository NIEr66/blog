# Java Basics

## JDK & JRE & JVM
### JDK(Java Development Kit) 
- a **toolset** for developing Java programs
- including core **tools and environment** for write, compile and run Java code
    - **compile** is the process of coverting *human-readable* source code(e.g. Java) into *computer-executable* instructions

### JRE(Java Runtime Environment)
- provides a *space* for *written Java programs* to **run**

### JVM(Java Virtual Machine)
- core of JRE
- *translates* the Java code to **enable programs run on different systems**(macOS/Windows/Linux/...)

### `JDK includes JRE & JRE includes JVM`

### Steps for JDK Installation & Environment Variable Configuration on *Windows*
1. download JDK on [Oracle's official website](https://www.oracle.com/cn/java/technologies/downloads/)
2. install JDK and remember the path
3. configure environment variables
    - step1: "此电脑" -> "属性" -> "编辑系统环境变量" -> "系统环境变量"
    - step2: add the **JAVA_HOME** variable in "系统变量" (enter the JDK path)
    - step3: add **%JAVA_HOME%\bin** and **%JAVA_HOME%\jre\bin** in "用户变量/Path"
4. open cmd and type in "java -version" to test whether the configuration is successful


## 8 basic variable types
- **4 Integer type**
    - byte(can only store *8* bits)
    - short(can only store *16 bits/2 bytes*)
    - int(can only store *32 bits/4 bytes*)
    - long(can only store *64 bits/8 bytes*)
        - **bit** is the ```smallest storage unit``` of computer
        - 1 bit can only store 0 or 1
        - 1 Byte = 8 bits(8 consecutive binary bits)
- **1 Character type**
    - use ```single quotation marks ''```
    - can only store ```1 character```
- **2 Floating-point type**
    - float(32 bits)
        - needs to add the suffix **f/F**
    - double(64 bits)
        - default type
        - scientific notation
            - e.g. 3.14 * 10^2 = 3.14e2
            - e.g. 5 * 10^(-3) = 5e-3
- **1 Boolean type**
    - true(1)
    - false(0)
    - ```cannot use 0 1 for assignment```
- other about variable 
    - String type (*not belongs to the 8 basic types*)
        - ```cannot be changed``` once created
        - use ```double quotation marks ""```
    - data type conversion
        ![data type conversion](..\image\dataTypeConversion.png)
        - low-percision type likes a smaller glass
        - high-percision type likes a larger glass which can contain more data
        - high-percision type convert to low-percision type may result ```overflow``` (```explicit casting``` is required)
        - ```java
            public class HelloWorld {

            public static void main(String[] args) {

                char c = 'A';
                short s = 80;
                
                //虽然short和char都是16位的，长度是一样的
                //但是彼此之间，依然需要进行强制转换
                c = (char) s;
                //直接进行转换，会出现编译错误
                s = c;
                }
            }
            ```
    - **Scope**
        - refers to the code range where a variable/field can be accessed
        - Fields(member variables)
            - defined inside a class but outside methods
            - with the scope of ```entire class```
        - Parameters(method parameters)
            - defined in the method's parameter list
            - with the scope of the ```current class interior```
            - destroyed after the method is executed
        - Local variables
            - defined inside methods or code blocks
            - with the scope of the ```current code block interior```
        - ```Priority (when names are the same): Local variables > Parameters > Fields```
        - ```java
            public class HelloWorld {
                
                int i = 1; // this i is a Filed

                public void method1(int i){ //this i is a method parameter
                    System.out.println(i);
                }
                
                public static void main(String[] args) {
                    new HelloWorld().method1(5);
                    //the result is 5
                }
            }
            ```
    - final
        - when a variable modified by *final*, it can only ```be assigned a value once (cannot be changed``` after assignment)
        - declaration(there's a variable named XX with type of YY) & assignment(set a specific value) 
        - ```java
            public class HelloWorld {

                // 定义method1方法，参数j被final修饰
                public void method1(final int j) {
                    // 注意：下面这行代码如果解开注释，编译会报错（final基本类型参数不可重新赋值）
                    // j = 5; 
                    System.out.println("method1方法接收到的参数值是：" + j);
                }

                // 程序入口main方法（说明在哪里开始运行）
                public static void main(String[] args) {
                    // 1. 创建HelloWorld类的对象，同时调用method1方法，传入实参8
                    new HelloWorld().method1(8);
                    // Java调用带参数的方法必须显式传参
                    // 调用Scanner通过控制台输入参数的形式也是显式传参
                    
                    // 2. 也可以拆分成两步写
                    // HelloWorld hello = new HelloWorld(); // 创建对象
                    // hello.method1(8); // 调用方法并传参
                }
            }
          ```

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

## Operators
### Arithmetic Operators
- modulus(%)
    ```java
    int i = 5;
    int j = 2;
    System.out.println(i%j); // output is 1
    ```
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

### Logical Operations
- Long-circuit And &
    - need to ```execute both sides```
- Short-circuit And &&
    - if the left expression is false then ```don't need``` to execute the  ```right one```
- Long-circuit Or |
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
- ```Long-circuit``` is specially for ```logical condition judgment``` while Short-circuit is for handling binary values
- Exclusive OR
    - two binary bits are the ```same```, the result is ```0```
    - two binary bits are the ```different```, the result is ```1```
```java
int i = 1;
boolean b = !(i++ == 3) ^ (i++ ==2) && (++==3);
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

### Ternary Operator
- ```expression ? value1 : value2```
- if expression is ```ture``` then return ```value1```
- if expression is ```false``` then return ```value2```
```java
class exercise{
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        System.out.println("今天是周几?");
        int i = s.nextInt();
        String day = (1 <= i & i <= 5) ? "今天是工作日" : "今天是周末";
        System.out.println(day);

        /**相当于
        if (1 <= i & i <= 5){
            day = "今天是工作日";
        } else{
            day = "今天是周末";
        }
         */
    }
}
```

## Syntax
### muti-condition branch judgment
- if else
    ```java
        if(condition1){
            // todo
        } else{
            //todo
        }
    ```
- else if
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
- switch
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
- while
    - will continuously execute if only the expression is true
    ```java
    // print 1 to 4
    public class while_doWhile {
    public static void main(String[] args) {
        int i = 0;
        while(i < 5){
            System.out.println(i);
            i++;
            }
        }
    }
    ```
- do-while
    - execute first then determine whether the conditions are met(if meet then execute)

