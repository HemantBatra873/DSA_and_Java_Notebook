# Regular Expressions (Regex) in Java for DSA & Interviews

## What is Regex?

Regular Expressions (Regex) are patterns used to search, validate, extract, split, and replace text.

In DSA and coding interviews, regex is most useful for:

- String validation
- Input parsing
- Data extraction
- String cleanup
- Tokenization

For most algorithmic problems, techniques like Two Pointers, Sliding Window, Hashing, KMP, Z-Function, Trie, and Dynamic Programming are usually preferred over regex.

---

# Java Regex Classes

Java provides:

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;
```

You can also use regex directly through String methods:

```java
matches()
split()
replaceAll()
replaceFirst()
```

---

# Common Regex Symbols

| Regex | Meaning | Example |
|---------|---------|---------|
| `.` | Any character | `a.c` |
| `*` | Zero or more | `ab*c` |
| `+` | One or more | `ab+c` |
| `?` | Zero or one | `colou?r` |
| `^` | Start of string | `^abc` |
| `$` | End of string | `abc$` |
| `[]` | Character set | `[abc]` |
| `[^]` | Negated set | `[^abc]` |
| `()` | Grouping | `(abc)+` |
| `|` | OR | `cat|dog` |
| `\\` | Escape character | `\\.` |

---

# Character Classes

## Digits

```regex
\d
```

Equivalent:

```regex
[0-9]
```

Example:

```java
"123".matches("\\d+");
```

Output:

```text
true
```

---

## Non-Digits

```regex
\D
```

---

## Word Characters

```regex
\w
```

Matches:

```text
a-z
A-Z
0-9
_
```

---

## Non-Word Characters

```regex
\W
```

---

## Whitespace

```regex
\s
```

Matches:

```text
Space
Tab
Newline
```

---

## Non-Whitespace

```regex
\S
```

---

# Quantifiers

## Exactly n Times

```regex
a{3}
```

Matches:

```text
aaa
```

---

## Between m and n Times

```regex
a{2,5}
```

---

## At Least n Times

```regex
a{2,}
```

---

# String.matches()

```java
String value = "12345";

boolean result = value.matches("\\d+");
```

Output:

```text
true
```

Important: `matches()` checks the entire string.

```java
"abc123".matches("\\d+");
```

Output:

```text
false
```

---

# Splitting Strings

```java
String[] words = text.split(" ");
```

Multiple spaces:

```java
String[] words = text.trim().split("\\s+");
```

---

# Replacing Text

Remove digits:

```java
text.replaceAll("\\d", "");
```

Keep only digits:

```java
text.replaceAll("\\D", "");
```

Remove special characters:

```java
text.replaceAll("[^a-zA-Z0-9]", "");
```

---

# Pattern and Matcher

```java
Pattern pattern = Pattern.compile("\\d+");
Matcher matcher = pattern.matcher("ab123cd45");

while (matcher.find()) {
    System.out.println(matcher.group());
}
```

Output:

```text
123
45
```

---

# Useful Matcher Methods

```java
matcher.find();   // Find next occurrence
matcher.group();  // Get matched text
matcher.start();  // Starting index
matcher.end();    // Ending index + 1
```

---

# Count Occurrences of a Pattern

```java
Pattern pattern = Pattern.compile("abc");
Matcher matcher = pattern.matcher(text);

int count = 0;

while (matcher.find()) {
    count++;
}
```

---

# Extract Numbers from a String

Input:

```text
abc12xy34z5
```

Solution:

```java
Pattern pattern = Pattern.compile("\\d+");
Matcher matcher = pattern.matcher(input);

while (matcher.find()) {
    System.out.println(matcher.group());
}
```

Output:

```text
12
34
5
```

---

# Email Validation

```java
String regex =
    "^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+$";
```

Usage:

```java
email.matches(regex);
```

---

# Phone Number Validation

Exactly 10 digits:

```java
phone.matches("\\d{10}");
```

---

# Alphanumeric Validation

```java
text.matches("[a-zA-Z0-9]+");
```

---

# Consecutive Repeated Characters

Input:

```text
aaabbcc
```

Regex:

```regex
(.)\1+
```

Explanation:

```text
(.)   Capture a character
\1    Same character again
+     One or more times
```

Matches:

```text
aaa
bb
cc
```

---

# Capturing Groups

Regex:

```regex
(\d+)-(\d+)
```

Input:

```text
123-456
```

Code:

```java
Matcher matcher =
    Pattern.compile("(\\d+)-(\\d+)")
           .matcher("123-456");

if (matcher.find()) {
    System.out.println(matcher.group(1));
    System.out.println(matcher.group(2));
}
```

Output:

```text
123
456
```

---

# Lookahead (Advanced)

Match digits followed by letters.

```regex
\d+(?=[a-zA-Z])
```

Input:

```text
123abc
```

Match:

```text
123
```

---

# Lookbehind (Advanced)

```regex
(?<=#)\w+
```

Input:

```text
#java #dsa
```

Matches:

```text
java
dsa
```

---

# Frequently Used DSA Regex Patterns

| Task | Regex |
|--------|--------|
| Digits Only | `\\d+` |
| Letters Only | `[a-zA-Z]+` |
| Alphanumeric | `[a-zA-Z0-9]+` |
| Extract Numbers | `\\d+` |
| Extract Words | `[a-zA-Z]+` |
| Remove Spaces | `\\s+` |
| Hex Number | `[0-9a-fA-F]+` |
| Binary String | `[01]+` |

---

# Regex Cheat Sheet

```text
.       Any character
\d      Digit
\D      Non-digit
\w      Word character
\W      Non-word character
\s      Whitespace
\S      Non-whitespace

*       0 or more
+       1 or more
?       0 or 1

{n}     Exactly n
{m,n}   Between m and n
{n,}    At least n

^       Start of string
$       End of string

[]      Character set
[^]     Negated set

()      Grouping
|       OR
```

---

# Interview Advice

Use Regex For:

- Validation
- Parsing
- Data extraction
- String cleanup
- Log processing

Avoid Regex For:

- KMP-style searching
- Z-Function problems
- Performance-critical string matching

Master:

- matches()
- split()
- replaceAll()
- Pattern
- Matcher
- Capturing Groups
- Backreferences
- Lookahead
- Lookbehind