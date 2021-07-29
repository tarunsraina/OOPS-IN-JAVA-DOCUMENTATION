# OOPS IN JAVA



## Why this documentation?
- OOPS in java is kinda huge topic,so i thought documenting would help in future for quick revision.I've tried to highlight
core concepts with examples along with common misconceptions,points to remember and good programming practices.


## Contents
- Java Source File Structure.


- Import Statements.


- Package Statements


- Class Level Modifiers
   - public and default modifier                                            
    - abstract modifier(abstract methods and abstract classes)
    
    
- Member Modifiers
  - public
  - default
  - private
  - protected
  
  
 - Interface
 
 
 - Data hiding
 
 
 - abstraction
 
 
 - Encapsulation
 
 

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
But fully qualified names increase code redundancy and decrease readability,beacuse every time you use Scanner class,you should use the
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
## Member modifiers

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



#### protected

If variables or methods are declared as protected,then


case 1:Within the current package,you can access those variable or methods[no restrictions]

case 2:From outside the package,they can be accessed from child classes only.

> protected=default + child classes

To sum up:


|  **Modifiers**  | **Access level** |
| --- | --- |
| *private* | *class level* |
| *default* | *package level* |
| *public*| *global level* |

``` java
package pack1;
class A
{
	protected void m1()
	{
		System.out.println("Hello");
	}
}

class B extends A
{
	public static void main(String args[])
	{
		A a=new A();
		A.m1();
		
		B b=new B();
		b.m1();
		
		A obj=new B();
		obj.m1();
	}
}

```


Above example is valid,since both classes are in the same package,protected method can be called from anywhere within the same package.



consider same example,but in diffrent packages:

``` java

package pac1;
class A
{
	protected void m1()
	{
		System.out.println("Hello");
	}
}

```

``` java

package pack2;
import pack1.A;
public class B extends A
{
	public static void main(String args[])
	{
		
		A a=new A();
		A.m1();     	// not valid because of parent reference
		
		B b=new B();
		b.m1();   	 // valid
		
		
		A obj=new B();
		obj.m1();   	// not valid because of parent reference
	}
}

```

Remember:
> parent reference cannot be used to access protected members


#### summary of public,protected,default and private

| **visibility** | **public** | **protected** | **default** | **private** |
| --- | --- | --- | --- | --- |
| within the same class | yes | yes | yes | yes |
| from child class of same package | yes | yes | yes | no |
| from non-child of same package | yes | yes | yes | no |
| from child class of outside package | yes | yes[child reference only] | no | no |
| from non-child class of outside package | yes | no | no | no |


Restrictions high to low:
> private>default>protected>public







## Interface

def 1:Interface is defined as any service requirement specification(SRS).
def 2:Any contract between client and service provider is considered as interface.
def 3:

Consider this example,Lets say a particular company has three branches(head office,Branch A,Branch B)

Head office wants to know the number of active customers in from their sub-branches

case 1:If Interface is not used.

If head office wants to call a method to know active customers,they first have to know which method gives them active customers.
Lets say Branch A named its method as `getActiveCustomers()` and Branch B named its method as `getActCust()`.After knowing which 
methods serve their functionality they will call those two methods and get total active customers.

case 2:If interface is used.

Both branch A and B must implement a interface of Head Office.If head office wants to call a method to know active customers,
Since both the branches are implementing the interface,it must implement same methods.
The head office need not to worry about what methods to call.They can use the same methods that they use,
since both branches are implementing the interface provided by the head office.


## Declaration and implementation of interface


``` java

 interface MyInterface
{
       public void getMyDetails();
       public void updateMyDeatils();
}
//This is interface declaration,it has no implementation.The class has to provide implementation.

//The implementing class should use the keyword `implements` to implement a interface.

class serviceProvider implements MyInterface
{
        public void getMyDetails()  
        {
	//rule 1:must be declared public
        }

        public void updateMyDetails()
        {
	//rule 2:The implementing class must provide implementation for every methods of the interface
	//If you fail to implement all methods of interface,just declare your class as abstract
        }
}

```


## Data hiding

 we can implement data hiding by declaring variables as private.


Example to illustrate data hiding :

``` java

class Account
{
        private double balance;
         //Since this is private,it is automatically implementing data hiding.

        // Now,to check balance,validation is required

         public void getMybalnce
         {
	//validate user credentials

	if(valid)
	{
		return balance;
	}
         }
}

```

## Abstraction

Hiding internal implementation and highlight services provided.

Example:You know how ATM card swipe can be used and services provided,but you dont the queries,servers it is using to validate you.
Exposing these queries,servers,ip address is not recommended for security reasons.This is where abstraction must be used.

Advantages:



1.security


2.Enhancement will be easy


3.Maintainabilty


4.Modularity




## Encapsulation


The process of grouping data members and corresponding methods into a single unit is called encapsulation.
Every java class is an example for encapsulation.

> Encapsulation=Data hiding + abstraction

``` java

class Account
{
     private double balance;

     public void getBalance()
     {
	//validate the user
                   return balance;	
     }

    public void setbalance(double balance)
    {
	//validation
	//perform required operation
    }
}

```



















## How to reach me: 

  
[Github](www.github.com/tarunsraina)            
[Linkedin](https://www.linkedin.com/in/tarun-teja-814b3a1a9)                              
[Instagram](https://www.instagram.com/tarunsraina)                  
[Codechef](https://www.codechef.com/users/tarun728)          
[Hackerrank](https://www.hackerrank.com/tarunsraina)     
[Sololearn](https://www.sololearn.com/Profile/17499531/?ref=app)                 
Gmail:tarunsraina483@gmail.com
## Resources:

[How to use mark down language](https://www.youtube.com/watch?v=eJojC3lSkwg)

[OOPS in java](https://www.youtube.com/watch?v=5NQjLBuNL0I&t=15s)

#### I will keep updating this documentation with more topics.
#### If you find any errors please report the same,Thank you.







