# GCD (Greatest Common Divisor) in Java

---

## 1. What is GCD?

GCD (Greatest Common Divisor) is the **largest positive integer** that divides two or more numbers without leaving a remainder.

Example:

* GCD(36, 60) = 12

---

## 2. Euclid’s Algorithm (Core Idea)

Formula:

```
gcd(a, b) = gcd(b, a % b)
```

Base case:

```
gcd(a, 0) = a
```

---

## 3. Important Rule

> **It is NOT compulsory that a should be smaller than b.**

You can pass numbers in **any order**.

Why?

* If `a < b`, then `a % b = a`
* Algorithm automatically swaps values

So order does **not matter**.

---

## 4. GCD of Two Numbers (Java)

### Iterative version

```java
static int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}
```

### Recursive version

```java
static int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}
```

---

## 5. Order Does NOT Matter (Example)

### Case 1: a > b

```
gcd(60, 36)
→ gcd(36, 24)
→ gcd(24, 12)
→ gcd(12, 0)
= 12
```

### Case 2: a < b

```
gcd(36, 60)
→ gcd(60, 36)
→ gcd(36, 24)
→ gcd(24, 12)
→ gcd(12, 0)
= 12
```

Both give same result.

---

## 6. GCD of Multiple Numbers

Use pairwise reduction:

```
gcd(a, b, c) = gcd(gcd(a, b), c)
```

### Java Implementation

```java
static int gcd(int a, int b) {
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

static int gcdOfArray(int[] arr) {
    int result = arr[0];

    for (int i = 1; i < arr.length; i++) {
        result = gcd(result, arr[i]);
    }

    return result;
}
```

---

## 7. Built-in Method (Java 18+)

```java
int result = Math.gcd(36, 60);
```

---

## 8. Time Complexity

Euclid’s Algorithm runs in:

```
O(log(min(a, b)))
```

Very efficient.

---

## Edge Cases

* gcd(a, 0) = a
* gcd(0, b) = b
* gcd(0, 0) is undefined
