# Java Basics

## JDK & JRE & JVM
### JDK(Java Development Kit) 
- a **toolset** for developing Java programs
- including core **tools and environment** for write, compile and run Java code
    - **compile** is the process of coverting *human-readable* source code(e.g. Java) into *computer-executable* instructions

### JRE(Java Runtime Environment)
- provides a *space* for **writting and running** Java programs

### JVM(Java Virtual Machine)
- core of JRE
- *translates* the Java code to **enable programs run on different systems**(macOS/Windows/Linux/...)

### `JDK includes JRE & JRE includes JVM`

### Steps for JDK Installation & Environment Variable Configuration on *Windows*
1. download JDK on [Oracle's official website](https://www.oracle.com/cn/java/technologies/downloads/)
2. install JDK and remember the path
3. configure environment variables
    - step1: "此电脑" -> "属性" -> "编辑系统环境变量" -> "系统环境变量"
    - step2: add the **JAVA_HOME\bin** variable in "系统变量" (enter the JDK path)
    - step3: add **%JAVA_HOME** and **%JAVA_HOME%\jre\bin** in "用户变量/Path"
4. open cmd and type in "java -version" to test whether the configuration is successful


##