# Java-Jargon

Note:

<ul>
	<li>The .java file name should be equal to the public class name that contains the main method in it</li>
	<li>Other sibling classes cannot be public or static</li>
	<li>The inner classes can be used with any modifiers</li>
</ul>

<h2>Access Modifiers</h3>

<h3>Private Access Modifier</h3>
As the name suggests, the scope of this modifier is very restricted.</br>
When the data members and the class methods are prefixed with a private modifier, they can be accessed only in the class itself even the other classes of the same package cannot access the private members or methods.</br>

```
class Scaler {

  //Private members
  private int roll;
  private String name;

  //Parameterised Constructor
  Scaler(int a) {
    System.out.print(a);
  }

  //Default constructor private
  private Scaler() {}

  //Private method
  private void print() {
    System.out.println("This is the Scaler class");
  }
}

class Main {

  public static void main(String args[]) {
    //Creating the instance of the Scaler class
    //This will successful run
    Scaler ob1 = new Scaler(1);
      
    //Creating another instance of Scaler class
    //This will cause an error
    Scaler ob = new Scaler();
      
    //These two lines also cause errors.
    ob.name = "Aayush";
    ob.print();
  }
}
```

<h3>Public Access Modifier</h3>
The public modifier provides no restriction on the methods, classes, and instance members of the particular class.</br>
When they are prefixed by the public modifier, they can be accessed in any package, in any class. The scope of the public modifier is very flexible as compared to the other modifiers.</br>

```
package First;

public class Scaler {

  //Instance member
  public int id = 1;

  //Class method
  public void print() {
    System.out.println("This is the Scaler class");
  }
}
-----------------------------------------------------------------------
package Second;

import First.Scaler;

public class InterviewBit {

  public static void main(String[] args) {
    //Creating the instance of the Scaler class
    Scaler ob = new Scaler();
    //Accessing the instance member of scaler class
    System.out.println(ob.id); //print 1
    //This is the Scaler class will print
    ob.print();
  }
}
```

<h3>Protected Access Modifier</h3>
We can use protected modifier methods, instance members within in the same package and access them in another package with the help of a child class which means we have to extend the class that contains protected members in another package.</br>

We cannot access them directly by creating the object of a class that contains protected members and functions.</br>

```
package First;

public class Scaler {

  int id = 1;

  protected void print() {
    System.out.println("This is the Scaler class");
  }
}
-----------------------------------------------------------------------
package Second;

import First.Scaler;

class InterviewBit extends Scaler {

  public static void main(String[] args) {
    Scaler ob = new Scaler();
    //This line will cause an error
    ob.print();

    InterviewBit ob1 = new InterviewBit();
    //This line will not cause an error
    ob1.print();
  }
}
```

<h3>Default Access Modifier</h3>

When the instance members, methods of the class are not specified with any modifier. It is said to be having a default modifier by default. The instance members and methods declared with default modifier can be accessed only within the same package. Hence it is sometimes called package-private.</br>

Real-life example: In the Facebook account, when you set your privacy status to "visible to your friends only".You and your's known friends can access your status.</br>


<h3>ArrayList</h3>

```
#Array to List conversion

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8);

or

Integer[] arr = {1, 2, 3, 4, 5};
List<Integer> list = new ArrayList<>(Arrays.asList(arr));

------------------------------------------------------------------------------------
		// For Each Loop for iterating ArrayList
		for (int i : numbers)
    { System.out.print(i + " "); }
------------------------------------------------------------------------------------    
    Iterator it = numbers.iterator(); 
        // Holds true till there is single element remaining in the list
        while (it.hasNext())
        { System.out.print(it.next() + " "); }
------------------------------------------------------------------------------------
    numbers.forEach(number->System.out.println(number));
------------------------------------------------------------------------------------
    for (int i = 0; i < numbers.size(); i++)
            // Printing and display the elements in ArrayList
            System.out.print(numbers.get(i) + " ");
------------------------------------------------------------------------------------
```

#Collections

![image](https://user-images.githubusercontent.com/108695777/232307390-599e05b4-c71c-4210-a0fa-d561e5620cc2.png)

#Generics

**The idea is to allow type (Integer, String, … etc and user-defined types) to be a parameter to methods, classes and interfaces. For example, classes like HashSet, ArrayList, HashMap, etc use generics very well. The generic classes can only be used for Non-primitive types and wrapper classes. Here are the major advantages of Generics in Java:**


1. Write once use for any non-primitive type: For eg, a single generic function can be written to add two numbers for multiple data types like Integer, Double, etc. Also, a single generic function can be written to print the elements of an array of any data type. The data types are passed to the generic function during compile time.</br>


2. Java Collections extensively use Generics: All the classes, interfaces and utility functions are generic functions and generic classes. For eg., ArrayList class can be used to work on various types of data types be it Integer, Character or user-defined data types like Student etc.</br>

3. Generics can be a class like ArrayList, LinkedList, Stack, Vector. It can be interfaces like Set, Map etc. They include functions like binarySearch(), sort, max(), min() etc.</br>

4. Type-Safe: Generics make errors to appear at compile time than at run time(It’s always better to know problems in your code at compile time rather than making your code fail at run time). Let's understand this using the following example.</br>


Example 1: In this, no Generic function is used and thus the code throws a RunTime exception.</br>

```
// A Simple Java program to demonstrate that NOT using 
// generics can cause run time exceptions 
import java.util.*; 

// Object class
class Pair {
    Object x;
    Object y;
}
class Test 
{ 
    public static void main(String[] args) 
    { 
        Pair p = new Pair();
        
        // Compiles fine because
        // p being an object accepts integer
        p.x = 12;
        
        // Compiles fine because
        // p being an object accepts string
        p.y = "GfG";
        
        // This throws a ClassCastException
        // as p.x was an integer and cannot be
        // casted to a string
        String str = (String) p.x;
    } 
} 
-------------------------------------------------------------------
Output:
Exception in thread "main" java.lang.ClassCastException: 
java.lang.Integer cannot be cast to java.lang.String
    at Test.main(File.java:16)
```

Example 2: In this, Generic function is used and thus the code shows compile-time errors.

```
// Using generics converts run time exceptions   
// into compile time exception. 
import java.util.*; 

// Generic class
class Pair<T, S> {
    T x;
    S y;
}
class Test 
{ 
    public static void main(String[] args) 
    { 
        // Creating object of generic class
        Pair<Integer, String> p = new Pair<Integer, String>();
        
        // Compiles fine because
        // p being an object accepts integer
        p.x = 12;
        
        // Compiles fine because
        // p being an object accepts string
        p.y = "GfG";
        
        // This shows compiler error
        // as p.x was an integer and cannot be
        // casted to a string
        String str = (String) p.x;
    } 
} 
-----------------------------------------------------------------------
Output:
prog.java:28: error: incompatible types: 
Integer cannot be converted to String
        String str = (String) p.x;
                               ^
1 error
```

Example 3: Working of a generic function.

```
// Java code to demonstrate working of
// generic function
import java.util.*; 

class Test 
{ 
    // Declaration of generic function
    // Type parameters defined before 
    // return type
    public static<T> int count(T arr[], T x)                   // we need to madatorily specify function return type as "static<T> int"
    {
        int res = 0;
        
        // Traverse the array
        for(T e: arr)
        {
            if (e.equals(x))
                res++;
        }
        return res;
    }
    public static void main(String[] args) 
    { 
        Integer arr[] = {10, 20, 30, 40, 10, 30};
        System.out.println(count(arr, 10));            //We don't need to specify count<Integer> here because java automatically infers this from the arguments
    } 
} 
---------------------------------------------------------
Output:
2
```

Question: Guess the output of the following code.

```
// Java code to demonstrate working of
// generic function
import java.util.*; 

// Generic class
class MyGen<T> {
    T x;
    static int count;
    MyGen()
    {
        count++;
    }
}
class Test 
{ 
    public static void main(String[] args) 
    { 
        // Creating object of generic class
        MyGen<Integer> m1 = new MyGen<>();
        
        // Creating object of a generic class
        MyGen<Integer> m2 = new MyGen<>();
        
        System.out.println(MyGen.count);
    } 
} 
-------------------------------------------------
Output:
2
```
