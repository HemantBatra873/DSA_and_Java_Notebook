# Binary Search on Answer (Parametric Search)

Binary Search on Answer is used when you are not searching in a sorted array but instead searching for a **numeric value** that satisfies a condition. The answer lies within a **range of possible values**, and you use a helper function (`check(x)`) to determine whether a candidate value is valid.

---

## 1. When Do We Use Binary Search on Answer?

Binary Search on Answer is used when **all three** of these conditions hold:

### **1. The answer is a number within a range**

There is no array to search. Instead, the solution is some integer or real value like:

* Minimum speed
* Minimum time
* Maximum capacity
* Minimum cost

---

### **2. There exists a monotonic relation**

If a candidate value `x` works:

* All values **greater than x** also work, or
* All values **less than x** also work

This monotonic behavior allows binary search.

---

### **3. You can write a function `check(x)` that verifies a candidate in O(n)**

For each candidate value `x`, you can test whether it meets the problem's requirements.

Examples:

* Can Koko finish bananas at speed `x`?
* Can we ship packages with capacity `x`?
* Can we finish tasks in `x` hours with these workers?

---

## 2. Classic Example Template

```java
int l = lowPossibleValue;
int r = highPossibleValue;

while (l < r) {
    int mid = l + (r - l) / 2;
    if (check(mid)) {
        r = mid;   // mid works, try smaller
    } else {
        l = mid + 1; // mid fails, try larger
    }
}
return l; // or r
```

---

## 3. Common Patterns

### **Pattern 1: Minimize the Maximum / Maximize the Minimum**

Examples:

* Koko Eating Bananas
* Allocate Minimum Pages
* Split Array Largest Sum
* Painters Partition Problem
* Minimize Max Distance between Gas Stations

These ask:

> What is the minimum value K such that some condition is satisfied?

---

### **Pattern 2: Feasibility Check Problems**

Examples:

* Ship packages within D days
* Finish tasks within H hours
* Find minimum time to complete builds

Here, `check(x)` tests whether a given time/capacity/speed is enough.

---

### **Pattern 3: Problems with very large search space**

If the answer could be anywhere from 1 to 1,000,000,000, you cannot iterate. But binary search solves it in ~30 steps.

---

### **Pattern 4: Numeric answers with monotonicity**

The types of answers you can search for:

* Speed
* Time
* Distance
* Capacity
* Height
* Threshold
* Cost

If increasing (or decreasing) the answer always keeps the problem valid, binary search applies.

---

## 4. Intuition in One Line

> Use Binary Search on Answer when the answer is a number, not in the array, and you have a `check(x)` that is monotonic.

---

## 5. Example Problems

* Koko Eating Bananas
* Split Array Largest Sum
* Capacity to Ship Packages Within D Days
* Allocate Minimum Pages
* Aggressive Cows
* Magnetic Force Between Two Balls

---

## 6. Checklist

Use binary search on answer if:

* [x] You are asked for a **minimum/maximum numeric value**
* [x] The value lies in a **known numeric range**
* [x] You can implement a **check function** that verifies feasibility
* [x] The check result becomes **monotonic** over the range

If all four are true → apply Binary Search on Answer.
