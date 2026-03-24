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
## Important
- Class `attributes` (e.g., name, age) and `methods` (e.g., functions like eating, running) `can never be written inside the main method`, here's why:
    - `Wrong "level"`
        - Think of a **"class" as a "house"**, and the **main method as the "front door (entrance)"** of the house. **Class attributes/operations** are like the **"furniture (tables, chairs)" and "functional areas (kitchen, bedroom)"** in the house
        - You can only put furniture/functional areas "inside the house" (at the class level) — not "inside the front door" (inside the main method)
    - `Java rules don’t allow it`
        - Java’s rule is clear: `A method (like main) can only contain` `"temporary things"` (e.g., local variables) and `"actions to execute"` (e.g., using furniture, opening/closing doors) 
    - `Different purposes`
        - `Class attributes/operations` are "shared by the whole house" (`usable by all methods`), while `things inside main` only work "when you go through the front door" — they `become useless once you leave the door`. If you put attributes/operations inside main, other methods can’t use them at all, and the "class" loses its meaning