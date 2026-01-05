# Java IO

https://www.geeksforgeeks.org/java/java-io-input-output-in-java-with-examples/

# Java Scanner & System.out for DSA (In Depth)

## 1. Scanner Basics (What Actually Happens)

```java
Scanner sc = new Scanner(System.in);
```

Internally, `Scanner`:

* Reads from `InputStream` (`System.in`)
* Uses **regular expressions** for tokenization
* Is **locale-aware** (important for decimal parsing)

This is why Scanner is **slow but convenient**.

---

## 2. Most Used Scanner Methods (DSA)

### 2.1 `nextInt()`

```java
int x = sc.nextInt();
```

**Behavior**

* Skips leading whitespace
* Reads digits until non-digit
* Leaves the **newline (\n)** in buffer

**Common Mistake (CRITICAL)**

```java
int x = sc.nextInt();
String s = sc.nextLine(); // s == ""
```

**Why?**

* `nextInt()` does NOT consume `\n`
* `nextLine()` immediately reads that leftover newline

**Correct Pattern**

```java
int x = sc.nextInt();
sc.nextLine(); // consume newline
String s = sc.nextLine();
```

---

### 2.2 `next()` vs `nextLine()` (VERY IMPORTANT)

```java
String a = sc.next();     // token-based
String b = sc.nextLine(); // line-based
```

| Method       | Reads        | Stops At   |
| ------------ | ------------ | ---------- |
| `next()`     | Single token | Whitespace |
| `nextLine()` | Full line    | Newline    |

**DSA Rule of Thumb**

* Use `next()` for words
* Use `nextLine()` for sentences / full lines

---

### 2.3 `nextLong()`, `nextDouble()`

```java
long n = sc.nextLong();
double d = sc.nextDouble();
```

**Traps**

* `InputMismatchException` if input exceeds range
* Locale issues with decimal separators

**Safe Competitive Pattern**

```java
long n = Long.parseLong(sc.next());
```

---

## 3. Scanner Edge Cases That Cause WA / RE

### 3.1 Empty Input Line Issues

```java
String s = sc.nextLine();
```

Fails when:

* Previous call was `nextInt()` / `next()`

Always mentally track:

> "Did I leave a newline behind?"

---

### 3.2 Reading Arrays Using Scanner

```java
int n = sc.nextInt();
int[] arr = new int[n];
for (int i = 0; i < n; i++) {
    arr[i] = sc.nextInt();
}
```

**Mistake**

* Forgetting input size
* Assuming input is line-based

---

### 3.3 Multiple Test Cases Pattern

```java
int t = sc.nextInt();
while (t-- > 0) {
    int n = sc.nextInt();
}
```

**Common Bug**

* Mixing `nextLine()` inside loop without cleanup

---

## 4. Scanner Performance Reality (Important for DSA)

| Input Size | Scanner    |
| ---------- | ---------- |
| ≤ 10^4     | OK         |
| 10^5       | Risky      |
| ≥ 10^6     | TLE likely |

**Why?**

* Regex parsing
* Synchronization overhead

This is why competitive programmers switch to `BufferedReader`.

---

## 5. System.out Output Methods (DSA Focus)

### 5.1 `print()` vs `println()`

```java
System.out.print(x);
System.out.println(x);
```

| Method    | Newline |
| --------- | ------- |
| `print`   | ❌       |
| `println` | ✅       |

---

### 5.2 `printf()`

```java
System.out.printf("%d %s", x, s);
```

**DSA Warning**

* Slower than `print/println`
* Avoid inside large loops

---

## 6. Output Performance Trap (VERY COMMON)

❌ Bad

```java
for (int i = 0; i < n; i++) {
    System.out.println(arr[i]);
}
```

✅ Good

```java
StringBuilder sb = new StringBuilder();
for (int i = 0; i < n; i++) {
    sb.append(arr[i]).append('\n');
}
System.out.print(sb.toString());
```

**Reason**

* Each `println` flushes internally
* `StringBuilder` minimizes I/O calls

---

## 7. Mixing Scanner Input & Output (Safe Patterns)

### 7.1 Read → Compute → Print

```java
int a = sc.nextInt();
int b = sc.nextInt();
System.out.println(a + b);
```

Safe because:

* No line-based input

---

### 7.2 Line-Based Input + Output

```java
String s = sc.nextLine();
System.out.println(s);
```

Fails only if previous token-based input exists.

---

## 8. Interview-Trap Scanner Questions

### Q1: Why is Scanner slow?

* Uses regex
* Performs type validation
* Locale checks

### Q2: Why does `nextLine()` return empty?

* Leftover newline in buffer

### Q3: Is closing Scanner necessary?

* Yes in real apps
* Often skipped in CP to avoid closing `System.in`

---

## 9. Golden Rules for DSA Using Scanner

1. Never mix `nextInt()` and `nextLine()` blindly
2. Always consume newline when switching modes
3. Use `StringBuilder` for output
4. Avoid `printf()` in loops
5. Scanner is OK only for **small to medium input**

---

## 10. Minimal Safe DSA Template (Scanner Based)

```java
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();
StringBuilder sb = new StringBuilder();
for (int i = 0; i < n; i++) {
    int x = sc.nextInt();
    sb.append(x).append('\n');
}
System.out.print(sb.toString());
```
