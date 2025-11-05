# Car Fleet

https://leetcode.com/problems/car-fleet/description/

There are n cars at given miles away from the starting mile 0, traveling to reach the mile target.

You are given two integer arrays position and speed, both of length n, where position[i] is the starting mile of the ith car and speed[i] is the speed of the ith car in miles per hour.

A car cannot pass another car, but it can catch up and then travel next to it at the speed of the slower car.

A car fleet is a single car or a group of cars driving next to each other. The speed of the car fleet is the minimum speed of any car in the fleet.

If a car catches up to a car fleet at the mile target, it will still be considered as part of the car fleet.

Return the number of car fleets that will arrive at the destination.

## Understandings

The main thing is that when a fast car goes past a slow car it's speed reduces to the speed of slow hence the time after then also depends on the slow cars time. 

This makes it easier for us as we can be sure that if a car has less time to reach that the car ahead it will reach in same fleet ad we also have the speed of this fleet. And if a car has less time to target than the car ahead then it will reach as an independent fleet.

We can actually also do this without the stack by keeping some variables but this is a good question where stack is useful.

## With stack solution 

```java

class Solution {
    public int carFleet(int target, int[] position, int[] speed) {
        int n = position.length;
        
        int[][] cars = new int[n][2];
        for (int i = 0; i < n; i++) {
            cars[i][0] = position[i];
            cars[i][1] = speed[i];
        }
        
        Arrays.sort(cars, (a, b) -> Integer.compare(b[0], a[0]));
        
        Stack<Double> stack = new Stack<>();
        
        for (int[] car : cars) {
            int pos = car[0];
            int spd = car[1];
            double timeTaken = (double)(target - pos) / spd;
            
            if (stack.isEmpty() || timeTaken > stack.peek()) {
                stack.push(timeTaken);
            }
        }
        
        return stack.size();       
    }
}

```java

## Without Stack same logic 

```
class Solution {
    public int carFleet(int target, int[] position, int[] speed) {
        int n = position.length;
        int[][] cars = new int[n][2];
        
        for (int i = 0; i < n; i++) {
            cars[i][0] = position[i];
            cars[i][1] = speed[i];
        }

        Arrays.sort(cars, (a, b) -> b[0] - a[0]);  // sort by position descending

        int fleets = 0;
        double prevTime = 0;

        for (int[] car : cars) {
            double time = (double) (target - car[0]) / car[1];
            if (time > prevTime) {   // new fleet
                fleets++;
                prevTime = time;
            }
        }

        return fleets;
    }
}
```