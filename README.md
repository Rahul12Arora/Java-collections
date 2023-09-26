# Java-Jargon

Note:

<ul>
	<li>The .java file name should be equal to the public class name that contains the main method in it</li>
	<li>Other sibling classes cannot be public or static</li>
	<li>The inner classes can be used with any modifiers</li>
</ul>



# Collections

![image](https://user-images.githubusercontent.com/108695777/232307390-599e05b4-c71c-4210-a0fa-d561e5620cc2.png)

# Generics

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

#Arguments are Pass Bye Value In Java

In Java, all arguments to methods are passed by value, but it's important to clarify what "passed by value" means in this context, especially when dealing with objects.

1. **Primitive Data Types (Passed by Value):** For primitive data types (e.g., `int`, `float`, `boolean`), the actual value of the variable is passed to the method. Any changes made to the parameter inside the method do not affect the original variable.

    ```java
    public void modifyValue(int x) {
        x = 10;
    }
    
    int num = 5;
    modifyValue(num);
    System.out.println(num); // Output: 5 (unchanged)
    ```

2. **Reference Data Types (Passed by Value):** When you pass an object (e.g., instances of classes) as an argument to a method, what is actually passed is a copy of the reference to the object in memory. This copy of the reference still points to the same object in memory. However, you cannot change the original reference itself within the method.

    ```java
    class MyClass {
        int value;
        MyClass(int value) {
            this.value = value;
        }
    }

    public void modifyObjectReference(MyClass obj) {
        obj = new MyClass(10); // This changes the local reference, not the original object.
    }

    public void modifyObjectValue(MyClass obj) {
        obj.value = 10; // This changes the value of the original object.
    }

    MyClass myObject = new MyClass(5);
    modifyObjectReference(myObject);
    System.out.println(myObject.value); // Output: 5 (unchanged)

    modifyObjectValue(myObject);
    System.out.println(myObject.value); // Output: 10 (changed)
    ```

In the first example (`modifyObjectReference`), the local reference `obj` is changed to point to a new object, but the original object remains unchanged.

In the second example (`modifyObjectValue`), we modify the object's internal state through the reference, so the changes are reflected in the original object.

In summary, Java passes all arguments by value, but when dealing with reference types, it's essential to understand that you are passing a copy of the reference, not the object itself. Changes to the object's state through the reference are visible outside the method, while reassigning the reference inside the method doesn't affect the original reference outside the method.
