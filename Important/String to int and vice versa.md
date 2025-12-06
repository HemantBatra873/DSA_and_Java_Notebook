# Integer ↔ String Conversion in Java

## Very important 

Never use these methods for char to int conversions because chars get promoted to their ASCII values and will lead to wrong int values. '1' will become 49 in int.

## 1. Convert Integer to String

### Method 1: `String.valueOf(int)` (Recommended)

```java
int num = 123;
String s = String.valueOf(num);
```

### Method 2: `Integer.toString(int)`

```java
int num = 123;
String s = Integer.toString(num);
```

### Method 3: Using concatenation (Not recommended)

```java
int num = 123;
String s = num + "";
```

---

## 2. Convert String to Integer

### Method 1: `Integer.parseInt(String)` (Recommended)

```java
String s = "123";
int num = Integer.parseInt(s);
```

### Method 2: `Integer.valueOf(String)`

```java
String s = "123";
int num = Integer.valueOf(s);
```

---

## Summary Table

| Conversion   | Recommended Function       | Notes                                     |
| ------------ | -------------------------- | ----------------------------------------- |
| int → String | `String.valueOf(int)`      | Simple & safe                             |
| String → int | `Integer.parseInt(String)` | Throws `NumberFormatException` if invalid |
