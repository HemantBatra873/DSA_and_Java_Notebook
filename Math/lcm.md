# LCM (Least Common Multiple) in Java

---

## 1. Mathematical Formula

For two numbers:

```
LCM(a, b) = |a × b| / GCD(a, b)
```

We use **GCD (Greatest Common Divisor)** to compute LCM efficiently.

---

## 2. Optimized Approach

### Key Optimizations

* Iterative **Euclidean Algorithm** (no recursion)
* Uses `long` to prevent overflow
* Prevents multiplication overflow using `(a / gcd) * b`
* Early exit when result becomes `0`

---

## 3. Optimized LCM for Two Numbers

```java
class OptimizedLCM {

    static long gcd(long a, long b) {
        while (b != 0) {
            long temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    static long lcm(long a, long b) {
        if (a == 0 || b == 0) return 0;
        return Math.abs(a / gcd(a, b) * b);
    }

    public static void main(String[] args) {
        System.out.println(lcm(12, 18)); // Output: 36
    }
}
```

---

## 4. Optimized LCM for Multiple Numbers

We apply pairwise reduction:

```
LCM(a, b, c) = LCM(LCM(a, b), c)
```

```java
class OptimizedLCMMultiple {

    static long gcd(long a, long b) {
        while (b != 0) {
            long temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    static long lcm(long a, long b) {
        if (a == 0 || b == 0) return 0;
        return Math.abs(a / gcd(a, b) * b);
    }

    static long lcmArray(int[] arr) {
        long result = arr[0];

        for (int i = 1; i < arr.length; i++) {
            result = lcm(result, arr[i]);
            if (result == 0) return 0;
        }
        return result;
    }

    public static void main(String[] args) {
        int[] nums = {4, 6, 8};
        System.out.println(lcmArray(nums)); // Output: 24
    }
}
```

---

## 5. Time Complexity

```
O(n log M)
```

Where:

* `n` = count of numbers
* `M` = maximum value
