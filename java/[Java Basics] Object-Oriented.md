# Java Basics - Object-Oriented

## Class
- an `abstract` definition/template for a group of objects with the same attributes and operations 
- the class name
    - the `first letter` should be `uppercase`
    - if consists of multiple words, the `first letter of each subsequent word` should be `uppercase`
## Attribute
- the data/state that `describes the characteristics` of an object/class
- the attribute name
    - the `first letter` should be `lowercase`
    - if consists of multiple words, the `first letter of each subsequent word` should be `uppercase`
## Method
- the `behaviour/function` that an object can perform
- representing the dynamic `features` of a **class or object**
- implement specific **functions** `based on` the object's `attribute`
- can accept parameter
- type
    - have return value
        - `clarify the type` of the return
        - need to write `"return"` inside the method
    - do not have return value
        - set method to `void`
- the method name
    - using a verb to begin
    - the `first letter` should be `lowercase`
    - if consists of multiple words, the `first letter of each subsequent word` should be `uppercase`
## Example
```java
public class Item {
    String name;
    int price;
    float hp;

    // without return, then should set the method to be "void"
    void legendary(){
        System.out.println("legendary!");
    }

    // with return, then should clarify the type of return value
    float getHp(){
        return hp;
    }

    // with parameter
    void recovery(float blood){
        hp = hp + blood;
    }

    // the entrance of a class, should be static and void, the parameter should be String type
    public static void main(String[] args){
        Item blood = new Item();
        blood.name = "血瓶";
        blood.price = 50;

        Item grass = new Item();
        grass.name = "草鞋";
        grass.price = 350;
    }
}

```