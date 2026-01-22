# Implementing `Math.pow()` in Java

## 1. Using Built-in `Math.pow()`

### Syntax

```java
double result = Math.pow(double base, double exponent);
```

### Example

```java
public class Main {
    public static void main(String[] args) {
        double base = 2;
        double exponent = 3;

        double result = Math.pow(base, exponent);
        System.out.println(result);  // Output: 8.0
    }
}
```

### Key Points

* Returns a `double`
* Supports:

  * Integers
  * Decimals
  * Negative powers

### More Examples

#### Square

```java
Math.pow(5, 2);   // 25.0
```

#### Cube root

```java
Math.pow(27, 1.0/3); // 3.0
```

#### Negative exponent

```java
Math.pow(2, -2); // 0.25
```

---

## 2. Custom Implementation (Without `Math.pow`)

### For Integer Exponent

```java
static double power(double base, int exp) {
    double result = 1;

    for(int i = 0; i < Math.abs(exp); i++) {
        result *= base;
    }

    return exp < 0 ? 1/result : result;
}
```

### Usage

```java
System.out.println(power(2, 3));   // 8.0
System.out.println(power(2, -2));  // 0.25
```

---

## 3. Optimized Fast Power (O(log n))

```java
static double fastPow(double base, int exp) {
    if(exp == 0) return 1;

    double half = fastPow(base, exp/2);

    if(exp % 2 == 0)
        return half * half;
    else
        return exp > 0 ? half * half * base : (half * half) / base;
}
```

---

## 4. When to Use What?

| Use Case        | Method               |
| --------------- | -------------------- |
| General usage   | `Math.pow()`         |
| Interviews / CP | Custom fast power    |
| Large exponent  | Optimized fast power |