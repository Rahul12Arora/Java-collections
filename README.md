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
