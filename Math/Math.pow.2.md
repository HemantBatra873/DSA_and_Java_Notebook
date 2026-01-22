# Binary Exponentiation in Java (Power Function)

---

## 1. Original Code

```java
private static int Power(int n){
    int ans = 1, x = 2;
    while(n != 0){
        if(n % 2 == 1){
            ans = ans * x;
        }
        x *= x;
        n = n >> 1;
    }
    return ans;
}
```

This function computes:

```
2^n
```

It uses **Binary Exponentiation** (also called fast exponentiation).

---

## 2. How It Works

The idea is based on:

```
a^n = (a^(n/2))^2        if n is even
a^n = a * a^(n-1)       if n is odd
```

Instead of recursion, this code uses an **iterative bit-based method**.

### Variable Meaning

| Variable | Purpose                          |
| -------- | -------------------------------- |
| `ans`    | Stores final result              |
| `x`      | Current base value (starts at 2) |
| `n`      | Exponent                         |

### Loop Explanation

| Statement        | Role                       |
| ---------------- | -------------------------- |
| `if(n % 2 == 1)` | Checks if current bit is 1 |
| `ans *= x`       | Multiply result            |
| `x *= x`         | Square base                |
| `n >>= 1`        | Right shift (n = n/2)      |

### Example: n = 5

Binary of 5 = `101`

| Step | n | x  | ans    |
| ---- | - | -- | ------ |
| 1    | 5 | 2  | 1 → 2  |
| 2    | 2 | 4  | 2      |
| 3    | 1 | 16 | 2 → 32 |
| End  | 0 | -  | 32     |

Result = `2^5 = 32`

---

## 3. General Implementation (Any Base)

```java
static long power(long x, long n) {
    long ans = 1;

    while(n > 0) {
        if((n & 1) == 1) {
            ans *= x;
        }
        x *= x;
        n >>= 1;
    }
    return ans;
}
```

* Works for any base `x`
* Time complexity: **O(log n)**

---

## 4. Recursive Version

```java
static long power(long x, long n) {
    if(n == 0) return 1;

    long half = power(x, n/2);

    if(n % 2 == 0)
        return half * half;
    else
        return x * half * half;
}
```

---

## 5. Modulo Power (Competitive Programming)

```java
static long power(long x, long n, long mod) {
    long ans = 1;
    x %= mod;

    while(n > 0) {
        if((n & 1) == 1)
            ans = (ans * x) % mod;

        x = (x * x) % mod;
        n >>= 1;
    }
    return ans;
}
```

Used when numbers become very large.

---

## 6. When to Use This vs Math.pow()

| Scenario                | Prefer                |
| ----------------------- | --------------------- |
| Competitive programming | Binary exponentiation |
| Large exponents         | Binary exponentiation |
| Modulo calculations     | Binary exponentiation |
| Floating-point powers   | Math.pow()            |
| Simple programs         | Math.pow()            |

### Why not Math.pow()?

* Uses `double`
* Precision errors
* Slower
* Requires type casting

Example:

```java
(int)Math.pow(2, 50)   // Incorrect
```

---

## 7. Usage in Your Code

```java
System.out.println(Codechef.Power(cnt) - 1);
```

This computes:

```
2^cnt - 1
```

Commonly used to count **non-empty subsets**.

---

## Conclusion

Binary exponentiation is:

* Faster
* More accurate
* More controllable than Math.pow()

Highly recommended for:

* Algorithm problems
* Large exponent calculations
* Modular arithmetic
