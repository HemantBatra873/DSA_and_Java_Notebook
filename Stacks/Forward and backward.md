## Two different patterns of finding Next Greater/Smaller

1. **Backward checking (standard)** — we move from the end toward the start (right → left) and directly find the next element for each bar.
2. **Forward checking (builder)** — we move from start → end and for each new element, we pop from stack to resolve all the elements whose "next" we’ve just found.

So there are effectively **8 total implementations** (2 per concept × 4 base types).

---

## 🌟 1️⃣ Next Greater to Right (NGR)

### ➤ **Right → Left (Common)**

```java
public static int[] nextGreaterToRight1(int[] arr) {
    int n = arr.length;
    int[] res = new int[n];
    Stack<Integer> st = new Stack<>();

    for (int i = n - 1; i >= 0; i--) {
        while (!st.isEmpty() && arr[st.peek()] <= arr[i]) st.pop();
        res[i] = st.isEmpty() ? -1 : arr[st.peek()];
        st.push(i);
    }
    return res;
}
```

### ➤ **Left → Right (Alternative)**

```java
public static int[] nextGreaterToRight2(int[] arr) {
    int n = arr.length;
    int[] res = new int[n];
    Arrays.fill(res, -1);
    Stack<Integer> st = new Stack<>();

    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && arr[i] > arr[st.peek()]) {
            res[st.pop()] = arr[i];
        }
        st.push(i);
    }
    return res;
}
```

---

## 🌟 2️⃣ Next Smaller to Right (NSR)

### ➤ **Right → Left (Common)**

```java
public static int[] nextSmallerToRight1(int[] arr) {
    int n = arr.length;
    int[] res = new int[n];
    Stack<Integer> st = new Stack<>();

    for (int i = n - 1; i >= 0; i--) {
        while (!st.isEmpty() && arr[st.peek()] >= arr[i]) st.pop();
        res[i] = st.isEmpty() ? -1 : arr[st.peek()];
        st.push(i);
    }
    return res;
}
```

### ➤ **Left → Right (Alternative)**

```java
public static int[] nextSmallerToRight2(int[] arr) {
    int n = arr.length;
    int[] res = new int[n];
    Arrays.fill(res, -1);
    Stack<Integer> st = new Stack<>();

    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && arr[i] < arr[st.peek()]) {
            res[st.pop()] = arr[i];
        }
        st.push(i);
    }
    return res;
}
```

---

## 🌟 3️⃣ Next Greater to Left (NGL)

### ➤ **Left → Right (Common)**

```java
public static int[] nextGreaterToLeft1(int[] arr) {
    int n = arr.length;
    int[] res = new int[n];
    Stack<Integer> st = new Stack<>();

    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && arr[st.peek()] <= arr[i]) st.pop();
        res[i] = st.isEmpty() ? -1 : arr[st.peek()];
        st.push(i);
    }
    return res;
}
```

### ➤ **Right → Left (Alternative)**

```java
public static int[] nextGreaterToLeft2(int[] arr) {
    int n = arr.length;
    int[] res = new int[n];
    Arrays.fill(res, -1);
    Stack<Integer> st = new Stack<>();

    for (int i = n - 1; i >= 0; i--) {
        while (!st.isEmpty() && arr[i] > arr[st.peek()]) {
            res[st.pop()] = arr[i];
        }
        st.push(i);
    }
    return res;
}
```

---

## 🌟 4️⃣ Next Smaller to Left (NSL)

### ➤ **Left → Right (Common)**

```java
public static int[] nextSmallerToLeft1(int[] arr) {
    int n = arr.length;
    int[] res = new int[n];
    Stack<Integer> st = new Stack<>();

    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && arr[st.peek()] >= arr[i]) st.pop();
        res[i] = st.isEmpty() ? -1 : arr[st.peek()];
        st.push(i);
    }
    return res;
}
```

### ➤ **Right → Left (Alternative)**

```java
public static int[] nextSmallerToLeft2(int[] arr) {
    int n = arr.length;
    int[] res = new int[n];
    Arrays.fill(res, -1);
    Stack<Integer> st = new Stack<>();

    for (int i = n - 1; i >= 0; i--) {
        while (!st.isEmpty() && arr[i] < arr[st.peek()]) {
            res[st.pop()] = arr[i];
        }
        st.push(i);
    }
    return res;
}
```

---

## 🧠 Summary Table (Final)

| Type                         | Direction 1  | Direction 2  | Condition |
| ---------------------------- | ------------ | ------------ | --------- |
| **Next Greater Right (NGR)** | Right → Left | Left → Right | `>`       |
| **Next Smaller Right (NSR)** | Right → Left | Left → Right | `<`       |
| **Next Greater Left (NGL)**  | Left → Right | Right → Left | `>`       |
| **Next Smaller Left (NSL)**  | Left → Right | Right → Left | `<`       |

---

## 🧩 Key Difference Between the Two Methods

| Style            | Direction | Who Gets Their Answer                       | When Do We Pop                |
| ---------------- | --------- | ------------------------------------------- | ----------------------------- |
| **Right → Left** | Backward  | Current element finds its “next”            | Pop until stack top > current |
| **Left → Right** | Forward   | Popped elements get their “next” as current | Pop until current > top       |
