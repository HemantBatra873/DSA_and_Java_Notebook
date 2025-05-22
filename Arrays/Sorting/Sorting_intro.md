# Sorting in java 

How do we take the array by the user and print its value?  
Use the Scanner class which is the part of the java.util package.

What is System.in?  
This is your device's standard input stream. Usually your keyboard.

Important Note -
When mixing nextInt() and nextLine() method of the scanner always make sure to consume the \n (the new line character that is created when the user presses enter) by using an extra nextLine() function after the nextInt() or next() function because these fucntionns 
do not eat the new line character \n.

After using scanner you must close it by using scanner.close(); when you are done.

```
import java.util.Scanner
```
In order to print array :  
Arrays.toString(arr) method imported from java.util.Arrays.

Note an important thing if you call a non-static method from you main method that is static it will give you an error because static method belongs to class and for non static methods we need an instance so you can either :
1. Make your non static method static.
2. Make an insatnce for the class and then call the method.
   
Now if you function does not have anything to do with the instances it will be better to go with option 1.
