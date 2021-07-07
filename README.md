# OOPS IN JAVA



## why this documentation?
- OOPS in java is kinda huge topic,so i thought documenting would help in future for quick revision.I've tried to highlight
core concepts with examples along with common misconceptions,points to remember and good programming practices.

- Documentation is a good soft skill to have,so why not start with this?

## contents
- Java Source File Structure.


- Import Statements.


- Package Statements


- Class Level Modifiers
   - public and default modifier                                            
    - abstract modifier(abstract methods and abstract classes)
    
    
- Member Modifiers

## Java Source File Structure

A java program can contain any number of classes,but at most only one public class is allowed.
If there is no public class,then there are no restrictions on the name of java program and but if a public class exists in a program
then name of java file and public class name must be same.

Common misconception:java file is named after the class which contain main method.
But there is no relation between java file name and classes which contain main method.If there are n classes with n main methods
there is no restriction on the name of the java program.

If n classes contain n main methods,when we run a .class file,the main method corresponding to particular class will be executed.
When we run a .class file that contains no main method,we get an exception.

Remember:
> We can compile a .java program but we can run a .class file.

## Import Statements

We use it to access diffrent package and its classes.
For example,if we want to use Scanner class which is already defined,we tell the compiler to import the Scanner class from java.util package.

Without import statements,if we want to use any classes/methods of another class,then fully qualified names can be used.

Example:  ` java.util.Scanner sc=new Scanner(); ` is valid without any import statements.
But fully qualified names increase code redundancy and decrease readability,beacuse every time use Scanner class,you should use the
above the syntax,so this is not recommended.

Types of import:


1.Explicit import.  [eg: java.util.ArrayList]


2.Implicit import   [eg:java.util.*]

Explicit import is always recommended over implicit import,just beacause it improves code readability.
Its not a good programming practice to use implicit import.

Example 1:
``` java

import com.hdfc.*;
import com.icici.*;
.
.
.
Loan loan=new Loan();
Account acc=new Account();
```
Example 2:
```java

import com.hdfc.Account;
import com.icici.Loan;
.
.
.
Loan loan=new Loan();
Account acc=new Account();

```

In the first example,when we create loan and account objects,we clearly dont know to which banks they refer to.
In the second example,we clearly know that loan object is from Loan class of icici bank and acc object is from HDFC Account class.

By deafult java.lang package is imported,there is no need to import explicitly.
Whenever we are importing java package all classes present inside the package are available but not sub package classes.

ex:   [java->util->regex->Pattern]
        To use Pattern class importing ` java.util.* ` is not valid, ` java.util.regex.* ` must be used.

## Package Statements

A group of related class and interfaces are grouped into a single unit called package.
For example to handle database operation,the required classes and interfaces are grouped into java.sql package.

Advantages:


1.Resolves naming conflicts.


For example,there are two Date classes[one in sql package,one in util package],but these can be easily diffrenciated using packages.


2.Modularity.(grouping related things under one roof)


3.Maintainability.(Easy to debug)


4.Security.(If classes are not declared public,then they cant be accessed)



> Creating packages is a good programming practice.

Naming convention of packages:use client internet domain name in reverse.


ex:If icici.com is the domain name,then use 'com.icici' as the package name[Highly recommended].



Inside any java program,at most only one package statement is allowed.


package statements cannot be used in between any java code.[only in the beginning]

order is important:


package statement [atmost one]


import statements [any #]


class/interfaces/enum [any #]



# Class Level Modifiers

## public and default

If no class level modifier is specified then by default,the class level modifier is default,which means the class can be accessed only within the package.


If the class is public,then there are no restrictions which means it can be accessed inside the package as well as outside the package.


If the class is abstract,then object creation is not poosible.[instantaneous is not possible].


If the class is final,then child creation/child class is not possible.



Remember:
> If you want to restrict object creation for your class,declare it as abstract.



Class level modifiers that are applicable to top level classes and inner classes:

``` java

class MyTopLevelClass   // This is top level class
{
        class MyInnerClass    // This is inner class
        {

        }
}
```

Remember:
> Inner class is diffrent from child class

The five class level modifiers that are applicable for top level class are:


1.public


2.default
  
  
3.abstract
  
  
4.final
  
  
5.strictfp
  
  

The three class level modifiers that are applicable for inner class level are:
  
  
1.private
  
  
2.protected
  
  
3.static
  
  

Consider this,

  
  
  ``` java
  package pack1;
  public class A
  {
  
  }
  
  ```
  
   ``` java
  package pack2;
  import pack1.A;
  public class B
  {
       public static void main(String args[])
       {
            A  obj=new A();
       }
  }
  
  ```
Since the class 'A' is declared public,it can be used in class 'B' of diffrent package just by importing it.

If class 'A' is not declared public and if we try to access it from diffrent package,then we get a compile time error saying
"A is not public in pack1,cannot be accessed from outside package".

Remember:
> Default modifier is also known as package level access.

## abstract modifiers

Abstract-partially completed/partial implementation.

Abstract modifiers are applicable for,
* Methods
* class

Remember:
> Abstract modifier is not applicable for variables.

### Abstract methods:

If you dont know complete implementation,we can declare it as abstract method so that child classes inheriting our class will have 
to provide implementation for the same method.

Remember
> Abstract method has only declaration but not implementation. [abstract methods cannot have a body]

consider this example,

```java
abstract class vehicle
{
      public abstract int getNumberOfWheels();
}
```
Above method 'getNumberOfWheels' is declared abstract because we dont the number of wheels a vehicle has.Based on the vehicle
the return value of this method will change[if its a car we return 4,if its a bike we return 2 and so on].
So instead of implementing it we just declare it.Child classes are responsible to provide implementation for these classes.

```java
public class car extends vehicle    //here 'car' class is a child of 'vehicle' class
{
         public int getNumberOfWheels()
         {
                 return 4;
         }
}
```

'car' class is a child class of 'vehicle',so 'car' class is responsible to provide implementation for 'getNumberOfWheels' method.
Since its a car class,in implementation we return 4.

Remember:
> If a class contains atleast one abstract method,then the class should be declared as abstract.

### Abstract class

Abstract classes are partially implemented classes and object creation is not allowed.

why object creation/instantiation is not allowed for abstract classes?
> If some other class creates a object of abstract class and calls a abstract method using same object,then the abstrct method cannot return anything 
since its not completely implemented,so we should restrict object creation.

Points to remember:

* If a class contain atleast one abstract method,then the class must be declared as abstract.
* Even though a class contain no abstract methods,the class can be declared as abstract.
* Childs classes are responsible to provide implementation for parent abstract methods.
* If there are n abstract methods in parent class,the child class must implement/override n methods or incase if the child class
   cannot override all abstract methods,then the child class must also be declared as abstract.The responsibility of implementing other 
   abstract methods will be given to next level child classes.


Example to sum up everthing about abatract classes and methods:

```java
abstrct class Vehicle   //this is abstract class
{
    public abstract int getNumberOfWheels();  // abstract method
}

class Car extends Vehicle    //car is a child class of vehicle,so it must implement 'getNumberOfWheels' method.
{
    public int getNumberOfWheels()
     {
	return 4;
     }
}

class Bike extends Vehicle   //bike is a child class of vehicle,so it must implement 'getNumberOfWheels' method.
{
    public int getNumberOfWheels()
     {
	return 2;
     }
}
 
class MyClass
{
      public static void main(String[] args)
     {
                Car car=new Car();
                System.out.println(car.getNumberOfWheels());   // prints 4

                Bike bike=new Bike();
                System.out.println(bike.getNumberOfWheels());  // prints 2
     }
}
```
## member modifiers

#### public

If any data memeber is declared public,then the data memeber can be accessed from same package as well as diffrent package.[no restrictions]
But make sure that the class in which the data memeber resides is public.

``` java
class A
{
  public void m1()
  {
  
  }
}

```
In the above case,even though ` m1() ` is public,the class is not public,so the method will not be accessible outside the package.

remember:
> Default data memebers are not accessible outside the package.

#### private

If any methods,variables are declared private,then those will be accessible in same class only.They cant be accessed from outside the class.

consider this example,

``` java

package pack1;
class A
{
	private void m1()
	{
		System.out.println("Hello");
	}
}

public class B
{
	public static void main(String args[])
	{
		A a=new A();
		a.m1();   //since m1 is declared private in class A,it cant be called from other class.
	}
}


```

> Its a good programming practice to use private modifier to our variables.[highly recommended]
> Recommended modifier for methods is public,since they serve functionality to other data memebers.

To sum up:


|  **Modifiers**  | **Access level** |
| --- | --- |
| *private* | *class level* |
| *default* | *package level* |
| *public*| *global level* |


















## How to reach me: 

  
[Github](www.github.com/tarunsraina)


[linkedin](https://www.linkedin.com/in/tarun-teja-814b3a1a9) 
       
[instagram](https://www.instagram.com/tarunsraina) 

gmail:tarunsraina483@gmail.com

## Resources:

[How to use mark down language](https://www.youtube.com/watch?v=eJojC3lSkwg)

[OOPS in java](https://www.youtube.com/watch?v=5NQjLBuNL0I&t=15s)


#### If you find any errors please report the same,Thank you.







