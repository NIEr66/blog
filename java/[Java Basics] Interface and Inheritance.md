# Java Basics - Interface and Inheritance

## Interface
- a `specification of behaviours`
- only declares methods `without implementation`
- a class can implement multiple interfaces
    - Implementing an interface means `keeping a certain promise`
    - Therefore, implementing an interface requires you to provide the `method declared` in the class (@Override)
    ```java
    package charactor;
 
    public interface AD {
        //物理伤害
        // 不能写方法体！！！
        public void physicAttack();

    }


    package charactor;
 
    public class ADHero extends Hero implements AD{
    
        @Override
        public void physicAttack() {
            System.out.println("进行物理攻击");
        }
    }
    ```

## Object type conversion
- **Reference type** is the variable type that `stores object address` (**Reference type = name card**)
- **Object type** is the real type of the `instance` itself (**Object type = real identity**)
- Generally, the reference type is the same as the object type.**Type conversion** refers to conversion when the `reference type differs from the actual object type`
    ```java
    Animal a = new Cat();
    // Animal is the reference type
    // Cat is the object type
    ```
- 5 types of Type Conversion
    - **Skill: Check if the right type can be used as the left type**
    - `Subclass to parent class (Upcasting)`
        - `Automatically convert` subclass objects to parent references. Safe and `no mandatory cast`
        ```java
        Hero h = new Hero();
        ADHero ad = new ADHero();
        h = ad; // right type can be used as the left type
        ```
    - Parent class to subclass (Downcasting)
        - Convert parent references back to subclass. `Mandatory cast required`
        - Sometimes may work, sometimes may not. Easy to throw `type exceptions`
        ```java
        // work
        Hero h = new Hero();
        ADHero ad = new ADHero();
        // The reference type of h is parent class Hero
        // The actual object type of h is subclass ADHero
        h = ad;
        ad = (ADHero) h;

        // throw type exceptions
        Hero h = new Hero();
        ADHero ad = new ADHero();
        Support s = new Support();
        // right type can be used as left type
        // object type of h is Support
        // reference typr of h is Hero
        h = s;
        // Support cannot convert to ADHero
        ad = (ADHero)h;
        ```
    - Conversion between two unrelated classes
        - Absolutely forbidden
    - Implementation class to interface (Upcasting)
        - `Automatically convert` implementation objects to interface references, same rule as parent-child upcasting
        - because the class definitely has the methods that the interface required
    - Interface to implementation class (Downcasting)
        - `Mandatory cast` with type safety risks
- instanceof
    - Checks if the actual object belongs to a type, returns true or false
    ```java
    //判断引用h1指向的对象，是否是ADHero类型
    System.out.println(h1 instanceof ADHero);
     
    //判断引用h2指向的对象，是否是APHero类型
    System.out.println(h2 instanceof APHero);
     
    //判断引用h1指向的对象，是否是Hero的子类型
    System.out.println(h1 instanceof Hero);
    ```

## Polymorphism
- the `same behavior acts differently` on different objects
- Operator polymorphism
    - The + operator can `do arithmetic calculation`, or `connect strings`
- Class polymorphism (2 requirements)
    - parent references(interfaces) pointing to subclass objects
    - The called method has been overridden
    ```java
    // 父类
    class Hero {
        public void attack() {
            System.out.println("英雄攻击");
        }
    }

    // 子类1
    class ADHero extends Hero {
        @Override // 重写
        public void attack() {
            System.out.println("AD英雄平A！");
        }
    }

    // 子类2
    class APHero extends Hero {
        @Override // 重写
        public void attack() {
            System.out.println("AP英雄放技能！");
        }
    }

    public class Test {
        public static void main(String[] args) {
            // 向上转型：父类引用指向子类对象
            Hero h1 = new ADHero(); 
            Hero h2 = new APHero();

            h1.attack(); // 输出：AD英雄平A！（运行的是ADHero的方法）
            h2.attack(); // 输出：AP英雄放技能！（运行的是APHero的方法）
        }
    }
    ```
- benifits for polymorphism
    - Code reuse and reduce redundant code
    - Decouple classes, parents control rules, children implement freely
        > What is decoupling
        > Reduce dependencies between classes. Modifying one class won’t affect others, improving maintainability
    - Strong scalability, following the open-close principle
        > What is Open-Closed Principle, OCP
        > Open for extension, closed for modification. Add new features via extension without changing existing code

## Hiding
- Similar to overriding: 
    - overriding means subclasses cover `instance methods` of the parent class
    - Hiding means subclasses cover `static methods` of the parent class
    ```java
    package charactor;
 
    public class Hero {
        public String name; 
        protected float hp; 
    
        //类方法，静态方法
        //通过类就可以直接调用
        public static void battleWin(){
            System.out.println("hero battle win");
        }
        
    }

    package charactor;
  
    public class ADHero extends Hero implements AD{
    
        @Override
        public void physicAttack() {
            System.out.println("进行物理攻击");
        }
        
        //隐藏父类的battleWin方法
        public static void battleWin(){
            System.out.println("ad hero battle win");
        }   
        
        public static void main(String[] args) {
            Hero.battleWin(); // hero battle win
            ADHero.battleWin(); // ad hero battle win
        }
    
    }
    ```
- Since static methods do not depend on instances at all, the `instantiated object on the right is hidden`, so it is called method `hiding`
    ```java
    class Hero{
        // 实例方法：重写
        public void attack(){
            System.out.println("父Hero普通攻击");
        }
        // 类静态方法：隐藏
        public static void battleWin(){
            System.out.println("父Hero胜利");
        }
    }

    class ADHero extends Hero{
        // 重写父类实例方法
        @Override
        public void attack(){
            System.out.println("ADHero平A攻击");
        }
        // 隐藏父类静态方法
        public static void battleWin(){
            System.out.println("ADHero胜利");
        }
    }


    Hero h = new ADHero();
    h.attack(); // ADHero平A攻击
    //no matter what, h is of type Hero
    //h.battleWin() is equivalent to Hero.battleWin();
    h.battleWin(); // 父Hero胜利
    ```

## supper
- super in Constructors
    - Whenever you create a subclass object with new, `the parent class constructor always runs first`
    - has `first-line restriction`
        - this. also must be the first statement inside a constructor
        - so super() and this. cannot exist in the same constructor
        ```java
        public class Hero {        
            public Hero(){
                System.out.println("Hero的构造方法 ");
            }
        }


        public class ADHero extends Hero implements AD{
            
            public ADHero(){
                System.out.println("AD Hero的构造方法");
            }
            
            public static void main(String[] args) {
                new ADHero(); 
                // Hero的构造方法
                // AD Hero的构造方法
            }
        }
        ```
    - Subclass no-arg constructor, `no super()` written
        - parent must has `explicit no-arg constructor + parameterized constructor`/ `only has no-arg constructor`
        - because `compiler will adds super() automatically`, calls parent no-arg constructor
        - so **"Subclass no-arg constructor, no super() written" is same as "Subclass no-arg constructor, with super() written"**
    - Any subclass parameterized constructor, `no super()` written
        - parent must has `explicit no-arg constructor + parameterized constructor`/ `only has no-arg constructor`
    - Any subclass parameterized constructor with `explicit super(parameters)` written
        - the parent does `not need` a no-arg constructor, but `must have` a matching parameterized constructor
- super in Ordinary Instance Methods
    - `No first-line restriction`, can be placed anywhere in the method body
- super with Member Variables
    - `super.attribute`: Access the `member variable of the parent` class forcibly
    - `this.attribute`: Access the `member variable of the current` subclass object
    - Without this or super, the subclass variable takes priority
    ```java
    public int getMoveSpeed(){
        return this.moveSpeed;
    }
    public int getMoveSpeed2(){
        return super.moveSpeed;
    }
    ```

## Object
- Object is the `root parent` class of all Java classes
- Every class `implicitly extends` Object without writing extends Object
    ```java
    public class Hero extends Object{}
    ```
- Common methods
    - toString()
        - Returns a `string description` of the current object
        - Printing an object via `System.out.println` outputs its toString() result
        ```java
        public String toString(){
            return name;
        }
        ```
    - finalize()
        - When `an object has no references pointing to it`, it `meets the conditions` for garbage collection
        - When the object is garbage collected, its finalize() method will be invoked
        - finalize() is not called manually by developers, but `by the JVM`
        ```java
        public class Hero {
            public String name;
            protected float hp;
            
            public String toString(){
                return name;
            }
            
            public void finalize(){
                System.out.println("这个英雄正在被回收");
            }
            
            public static void main(String[] args) {
                //只有一引用
                Hero h;
                for (int i = 0; i < 100000; i++) {
                    //不断生成新的对象
                    //每创建一个对象，前一个对象，就没有引用指向了
                    //那些对象，就满足垃圾回收的条件
                    //当，垃圾堆积的比较多的时候，就会触发垃圾回收
                    //一旦这个对象被回收，它的finalize()方法就会被调用
                    h = new Hero();
                }
            }
        }
        ```
    - equals()
        - is used to judge whether the whether two objects have the `same address`
            ```java
            Hero h1 = new Hero("盖伦");
            Hero h2 = h1; // h2 指向 h1 同一个对象
            Hero h3 = new Hero("盖伦"); // h3 是一个新对象

            System.out.println(h1.equals(h2)); // true → 同一对象
            System.out.println(h1.equals(h3)); // false → 不同对象        
            ```
        - similar to "=="
        - can be override (usually)
            ```java
            public class Hero {
                public String name;
                protected float hp;
                
                public boolean equals(Object o){
                    if(o instanceof Hero){
                        Hero h = (Hero) o;
                        return this.hp == h.hp;
                    }
                    return false;
                }
                
                public static void main(String[] args) {
                    Hero h1= new Hero();
                    h1.hp = 300;
                    Hero h2= new Hero();
                    h2.hp = 400;
                    Hero h3= new Hero();
                    h3.hp = 300;
                    
                    System.out.println(h1.equals(h2)); //false
                    System.out.println(h1.equals(h3)); //true
                }
            }
            ```
    - hashCode()
    - getClass()
    - methods related to thread synchronization
        - wait()
        - notify()
        - notifyAll()
- Exercise
    > Override the toString(), finalize() and equals() methods of Item.
    
    > toString() returns the name and price of the Item.

    > finalize() prints that the current object is being recycled.
    
    > equals(Object o) first checks whether o is an Item type, then compares whether the prices of two Items are equal.
    ```java
    public class Item{
        int name;
        double price;

        @Override
        public String toString(){
            return name + price;
        }

        @Override
        public void finalize(){
            System.out.println("this item is being recycled.");
        }

        @Override
        public boolean equals(Object o){
            if(o instanceof Item){
                Item h = (Item) o;
                return i.price == this.price;
            } 
            return false;
        }
    }
    ```

## final
- final class
    - cannot be extended
    ```java
    public final class String{}
    ```
- final method
    - cannot be overridden by subclasses
- final variable
    - cannot be reassigned
- final reference
    - cannot change object address, but object content can be modified
    ```java
        final Hero h;
        h  =new Hero();
        h  =new Hero(); // error
         
        h.hp = 5;  // work
        ```
- constants (static final)
    - unique in the whole class, cannot be reassigned forever
    ```java
    public static final int itemTotalNumber = 6;//物品栏的数量
    ```

## abstract
- abstract method
    - has `no method body`, only declaration
    ```java
    public abstract void attack();
    ```
    - No curly braces {}
    - Subclass extends abstract class
        - `Subclasses must override` all abstract methods
        - Or the `subclass is also an abstract` class
- abstract class
    - a class modified by abstract
    - when a class `has abstract method`, the class `must be an abstract class`
    - `cannot create object by "new"` (Cannot be instantiated)
    - `difference` of interface and abstract class
        - A `subclass` can `extend only one (abstract) class`, while can `implement many interfaces`
        - `define fields`
            - abstract class can `define fields` with
                - public, protected, package, private
                - static, non-static
                - final, non-final
            - while in interface, can only be defined by……, even there's no explicit statement
                - public 
                - static
                - fianl
                ```java               
                public interface AP {
                
                    public static final int resistPhysic = 100;
                    
                    //resistMagic即便没有显式的声明为 public static final
                    //但依然默认为public static final
                    int resistMagic = 0; 
                    
                    public void magicAttack();
                }
                ```

## Inner Class
- Why called inner class?
    - Inner class is `defined inside the body of another class`
    ```java
    Outer class {
        Inner class {}
    }
    ```
- Member Inner Class / Non-static Inner Class
    - defined inside the outer class, `outside all methods`
    - `at the same level` as member fields and member methods
    - without the static modifier
    - when be instantiated, need to be based on an instance
    - format: `Outer.Inner inner = new Outer().new Inner();`
    - can directly access all fields/methods outside, `including private fileds/methods`
    ```java 
    public class Hero {
        private String name; // 姓名
    
        float hp; // 血量
    
        float armor; // 护甲
    
        int moveSpeed; // 移动速度
    
        // 非静态内部类BattleScore，只有一个外部类对象存在的时候，才有意义
        // 战斗成绩只有在一个英雄对象存在的时候才有意义
        class BattleScore {
            int kill;
            int die;
            int assit;
    
            public void legendary() {
                if (kill >= 8)
                    System.out.println(name + "超神！");
                else
                    System.out.println(name + "尚未超神！");
            }
        }
    
        public static void main(String[] args) {
            Hero garen = new Hero();
            garen.name = "盖伦";
            // 实例化内部类
            // BattleScore对象只有在一个英雄对象存在的时候才有意义
            // 所以其实例化必须建立在一个外部类对象的基础之上
            BattleScore score = garen.new BattleScore();
            score.kill = 9;
            score.legendary();
        }
    
    }
    ```
- Static Inner Class
    - defined inside the outer class, `outside all methods`
    - `at the same level` as member fields and member methods
    - `with` the static modifier
    - when be instantiated, do not need to be based on an instance, can be created independently
    - format: `Outer.Inner inner = new Outer.Inner();`
    - `can only access static methods/fields` of outer class, cannot access instance members directly
    ```java
    public class Hero {
        public String name;
        protected float hp;
    
        private static void battleWin(){
            System.out.println("battle win");
        }
        
        //敌方的水晶
        static class EnemyCrystal{
            int hp=5000;
            
            //如果水晶的血量为0，则宣布胜利
            public void checkIfVictory(){
                if(hp==0){
                    Hero.battleWin();
                    
                    //静态内部类不能直接访问外部类的对象属性
                    System.out.println(name + " win this game");
                }
            }
        }
        
        public static void main(String[] args) {
            //实例化静态内部类
            Hero.EnemyCrystal crystal = new Hero.EnemyCrystal();
            crystal.checkIfVictory();
        }
    }
    ```
- Anonymous Inner Class
    - A temporary class `without a class name`
    - `inherits` parent class or implements interface immediately, overrides methods on site
    - `can only be used once`
    - format: 
        ```java
        Hero h = new Hero(){
            public void attack(){}
        };
        ```
    ```java
    public abstract class Hero {
        String name; //姓名
            
        float hp; //血量
            
        float armor; //护甲
            
        int moveSpeed; //移动速度
        
        public abstract void attack();
        
        public static void main(String[] args) {
            
            ADHero adh=new ADHero();
            //通过打印adh，可以看到adh这个对象属于ADHero类
            adh.attack();
            System.out.println(adh);
            
            Hero h = new Hero(){
                //当场实现attack方法
                public void attack() {
                    System.out.println("新的进攻手段");
                }
            };
            h.attack();
            //通过打印h，可以看到h这个对象属于Hero$1这么一个系统自动分配的类名
            
            System.out.println(h);
        }
    }
    ```
    - Local/Outer variables used `must be final` or effectively final
        - Why?: Anonymous inner class copies local variables. To `keep data consistent`, variables must be final
    - Cannot have constructor
- Local Inner Class
    - A class `with a name`, `defined inside a method block`
    - Local inner class = `named & reusable` anonymous inner class
    - format
        ```java
        public void method(){
            // 本地内部类
            class Hero{}
        }
        ```
    ```java   
    public abstract class Hero {
        String name; //姓名
            
        float hp; //血量
            
        float armor; //护甲
            
        int moveSpeed; //移动速度
        
        public abstract void attack();
        
        public static void main(String[] args) {
            
            //与匿名类的区别在于，本地类有了自定义的类名
            //main方法里的类
            class SomeHero extends Hero{
                public void attack() {
                    System.out.println( name+ " 新的进攻手段");
                }
            }
            
            SomeHero h  =new SomeHero();
            h.name ="地卜师";
            h.attack();
        } 
    }
    ```
    ```java
    public abstract class Hero {
        public abstract void attack();
    }

    public class Game {
        public void method() {
            // 方法里面的类 = 本地内部类 Local Inner Class
            class SomeHero extends Hero {
                @Override
                public void attack() {
                    System.out.println("本地英雄发起攻击");
                }
            }

            // 有名字！可以多次new使用
            SomeHero h1 = new SomeHero();
            SomeHero h2 = new SomeHero();
            h1.attack();
        }
    }
    ```

## default methods
- A `non-abstract` method `in interface` `modified by default`
- `with method body`
- Subclasses `do not have to override` it
    - but!!
    - when two interfaces have same default method → compile error
    - subclass(which implement the two interfaces) must override the default method to choose implementation
        - can use `interfaceName.super.defaultMethod();` **to call** the default implementation of a **specific parent interface**
        - Or `totally rewrite` a brand-new method logic of the defult method
```java
public interface Mortal {
    public void die();
 
    default public void revive() {
        System.out.println("本英雄复活了");
    }
}
```
- difference between `access modifier default` & `method type default`
    - `Java does NOT allow writing package / friendly / default as access modifiers`.Package-private access `can only be declared with no modifier`
    - 4 method types `in interface`
        - private(can only be used by itself,  `cannot be accessed outside`)
        - static(be used directly, `cannot be overrided/inherited`)
        - abstract(without method body, `must be overrided`, usually be omitted)
        - default(with method body, `could be overrided`)
        - {static, abstract, default} -> all `public by default`
- benifits / Why we have default methods?
    - Before Java 8, interfaces only had abstract methods.Adding new methods would break all old classes. Default methods have bodies, so old code doesn’t need to be modified
    - `Avoid breaking existing subclass code when updating interface`


## UML - Unified Module Language
- a standard `diagram language` to describe classes, interfaces, inheritance and implementation
- 3 structures
    - class name
    - attribute
    - method
- grammar: `Access Modifier name: data type`
    - Access Modified
        - + public
        - - private
        - # protected
        - ~ default/package
- relationships between classes
    - inheritance
        - Hollow triangle + Solid line
    - implementation
        - Hollow triangle + Dashed line
    - association
        - Solid straight line
    - aggregation/composition
        - Solid diamond + Solid line
- ![umlDiagramInterface](..\image\umlDiagramInterface.png)
- ![umlDiagramInherit](..\image\umlDiagramInherit.png)
- ![umlDiagramInherit](..\image\umlDiagramImplement.png)