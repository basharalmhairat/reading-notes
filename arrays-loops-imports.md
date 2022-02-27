
## packages
---
A package is a single folder containing a group of related classes .

A package declaration, must be the first thing in the file, and describes the folder . For example, the declaration:

***package org.xml.sax;***

specifies that the class is to be found in the directory org/xml/sax.

The import declaration can be used to make an entire package, or individual classes within a package, more easily accessible to your Java program.

If no package declaration is specified in a file, the "default package" is used. The default package cannot be imported by other packages.
- another axample:
***import javax.swing.*; // Make all classes visible altho only one is used.**

```
import javax.swing.JOptionPane;  // Make a single class visible.

class ImportTest {
    public static void main(String[] args) {
        JOptionPane.showMessageDialog(null, "Hi");
        System.exit(0);
    }
}
```
### Types of packages in Java
---
1) User defined package: The package we create is called user-defined package.
2) Built-in package: The already defined package like java.io.*, java.lang.* etc are known as built-in packages.
**example**
```
package letmecalculate;

public class Calculator {
   public int add(int a, int b){
	return a+b;
   }
   public static void main(String args[]){
	Calculator obj = new Calculator();
	System.out.println(obj.add(10, 20));
   }
}
```
---
## loops
Loops in Java is a feature used to execute a particular part of the program repeatedly if a given condition evaluates to be true.

While all three types’ basic functionality remains the same, there’s a vast difference in the syntax and how they operate.

|Difference|For Loop|While Loop|Do-While Loop|
|:---:|:---:|:---:|:---:|
|Introduction|For loop in Java iterates a given set of statements multiple times.|The Java while loop executes a set of instructions until a boolean condition is met.|executes a set of statements at least once, even if the condition is not met. After the first execution, it repeats the iteration until the boolean condition is met.|
|Best time to use|Use it when you know the exact number of times to execute the part of the program.|Use it when you don’t know how many times you want the iteration to repeat.|Use it when you don’t know how many times you want the iteration to repeat, but it should execute at least one time|
|Syntax|```for(init; condition; icr/dcr){//statements to be repeated}```|```hile(condition){//statements to be repeated}```|```do{//statements to be repeated}while(condition);```|
|Example|```for(int x=0; x<=5; x++){System.out.println(x);}```|```int x=0;while(x<=5){System.out.println(x);x++;}```|```int x=0;do{System.out.println(x);x++;}while(x<=5);```|












