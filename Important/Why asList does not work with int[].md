# Why `Arrays.asList()` Does Not Work With `int[]`

## 1. Works fine with `Integer[]`

```java
Integer[] arr = {1, 2, 3};
Arrays.asList(arr); // → List<Integer> = [1, 2, 3]
```

This works because `Integer` is an object type, so each element is treated as an individual item.

---

## 2. Fails with `int[]`

```java
int[] arr = {1, 2, 3};
Arrays.asList(arr); // → List<int[]> size = 1
```

The entire primitive array becomes **one single element** in the resulting list.

### Why?

`Arrays.asList()` is defined as:

```java
public static <T> List<T> asList(T... a)
```

* `int[]` is **not** an array of objects.
* `int` is primitive, so auto-boxing does not expand the elements.
* `int[]` is treated as a single object of type `T`.

Thus:

```
asList(int[]) → List<int[]> with 1 element
```

---

## 3. Converting `int[]` properly

### **Option 1: Streams + boxed()**

```java
int[] arr = {1, 2, 3};
List<Integer> list = Arrays.stream(arr)
                           .boxed()
                           .toList();
```

---

### **Option 2: Manual conversion**

```java
int[] arr = {1, 2, 3};
List<Integer> list = new ArrayList<>();
for (int x : arr) list.add(x);
```

---

## 4. Summary

| Array Type  | Works With `asList()`? | Result                                             |
| ----------- | ---------------------- | -------------------------------------------------- |
| `Integer[]` | ✔ Yes                  | List of individual elements                        |
| `int[]`     | ❌ No                   | List containing **one element** (the array itself) |
