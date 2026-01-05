# Can we use `nextInt()` directly after `nextInt()`?

## Short answer

* **`nextInt()` → `nextInt()`** ✅ **Yes**, you can use it directly.
* **`nextInt()` → `nextLine()`** ❌ **No**, you must consume the leftover newline first.

---

## Case 1: `nextInt()` followed by `nextInt()`

```java
Scanner sc = new Scanner(System.in);

int a = sc.nextInt();
int b = sc.nextInt();
```

### Why this works

* `nextInt()` reads only the integer token.
* It skips leading whitespace automatically.
* The remaining newline (`\n`) does **not** affect another `nextInt()`.

No extra handling is needed.

---

## Case 2: `nextInt()` followed by `nextLine()` (IMPORTANT)

```java
Scanner sc = new Scanner(System.in);

int a = sc.nextInt();
sc.nextLine();          // consume leftover newline
String s = sc.nextLine();
```

### Why this is required

* `nextInt()` **does not consume** the newline after the number.
* `nextLine()` reads input **until it hits a newline**.
* Without the extra `nextLine()`, it immediately reads the leftover newline and returns an empty string.

---

## Common beginner bug

```java
int n = sc.nextInt();
String name = sc.nextLine(); // name becomes ""
```

### Correct version

```java
int n = sc.nextInt();
sc.nextLine();
String name = sc.nextLine();
```

---

## Scanner behavior summary (very important for DSA)

| Method       | Reads                   | Consumes newline |
| ------------ | ----------------------- | ---------------- |
| `nextInt()`  | Integer token           | ❌ No             |
| `next()`     | Single word token       | ❌ No             |
| `nextLine()` | Entire line (till `\n`) | ✅ Yes            |

---

## Golden rules to remember (exam & interview safe)

1. **Number → Number**

   * `nextInt()` → `nextInt()` ✅ No issue

2. **Number → Line/String**

   * Always add one `nextLine()` to flush the newline

3. **Only line-based input**

   * Use only `nextLine()` consistently

---

## DSA input tip

For competitive programming and large inputs:

* Prefer **`BufferedReader` + `StringTokenizer`** for speed
* Use `Scanner` only for small inputs or practice

---

### One-line takeaway

> Use `nextLine()` **only when switching from token-based input to line-based input**.
