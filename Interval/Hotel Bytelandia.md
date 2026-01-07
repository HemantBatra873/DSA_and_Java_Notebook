# Hotel Bytelandia

https://www.codechef.com/practice/course/2-star-difficulty-problems/DIFF1500/problems/HOTEL?tab=statement

2ways - 

1. Event based 
- Sort both arrival and departure into one vector then treat them like events arrival increments count and departure decrements count. At each step you count max as max of max and count.

2. PriorityQueue based
- My first approach was make an array of interval with [arrival, departure] then sort it according to arrival time and every time on arrival keep removing previous guests count based on PriorityQueue of Integers.