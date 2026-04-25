# Java Basics - Numbers and Strings

## Boxing & Unboxing
- Wrapper classes `convert primitive` types into `object` types
    |Primitive|Wrapper|
    |--|--|
    |byte|Byte|
    |short|Short|
    |int|Integer|
    |long|Long|
    |float|Float|
    |double|Double|
    |char|Character|
    |boolean|Boolean|
- Boxing & Unboxing
    - Boxing: primative -> wrapper
    - Unboxing: wrapper -> primative
    ```java
    public class TestNumber {

        public static void main(String[] args) {
            int i = 5;
            
            //把一个基本类型的变量,转换为Integer对象 
            Integer it = new Integer(i);
            //把一个Integer对象，转换为一个基本类型的int
            int i2 = it.intValue(); 
        }
    }
    ```
    - automatic unboxing
        - use "="
    - automatic boxing
        - Automatic conversion is not allowed `between different` primitive types and wrapper classes
    ```java
    public class TestNumber {
 
        public static void main(String[] args) {
            int i = 5;
    
            //基本类型转换成封装类型
            Integer it = new Integer(i);
            //自动转换就叫装箱
            Integer it2 = i;

            //封装类型转换成基本类型
            int i3 = it.intValue();
            //自动转换就叫拆箱
            int i4 = it;
        }
    }
    ```
- class `Number`
    - `All numeric wrapper classes inherit from Number`, and automatic down-unboxing is `not supported`
    ```java
    public class TestNumber {
 
        public static void main(String[] args) {
            int i = 5;
            
            Integer it = new Integer(i);
            //Integer是Number的子类，所以打印true
            System.out.println(it instanceof Number);
        }
    }
    ```
- max and min
    - Integer.MAX_VALUE
    - Integer.MIN_VALUE
    - Byte.MAX_VALUE
    - Byte.MIN_VALUE
    - ……

## Type Conversion
- Digital type convert to String type (2 methods)
    - `String.valueOf()`
    ```java
    int i = 5;
    String str = String.valueOf(i);
    ```
    - convert to wrapper class first, then use `toString()` of object
    ```java
    int i =5;
    Integer it = i;
    String str = it.toString();
    ```
- String type convert to Digital type
    - `Integer.parseInt()`
    ```java
    String str = "999";
    int i = Integer.parseInt(str);
    ```


## Formatted output
- `printf = format`
- `%d`: int
- `%f`: double/float
- `%s`: String
- `%n`: new line
```java
String sentenceFormat = "%s 进行了连续 %d 次攻击后，获得了 %s 的称号 %n"
System.out.printf(sentenceFormat,name,number,title);
// smae
System.out.format(sentenceFormat,name,number,title);
```
```java
import java.util.Locale;
   
public class TestNumber {
   
    public static void main(String[] args) {
        int year = 2020;
        //总长度，左对齐，补0，千位分隔符，小数点位数，本地化表达
          
        //直接打印数字
        System.out.format("%d%n",year);
        //总长度是8,默认右对齐
        System.out.format("%8d%n",year);
        //总长度是8,左对齐
        System.out.format("%-8d%n",year);
        //总长度是8,不够补0
        System.out.format("%08d%n",year);
        //千位分隔符
        System.out.format("%,8d%n",year*10000);
  
        //小数点位数
        System.out.format("%.2f%n",Math.PI);
          
        //不同国家的千位分隔符
        System.out.format(Locale.FRANCE,"%,.2f%n",Math.PI*10000);
        System.out.format(Locale.US,"%,.2f%n",Math.PI*10000);
        System.out.format(Locale.UK,"%,.2f%n",Math.PI*10000);    
    }
}
```

## Character
- the wrapper class of char is Character
- common methods of Charactor
    ```java
    public class TestChar {
    
        public static void main(String[] args) {
            
            System.out.println(Character.isLetter('a'));//判断是否为字母
            System.out.println(Character.isDigit('a')); //判断是否为数字
            System.out.println(Character.isWhitespace(' ')); //是否是空白
            System.out.println(Character.isUpperCase('a')); //是否是大写
            System.out.println(Character.isLowerCase('a')); //是否是小写
            
            System.out.println(Character.toUpperCase('a')); //转换为大写
            System.out.println(Character.toLowerCase('A')); //转换为小写
    
            String a = 'a'; //不能够直接把一个字符转换成字符串
            String a2 = Character.toString('a'); //转换为字符串    
        }
    }
    ```
- common Escape

| 转义符 | 中文含义 | English |
|--------|----------|---------|
| `\n` | 换行 | New line |
| `\t` | 水平制表符（空格缩进）| Horizontal tab |
| `\r` | 回车 | Carriage return |
| `\\` | 反斜杠本身 | Backslash |
| `\"` | 双引号 | Double quote |
| `\'` | 单引号 | Single quote |
| `\b` | 退格 | Backspace |
| `\f` | 换页符 | Form feed |
```java
public class TestChar {
  
    public static void main(String[] args) {
        System.out.println("使用空格无法达到对齐的效果");
        System.out.println("abc def");
        System.out.println("ab def");
        System.out.println("a def");
          
        System.out.println("使用\\t制表符可以达到对齐的效果");
        System.out.println("abc\tdef");
        System.out.println("ab\tdef");
        System.out.println("a\tdef");
         
        System.out.println("一个\\t制表符长度是8");
        System.out.println("12345678def");
          
        System.out.println("换行符 \\n");
        System.out.println("abc\ndef");
 
        System.out.println("单引号 \\'");
        System.out.println("abc\'def");
        System.out.println("双引号 \\\"");
        System.out.println("abc\"def");
        System.out.println("反斜杠本身 \\");
        System.out.println("abc\\def");
    }
}
```


## String
- 3 ways of create a string
    - Create string by `direct assignment`
    - Create string with `new` constructor
    ```java
    String s1 = "java";  // 只创建 1 个（常量池）
    String s2 = "java";  // 不创建，复用
    String s3 = new String("java"); // 创建 2 个！
    ```
    - Use `+` to concat Strings will also create new String object
- String is 
    - `immutable`, cannot be changed
    - `final`, cannot be inherited
- use `.length()` to get the length of the String object
- characters and numbers(short,int,long,……) `can be converted` to each other (ASCII)
- methods of manipulating Character
    - charAt(): get Char
        ```java
        String sentence = "盖伦,在进行了连续8次击杀后,获得了 超神 的称号";
         
        char c = sentence.charAt(0); //盖
        ```
    - toCharArray(): get corresponding char array
        ```java
        String sentence = "盖伦,在进行了连续8次击杀后,获得了超神 的称号";
 
        char[] cs = sentence.toCharArray(); //获取对应的字符数组
         
        System.out.println(sentence.length() == cs.length); // true
        ```
    - subString(): take a substring
        ```java
        String sentence = "盖伦,在进行了连续8次击杀后,获得了 超神 的称号";
         
        //截取从第3个开始的字符串 （基0）
        String subString1 = sentence.substring(3);
         
        System.out.println(subString1);
         
        //截取从第3个开始的字符串 （基0）
        //到5-1的位置的字符串
        //左闭右开
        String subString2 = sentence.substring(3,5);
        ```
    - split()
        ```java
        String sentence = "盖伦,在进行了连续8次击杀后,获得了 超神 的称号";
         
        //根据,进行分割，得到3个子字符串
        String subSentences[] = sentence.split(",");
        ```
    - trim(): take off the write space of head and tail
    - toUpperCase()/toLowerCase()
        ```java
        // capitalize the first letter of each word
        String sentence = "let there be light";
        String[] str = sentence.split(" ");
        System.out.println(Arrays.toString(str));

        for(int i=0;i<str.length;i++){
            str[i] = str[i].substring(0,1).toUpperCase() + str[i].substring(1);
            System.out.print(str[i] + " ");
        } // Let There Be Light
        ```
    - indexOf()
    - lastIndexOf()
    - contains()
        ```java
        String sentence = "盖伦,在进行了连续8次击杀后,获得了超神 的称号";
  
        System.out.println(sentence.indexOf('8')); //字符第一次出现的位置
          
        System.out.println(sentence.indexOf("超神")); //字符串第一次出现的位置
          
        System.out.println(sentence.lastIndexOf("了")); //字符串最后出现的位置
          
        System.out.println(sentence.indexOf(',',5)); //从位置5开始，出现的第一次,的位置
          
        System.out.println(sentence.contains("击杀")); //是否包含字符串"击杀"
        ```
    - replaceAll()
    - replaceFirst(): only replace the first one
    - equals()
    - equalsIgnoreCase(): ignore the difference of  lowercase and uppercase
    - startWith(): judge whether a string starts with a substring
    - endsWith()


## StringBuffer
- a `mutable` character sequence, can modify string content directly without creating new objects
- The `underlying structure` of String is a `final char array`, so its length is fixed and cannot be changed
- StringBuffer uses a `non-final char array` and a variable count to store the actual length
- methods
    - append()
    - delete()
    - insert()
    - reverse()
    ```java
    public class TestString {
    
        public static void main(String[] args) {
            String str1 = "let there ";
    
            StringBuffer sb = new StringBuffer(str1); //根据str1创建一个StringBuffer对象
            sb.append("be light"); //在最后追加
            
            System.out.println(sb);
            
            sb.delete(4, 10);//删除4-10之间的字符 ( start (inclusive) to end (exclusive))
            
            System.out.println(sb);
            
            sb.insert(4, "there ");//在4这个位置插入 there
            
            System.out.println(sb);
            
            sb.reverse(); //反转
            
            System.out.println(sb);
        }
    }
    ```

