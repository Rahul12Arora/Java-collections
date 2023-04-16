# Java-Jargon



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
