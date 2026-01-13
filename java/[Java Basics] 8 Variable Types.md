# Java Basics - 8 variable types

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