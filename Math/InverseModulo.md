# Modular Inverse

## What is a Modular Inverse?

In normal arithmetic, division is straightforward.

```text
8 / 2 = 4
```

However, in **modular arithmetic**, direct division is **not defined**.

Instead of dividing by a number, we multiply by its **modular inverse**.

For example, suppose we want to compute:

```text
8 / 2 mod 5
```

First, find a number `x` such that:

```text
2 × x ≡ 1 (mod 5)
```

Try different values of `x`:

```text
2 × 1 = 2 mod 5 = 2
2 × 2 = 4 mod 5 = 4
2 × 3 = 6 mod 5 = 1 ✅
```

Therefore,

```text
inverse(2) = 3
```

Now replace division with multiplication.

```text
8 / 2 mod 5
= 8 × inverse(2) mod 5
= 8 × 3 mod 5
= 24 mod 5
= 4
```

---

# Why Can't We Divide in Modular Arithmetic?

Modulo arithmetic supports:

- Addition
- Subtraction
- Multiplication
- Modulo

It **does not** support direct division.

Whenever you see:

```text
a / b mod M
```

convert it into:

```text
a × inverse(b) mod M
```

This is the entire purpose of the modular inverse.

---

# Formal Definition

The modular inverse of `a` modulo `m` is a number `x` such that

```text
a × x ≡ 1 (mod m)
```

Think of it as the modular version of:

```text
a × (1 / a) = 1
```

---

# Example 1

Find the modular inverse of `7` modulo `13`.

We need:

```text
7 × x ≡ 1 (mod 13)
```

Try values:

```text
7 × 1 = 7
7 × 2 = 14 mod 13 = 1 ✅
```

Therefore,

```text
inverse(7) = 2
```

Verification:

```text
7 × 2 = 14

14 mod 13 = 1 ✅
```

---

# Does Every Number Have a Modular Inverse?

**No.**

A modular inverse exists **only if**

```text
gcd(a, m) = 1
```

This means `a` and `m` must be **coprime**.

---

## Example (Inverse Exists)

Find the inverse of `3 mod 7`.

```text
3 × 1 = 3
3 × 2 = 6
3 × 3 = 9 mod 7 = 2
3 × 4 = 12 mod 7 = 5
3 × 5 = 15 mod 7 = 1 ✅
```

Therefore,

```text
inverse(3) = 5
```

---

## Example (Inverse Does Not Exist)

Find the inverse of `2 mod 8`.

```text
2 × 1 = 2
2 × 2 = 4
2 × 3 = 6
2 × 4 = 8 mod 8 = 0
2 × 5 = 10 mod 8 = 2
```

The pattern repeats.

We'll never get `1`.

Why?

```text
gcd(2, 8) = 2 ≠ 1
```

Therefore,

```text
2 has no modular inverse modulo 8.
```

---

# Computing Division Using a Modular Inverse

Suppose we want:

```text
15 / 3 mod 11
```

### Step 1

Find the inverse of `3`.

```text
3 × 4 = 12 mod 11 = 1
```

So,

```text
inverse(3) = 4
```

### Step 2

Replace division.

```text
15 × 4 mod 11

= 60 mod 11

= 5
```

Answer:

```text
15 / 3 mod 11 = 5
```

---

# How to Compute a Modular Inverse

## Method 1 — Fermat's Little Theorem

This works **only when the modulus is prime**.

Common prime moduli:

```text
1,000,000,007
998,244,353
```

Formula:

```text
inverse(a) = a^(mod - 2) mod mod
```

Example:

```java
long inverse = power(a, mod - 2);
```

where `power()` is Binary Exponentiation.

### Time Complexity

```text
O(log M)
```

---

## Why Does Fermat's Formula Work?

Fermat's Little Theorem states:

```text
a^(mod - 1) ≡ 1 (mod mod)
```

Divide both sides by `a` (using modular inverse):

```text
a^(mod - 2) ≡ inverse(a)
```

Therefore,

```text
inverse(a) = a^(mod - 2) mod mod
```

---

## Method 2 — Extended Euclidean Algorithm

Works whenever

```text
gcd(a, m) = 1
```

even if the modulus is **not prime**.

### Time Complexity

```text
O(log M)
```

---

# Where Is Modular Inverse Used?

## 1. Computing nCr

Normally,

```text
nCr = n! / (r! × (n-r)!)
```

Under modulo, division isn't allowed.

Instead compute:

```text
n!
× inverse(r!)
× inverse((n-r)!)
```

This is the most common application.

---

## 2. Probability Problems

Expressions like

```text
5 / 7 mod M
```

become

```text
5 × inverse(7)
```

---

## 3. Number Theory

Used in:

- Modular equations
- Congruences
- Euler Totient problems
- Chinese Remainder Theorem

---

## 4. Polynomial Hashing

Rolling hash algorithms often need to divide by powers of the base.

They use modular inverses instead.

---

## 5. Matrix Operations

Matrix inversion over finite fields requires modular inverses.

---

# Is It Common in DSA?

## Software Engineering Interviews

Usually **not asked directly**.

Higher-priority topics include:

- Arrays
- Strings
- Linked Lists
- Trees
- Graphs
- Dynamic Programming
- Binary Search
- Greedy
- Heaps
- Tries

However, understanding modular inverses is useful for problems involving modular arithmetic.

---

## Competitive Programming

Yes.

It appears frequently in:

- Number Theory
- Combinatorics
- Probability
- Hashing
- Advanced Mathematics

---

# Time Complexities

| Method | Time Complexity | Works When |
|----------|----------------|------------|
| Brute Force | O(M) | Small modulus only |
| Fermat's Little Theorem | O(log M) | Modulus is prime |
| Extended Euclidean Algorithm | O(log M) | gcd(a, m) = 1 |

---

# Quick Revision

- Division is **not defined** in modular arithmetic.

- Replace

```text
a / b mod M
```

with

```text
a × inverse(b) mod M
```

- The modular inverse of `a` is a number `x` such that

```text
a × x ≡ 1 (mod m)
```

- A modular inverse exists **only if**

```text
gcd(a, m) = 1
```

- Two standard methods:

  - Fermat's Little Theorem (prime modulus)
  - Extended Euclidean Algorithm (general modulus)

- Most common use:

```text
Computing nCr modulo a prime.
```

---

# Interview Tips

If the modulus is prime:

```text
Think: Fermat's Little Theorem
```

If the modulus is not prime:

```text
Think: Extended Euclidean Algorithm
```

Whenever you see:

```text
a / b mod M
```

immediately think:

```text
a × inverse(b) mod M
```

Remember the most important formula:

```text
inverse(a) = a^(mod - 2) mod mod
```

(Only when the modulus is prime.)
