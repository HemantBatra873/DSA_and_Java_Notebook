# Sorting in java 

How do we take the array by the user and print its value?  
Use the Scanner class which is the part of the java.util package.

What is System.in?  
This is your device's standard input stream. Usually your keyboard.

Important Note -
When mixing nextInt() and nextLine() method of the scanner always make sure to consume the \n (the new line character that is created when the user presses enter) by using an extra nextLine() function after the nextInt() or next() function because these fucntionns 
do not eat the new line character \n.

```
import java.util.Scanner
