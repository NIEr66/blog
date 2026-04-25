## Java Intermediates —— Exception
## definition
- an abnormal condition that occurs during program runtime, which disrupts the normal execution flow of a program
- 3 types of exceptions
    - 2 `Unchecked Exception`
        - `not compulsory to use` try-catch, while can also use try-catch to handle
        - `Error`
            - serious `system-level problems` that cannot be handled by application code
            - `thrown by the JVM`, usually indicating a failure of the virtual machine itself or resource exhaustion
        - `RuntimeException`
            - not checked at compile time. They can be left unhandled in code and are thrown only at runtime, usually caused by logical errors in the program
    - 1 `Checked Exception`
        - checked `at compile time`
        - `must be explicitly handled`, otherwise the code will not compile
            - either caught with `try-catch`
            - or declared to be thrown with `throws`


## Deal with Exeption
- try-catch
    - is used to catch and handle exceptions, preventing the program from crashing
    - execution process
        - Run code in try block first
        - If no exception, catch will not run
        - If exception occurs, jump to catch and handle it
    ```java 
    import java.io.File;
    import java.io.FileInputStream;
    import java.io.FileNotFoundException;
    
    public class TestException {
    
        public static void main(String[] args) {
            
            File f= new File("d:/LOL.exe");
            
            try{
                System.out.println("试图打开 d:/LOL.exe");
                new FileInputStream(f);
                System.out.println("成功打开");
            }
            catch(FileNotFoundException e){
                System.out.println("d:/LOL.exe不存在");
                e.printStackTrace();
            } 
            /**
             * can also use the parent class of FileNotFoundException
             * catch(Exception e){
                System.out.println("d:/LOL.exe不存在");
                e.printStackTrace();
            }
             */
        }
    }
    ```
    - 2 methods to capture various exceptions
        - `Multiple catch blocks` 
            ```java
            catch (FileNotFoundException e) {
                System.out.println("d:/LOL.exe不存在");
                e.printStackTrace();
            } catch (ParseException e) {
                System.out.println("日期格式解析错误");
                e.printStackTrace();
            }
            ```
        - if conditions in one catch block
            ```java
            catch (FileNotFoundException | ParseException e) {
                if (e instanceof FileNotFoundException)
                    System.out.println("d:/LOL.exe不存在");
                if (e instanceof ParseException)
                    System.out.println("日期格式解析错误");
    
                e.printStackTrace();
            }
            ```
- try-catch-finally
    - whether there's an error, the finally block will be excuted
    ```java
    try{
        System.out.println("试图打开 d:/LOL.exe");
        new FileInputStream(f);
        System.out.println("成功打开");
    }
    catch(FileNotFoundException e){
        System.out.println("d:/LOL.exe不存在");
        e.printStackTrace();
    }
    finally{
        System.out.println("无论文件是否存在，都会执行的代码");
    }
    ```
    - If the finally block also contains a return statement, it `will override the value temporarily` stored in try/catch, causing the method to ultimately return the value from the finally block instead
    ```java
    public class TestFinallyReturn {
        public static int method() {
            try {
                return 1;
            } catch (Exception e) {
                return 2;
            } finally {
                return 3;
            }
        }

        public static void main(String[] args) {
            System.out.println(method()); // 输出：3
        }
    }
    ```
- throws
    - Declare `potential exceptions` and `hand them to the caller`
    - declare throws in the `statement of method`
        - private static void method2() `throws FileNotFoundException`{}
    ```java
    public class TestException {
    
        public static void main(String[] args) {
            method1(); // main method calls method1
        }
    
        private static void method1() {
            try {
                method2(); // method1 calls method2
            } catch (FileNotFoundException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
                // 把异常发生的位置、原因、调用路径完整打印在控制台
            }
        }
    
        // pass method2's potential error to method1
        private static void method2() throws FileNotFoundException {
    
            File f = new File("d:/LOL.exe");
    
            System.out.println("试图打开 d:/LOL.exe");
            new FileInputStream(f);
            System.out.println("成功打开");
        }
    }
    ```
- throw
    - Manually throw an exception in code (inside the method body)
    - when execute throw, there must have some errors, unlike throws which is a potential


## Throwable
- the `superclass of all objects` that can be thrown via the throw statement and caught via the catch statement in Java
- Both Exception and Error are `direct subclasses` of Throwable
    ```java
    java.lang.Object
        └─ java.lang.Throwable
            ├─ java.lang.Error                      // ← 【Unchecked Exception 非可查异常】
            │  └─ OutOfMemoryError, StackOverflowError...
            └─ java.lang.Exception
                ├─                                  // ← 【Checked Exception 可查异常】
                │  └─ IOException, SQLException...
                └─ java.lang.RuntimeException       // ← 【Unchecked Exception 非可查异常】
                    └─ NullPointerException...
    ```


## Custom Exception
- `defined by developers` to represent business-specific errors, such as wrong password, insufficient balance or account exceptions