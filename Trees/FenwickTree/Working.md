A Fenwick Tree (also called a **Binary Indexed Tree / BIT**) is basically a clever data structure for answering:

> **"What is the sum of elements from 1 to X?"**

while also allowing you to **change an element** quickly.

The easiest way to understand it is by comparing it with a normal array.

### 1. The problem

Suppose we have:

```text
Index:  1  2  3  4  5  6  7  8
Value:  2  1  5  3  7  4  6  2
```

If I ask:

> What is the sum from index `1` to `6`?

You could calculate:

```text
2 + 1 + 5 + 3 + 7 + 4 = 22
```

That's **O(N)**.

If I ask this thousands of times, that's expensive.

---

### 2. What if we store partial sums?

A Fenwick Tree doesn't store every possible range.

Instead, it cleverly stores certain **groups of consecutive elements**:

```text
Index:       1   2   3   4   5   6   7   8

Values:      2   1   5   3   7   4   6   2

Fenwick:
             2   3   5  11   7  11   6  30
```

The important thing is what each position represents.

For example:

```text
BIT[4] = 11
```

represents:

```text
values[1] + values[2] + values[3] + values[4]

= 2 + 1 + 5 + 3
= 11
```

But:

```text
BIT[6] = 11
```

represents only:

```text
values[5] + values[6]

= 7 + 4
= 11
```

And:

```text
BIT[8] = 30
```

represents:

```text
values[1] ... values[8]
```

The groups are determined by a neat property of binary numbers.

---

### 3. The key trick

Look at the binary representation of an index:

```text
1 = 0001
2 = 0010
3 = 0011
4 = 0100
5 = 0101
6 = 0110
7 = 0111
8 = 1000
```

Fenwick Tree uses the **lowest set bit**.

For example:

```text
4 = 0100
```

The lowest set bit is:

```text
0100
  ↑
  4
```

So `BIT[4]` covers **4 elements**:

```text
[1, 2, 3, 4]
```

For `6`:

```text
6 = 0110
       ↑
       2
```

So `BIT[6]` covers **2 elements**:

```text
[5, 6]
```

For `8`:

```text
8 = 1000
      ↑
      8
```

So it covers:

```text
[1,2,3,4,5,6,7,8]
```

That's the fundamental idea behind a Fenwick Tree.

---

## 4. How does it get a prefix sum so quickly?

Suppose we want:

```text
sum(1 ... 7)
```

Instead of adding 7 elements, Fenwick breaks it into chunks.

Start at `7`:

```text
7 = 0111
```

`BIT[7]` gives us:

```text
[7]
```

Then we move to:

```text
7 - lowestBit(7)
```

which gives:

```text
6
```

`BIT[6]` gives:

```text
[5, 6]
```

Then:

```text
6 - lowestBit(6)
= 6 - 2
= 4
```

`BIT[4]` gives:

```text
[1, 2, 3, 4]
```

So we have:

```text
[1 2 3 4] + [5 6] + [7]
```

That's the entire range:

```text
1 ---------------------- 7
|------|----|-----------|
   4     2       1
```

Only **3 additions** instead of 7.

For a million elements, you need roughly **log₂(N)** operations.

---

## 5. What about updating a value?

Suppose:

```text
index 3
```

changes by `+5`.

A normal prefix-sum array would potentially require updating many values.

Fenwick Tree updates only the relevant chunks.

The code:

```java
index += index & -index;
```

moves through the Fenwick nodes that contain that index.

For index `3`:

```text
3 → 4 → 8 → ...
```

So only a few nodes need updating.

That's also:

```text
O(log N)
```

---

## 6. So what does a Fenwick Tree actually give you?

It gives you this combination:

| Operation          | Normal Array |                       Fenwick Tree |
| ------------------ | -----------: | ---------------------------------: |
| Get value at index |         O(1) | O(log N) / can maintain separately |
| Update one value   |         O(1) |                           O(log N) |
| Prefix sum         |         O(N) |                       **O(log N)** |
| Range sum          |         O(N) |                       **O(log N)** |

The important use case is:

> **I repeatedly modify individual elements AND repeatedly ask for sums over ranges.**

---

### The mental model I'd recommend

Don't initially think:

> "Fenwick Tree is some complicated binary tree."

It isn't really a tree that you visualize like a segment tree.

Think of it as:

> **An array containing carefully chosen partial sums, where binary arithmetic tells us which partial sums to combine.**

The two lines that make the whole thing work are:

```java
index += index & -index;  // move upward during update
```

and

```java
index -= index & -index;  // move backward during query
```

Once you understand **why `index & -index` tells us the size of the chunk**, Fenwick Trees become much less mysterious.
