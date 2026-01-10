# BufferedReader & StringTokenizer – Complete Replacement for Scanner

## 1. Why avoid Scanner?

| Reason             | Explanation                  |
| ------------------ | ---------------------------- |
| Slow               | Uses regex & synchronization |
| High overhead      | Poor for large inputs        |
| Contest unfriendly | Causes TLE                   |

**Conclusion:** Use `BufferedReader` instead.

---

## 2. Basic Setup

```java
BufferedReader br = new BufferedReader(
        new InputStreamReader(System.in)
);
```

---

## 3. Reading Different Types of Inputs

---

### A) Reading a single integer

**Input**

```
10
```

**Code**

```java
int n = Integer.parseInt(br.readLine());
```

---

### B) Reading a single string (full line)

**Input**

```
Hello World
```

**Code**

```java
String s = br.readLine();
```

---

### C) Reading int then string

**Input**

```
5
Hemant
```

**Code**

```java
int n = Integer.parseInt(br.readLine());
String name = br.readLine();
```

---

### D) Reading multiple space-separated integers (one line)

**Input**

```
10 20 30 40 50
```

**Code**

```java
StringTokenizer st = new StringTokenizer(br.readLine());

while(st.hasMoreTokens()) {
    int x = Integer.parseInt(st.nextToken());
    System.out.print(x + " ");
}
```

---

### E) Reading fixed count of numbers

**Input**

```
5
1 2 3 4 5
```

**Code**

```java
int n = Integer.parseInt(br.readLine());
int[] arr = new int[n];

StringTokenizer st = new StringTokenizer(br.readLine());

for(int i = 0; i < n; i++)
    arr[i] = Integer.parseInt(st.nextToken());
```

---

### F) Reading int → string → numbers in same test case

**Input**

```
3
Hemant
10 20 30
```

**Code**

```java
int n = Integer.parseInt(br.readLine());
String name = br.readLine();

StringTokenizer st = new StringTokenizer(br.readLine());

for(int i = 0; i < n; i++) {
    int x = Integer.parseInt(st.nextToken());
    System.out.print(x + " ");
}
```

---

### G) Reading multiple test cases

**Input**

```
2
3
1 2 3
2
10 20
```

**Code**

```java
int t = Integer.parseInt(br.readLine());

while(t-- > 0) {
    int n = Integer.parseInt(br.readLine());

    StringTokenizer st = new StringTokenizer(br.readLine());

    for(int i = 0; i < n; i++) {
        int x = Integer.parseInt(st.nextToken());
        System.out.print(x + " ");
    }
    System.out.println();
}
```

---

## 4. Reading Mixed Data Types

**Input**

```
101
Hemant Kumar
99.5
```

**Code**

```java
int id = Integer.parseInt(br.readLine());
String name = br.readLine();
double marks = Double.parseDouble(br.readLine());
```

---

## 5. Important Rules

### 1. BufferedReader returns String

You must manually convert:

```java
Integer.parseInt()
Long.parseLong()
Double.parseDouble()
```

---

### 2. Create new StringTokenizer per line

```java
st = new StringTokenizer(br.readLine());
```

---

### 3. Never mix Scanner and BufferedReader

❌ Wrong

```java
Scanner sc = new Scanner(System.in);
BufferedReader br = new BufferedReader(...);
```

---

### 4. Handle empty lines

```java
String line;
while((line = br.readLine()).isEmpty());
```

---

## 6. Scanner → BufferedReader Mapping

| Scanner    | BufferedReader                  |
| ---------- | ------------------------------- |
| nextInt()  | Integer.parseInt(br.readLine()) |
| next()     | StringTokenizer                 |
| nextLine() | br.readLine()                   |

---

## 7. Fast Contest Template

```java
import java.io.*;
import java.util.*;

class Main {
    public static void main(String[] args) throws Exception {

        BufferedReader br =
            new BufferedReader(
                new InputStreamReader(System.in)
            );

        int t = Integer.parseInt(br.readLine());

        while(t-- > 0) {
            StringTokenizer st =
                new StringTokenizer(br.readLine());

            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());

            System.out.println(a + b);
        }
    }
}
```

---

## 8. Summary

✔ BufferedReader = fast input
✔ StringTokenizer = fast split
✔ Manual parsing required
✔ One tokenizer per line
✔ Ideal for large input