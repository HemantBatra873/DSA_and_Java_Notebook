# Ceil and floor direct for integer division in Java

if you need two integers floored this is default in java 

eg. 

3 / 2 = 1

But if you want ceil value then the trick is 

(3 + 2 - 1) / 2

Which means add denom - 1 will give you the ceil in integer form.