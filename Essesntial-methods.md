# Essential Methods of Common Java Data Structures and Types

This document provides a detailed overview of crucial methods for fundamental Java data structures and types. Time complexities are approximate and refer to common Java Development Kit (JDK) implementations.

---

## 1. Primitive Arrays (e.g., `int[]`, `String[]`)

Arrays are fixed-size, sequential collections of elements of the same data type.

| Method/Concept     | Description                                                                 | Time Complexity (Typical) | Notes                                                            |
| :----------------- | :-------------------------------------------------------------------------- | :------------------------ | :--------------------------------------------------------------- |
| `declaration`      | Declaring an array variable (e.g., `int[] numbers;`).                      | O(1)                      |                                                                  |
| `initialization`   | Creating an array instance with a specified size or initial values.         | O(N) (N is array size)    | `int[] arr = new int[5];` or `String[] names = {"Alice", "Bob"};` |
| `arr[index]`       | **Accessing/Modifying:** Retrieving or setting an element at a specific index. | O(1)                      | Throws `ArrayIndexOutOfBoundsException` if `index` is invalid.     |
| `arr.length`       | Getting the fixed size of the array.                                        | O(1)                      | This is a field, not a method.                                   |
| `new Type[size]`   | Creation of a new array of a specified type and size.                       | O(size)                   | Memory allocation.                                               |

---

## 2. `java.util.Arrays` (Utility Class for Array Operations)

This class provides static methods for common operations on arrays, such as sorting and searching.

| Method                       | Description                                                                                               | Time Complexity (Typical)     | Notes                                                            |
| :--------------------------- | :-------------------------------------------------------------------------------------------------------- | :---------------------------- | :--------------------------------------------------------------- |
| `sort(array)`                | Sorts the specified array into ascending order. Overloaded for all primitive types and `Object[]`.        | O(N log N)                    | Uses Dual-Pivot Quicksort for primitives, Timsort for objects.   |
| `binarySearch(array, key)`   | Searches for the specified key in the specified array using the binary search algorithm. Array **must be sorted**. | O(log N)                      | Returns index if found, `-(insertion_point) - 1` if not found. |
| `equals(array1, array2)`     | Returns `true` if the two specified arrays are equal to one another (same elements in same order).      | O(N)                          | Overloaded for all primitive types and `Object[]`.             |
| `deepEquals(Object[] a1, Object[] a2)` | Returns `true` if two specified arrays are "deeply equal" (useful for multi-dimensional arrays). | O(N) (recursive)              | Compares nested arrays recursively.                              |
| `fill(array, value)`         | Assigns the specified value to each element of the specified array.                                     | O(N)                          |                                                                  |
| `copyOf(original, newLength)`| Copies the specified array, truncating or padding with default values/nulls to the specified length.    | O(N)                          | Returns a *new* array.                                           |
| `copyOfRange(original, from, to)`| Copies the specified range of the specified array into a new array.                                       | O(N)                          | `from` is inclusive, `to` is exclusive.                          |
| `toString(array)`            | Returns a string representation of the contents of the specified array (e.g., `"[1, 2, 3]"`).             | O(N)                          | Useful for printing array contents.                              |
| `deepToString(Object[] a)`   | Returns a string representation of the "deep contents" of the specified array (for nested arrays).      | O(N) (recursive)              |                                                                  |
| `asList(T... a)`             | Returns a fixed-size `List` backed by the specified array. Changes to the array reflect in the list, and vice-versa. | O(1) (creation)               | The returned list does not support add/remove operations.        |
| `parallelSort(array)`        | Sorts the specified array in parallel using a Fork/Join merge sort.                                     | O(N log N) (parallel overhead) | Potentially faster for large arrays on multi-core systems.       |
| `hashCode(array)`            | Returns a hash code based on the contents of the specified array.                                       | O(N)                          |                                                                  |

---

## 3. `java.lang.String` (Immutable Sequence of Characters)

Strings are immutable sequences of characters. All methods that seem to "modify" a string actually return a *new* string.

| Method                    | Description                                                                            | Time Complexity (Typical) | Returns (New String) |
| :------------------------ | :------------------------------------------------------------------------------------- | :------------------------ | :------------------- |
| `length()`                | Returns the number of characters in the string.                                        | O(1)                      | -                    |
| `charAt(int index)`       | Returns the character at the specified index.                                          | O(1)                      | `char`               |
| `substring(int beginIndex)` | Returns a new string that is a substring of this string, starting from `beginIndex` to the end. | O(N)                      | `String`             |
| `substring(int beginIndex, int endIndex)` | Returns a new string that is a substring of this string, from `beginIndex` (inclusive) to `endIndex` (exclusive). | O(N)                      | `String`             |
| `concat(String str)`      | Concatenates the specified string to the end of this string.                           | O(N + M)                  | `String`             |
| `indexOf(String str)`     | Returns the index of the first occurrence of the specified substring.                  | O(N * M) (worst-case)     | `int`                |
| `lastIndexOf(String str)` | Returns the index of the last occurrence of the specified substring.                   | O(N * M) (worst-case)     | `int`                |
| `equals(Object anObject)` | Compares this string to the specified object.                                          | O(N)                      | `boolean`            |
| `equalsIgnoreCase(String anotherString)` | Compares this string to another string, ignoring case considerations.                    | O(N)                      | `boolean`            |
| `compareTo(String anotherString)` | Compares two strings lexicographically.                                                | O(N)                      | `int`                |
| `startsWith(String prefix)` | Tests if this string starts with the specified prefix.                                 | O(M)                      | `boolean`            |
| `endsWith(String suffix)` | Tests if this string ends with the specified suffix.                                   | O(M)                      | `boolean`            |
| `contains(CharSequence s)`| Returns `true` if this string contains the specified sequence of characters.           | O(N * M) (worst-case)     | `boolean`            |
| `replace(char oldChar, char newChar)` | Returns a new string resulting from replacing all occurrences of `oldChar` with `newChar`. | O(N)                      | `String`             |
| `replaceAll(String regex, String replacement)` | Replaces each substring of this string that matches the given regular expression with the given replacement. | Varies (regex complexity) | `String`             |
| `trim()`                  | Returns a string whose value is this string, with all leading and trailing whitespace removed. | O(N)                      | `String`             |
| `toLowerCase()`           | Converts all of the characters in this string to lower case.                           | O(N)                      | `String`             |
| `toUpperCase()`           | Converts all of the characters in this string to upper case.                           | O(N)                      | `String`             |
| `split(String regex)`     | Splits this string around matches of the given regular expression. Returns a `String[]`. | Varies (regex complexity) | `String[]`           |
| `isEmpty()`               | Returns `true` if `length()` is 0.                                                     | O(1)                      | `boolean`            |
| `valueOf(primitive)`      | Static method to convert various primitive types (int, char, boolean, etc.) to their string representation. | O(digits)                 | `String`             |

---

## 4. `java.lang.Character` (Utility Class for Character Operations)

This class wraps a primitive `char` value in an object and provides static utility methods for character manipulation and classification (e.g., checking if a character is a digit or letter).

| Method                       | Description                                                                            | Time Complexity (Typical) |
| :--------------------------- | :------------------------------------------------------------------------------------- | :------------------------ |
| `isLetter(char ch)`          | Determines if the specified character is a letter.                                     | O(1)                      |
| `isDigit(char ch)`           | Determines if the specified character is a digit (0-9).                                | O(1)                      |
| `isLetterOrDigit(char ch)`   | Determines if the specified character is a letter or a digit.                          | O(1)                      |
| `isWhitespace(char ch)`      | Determines if the specified character is white space (space, tab, newline, etc.).      | O(1)                      |
| `isUpperCase(char ch)`       | Determines if the specified character is an uppercase character.                       | O(1)                      |
| `isLowerCase(char ch)`       | Determines if the specified character is a lowercase character.                        | O(1)                      |
| `toUpperCase(char ch)`       | Converts the character argument to uppercase.                                          | O(1)                      |
| `toLowerCase(char ch)`       | Converts the character argument to lowercase.                                          | O(1)                      |
| `getNumericValue(char ch)`   | Returns the int value that the specified Unicode character represents (e.g., '1' -> 1). | O(1)                      |
| `forDigit(int digit, int radix)` | Returns the character representation for a specific digit in the specified radix.      | O(1)                      |
| `toString(char ch)`          | Returns a `String` object representing the specified `char` value.                     | O(1)                      |

---

## 5. `java.util.List` (Interface)

Ordered collection (sequence) that allows duplicate elements. Elements can be accessed by their integer index. `ArrayList` and `LinkedList` are common implementations.

| Method                   | Description                                                               | Time Complexity (`ArrayList`/`LinkedList`) | Notes                                                               |
| :----------------------- | :------------------------------------------------------------------------ | :----------------------------------------- | :------------------------------------------------------------------ |
| `add(E e)`               | Appends the specified element to the end of this list.                    | O(1) / O(1)                                | Amortized O(1) for `ArrayList` (may resize).                         |
| `add(int index, E e)`    | Inserts the specified element at the specified position.                  | O(N) / O(N)                                | Shifts elements. `LinkedList` is O(N) as it must traverse to `index`. |
| `get(int index)`         | Returns the element at the specified position.                            | O(1) / O(N)                                | Random access for `ArrayList`, traversal for `LinkedList`.          |
| `set(int index, E e)`    | Replaces the element at the specified position.                           | O(1) / O(N)                                |                                                                     |
| `remove(int index)`      | Removes the element at the specified position.                            | O(N) / O(N)                                | Shifts elements for `ArrayList`, traversal for `LinkedList`.        |
| `remove(Object o)`       | Removes the first occurrence of the specified element, if present.        | O(N) / O(N)                                |                                                                     |
| `size()`                 | Returns the number of elements in this list.                              | O(1) / O(1)                                |                                                                     |
| `isEmpty()`              | Returns `true` if this list contains no elements.                         | O(1) / O(1)                                |                                                                     |
| `contains(Object o)`     | Returns `true` if this list contains the specified element.               | O(N) / O(N)                                |                                                                     |
| `indexOf(Object o)`      | Returns the index of the first occurrence, or -1 if not found.            | O(N) / O(N)                                |                                                                     |
| `clear()`                | Removes all elements from the list.                                       | O(N) / O(N)                                |                                                                     |
| `iterator()`             | Returns an iterator over the elements.                                    | O(1) / O(1)                                | For efficient traversal.                                            |
| `toArray()`              | Returns an array containing all of the elements in this list.             | O(N) / O(N)                                |                                                                     |

---

## 6. `java.util.Queue` (Interface - FIFO)

A collection designed for holding elements prior to processing. Typically, elements are added at the tail and removed from the head (FIFO).

| Method              | Description                                                              | Time Complexity (Typical) | Notes                                                                                                    |
| :------------------ | :----------------------------------------------------------------------- | :------------------------ | :------------------------------------------------------------------------------------------------------- |
| `add(E e)`          | Inserts the specified element into this queue. Throws `IllegalStateException` if full. | O(1)                      | Use this when capacity is guaranteed.                                                                    |
| `offer(E e)`        | Inserts the specified element into this queue. Returns `true` on success, `false` if full. | O(1)                      | Preferred over `add` for capacity-constrained queues (e.g., `ArrayBlockingQueue`).                       |
| `remove()`          | Retrieves and removes the head of this queue. Throws `NoSuchElementException` if empty. | O(1)                      |                                                                                                          |
| `poll()`            | Retrieves and removes the head of this queue. Returns `null` if empty.   | O(1)                      | Preferred over `remove` for graceful handling of empty queues.                                           |
| `element()`         | Retrieves, but does not remove, the head of this queue. Throws `NoSuchElementException` if empty. | O(1)                      |                                                                                                          |
| `peek()`            | Retrieves, but does not remove, the head of this queue. Returns `null` if empty. | O(1)                      | Preferred over `element` for graceful handling.                                                          |
| `isEmpty()`         | Returns `true` if this queue contains no elements.                       | O(1)                      |                                                                                                          |
| `size()`            | Returns the number of elements in this queue.                            | O(1)                      |                                                                                                          |

---

## 7. `java.util.Deque` (Interface - Double-Ended Queue)

A linear collection that supports element insertion and removal at both ends. Can be used as a Stack or a Queue.

| Method                    | Description                                                              | Time Complexity (Typical) | Notes                                                                                                                                                                  |
| :------------------------ | :----------------------------------------------------------------------- | :------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `addFirst(E e)` / `offerFirst(E e)` | Inserts the specified element at the front. (`addFirst` throws `IllegalStateException`, `offerFirst` returns boolean). | O(1)                      |                                                                                                                                                                        |
| `addLast(E e)` / `offerLast(E e)` | Inserts the specified element at the end. (`addLast` throws `IllegalStateException`, `offerLast` returns boolean).    | O(1)                      | Same as `add(E e)` / `offer(E e)` for `Queue` interface.                                                                                                             |
| `removeFirst()` / `pollFirst()` | Retrieves and removes the first element. (`removeFirst` throws `NoSuchElementException`, `pollFirst` returns null). | O(1)                      | Same as `remove()` / `poll()` for `Queue` interface when used as a queue.                                                                                            |
| `removeLast()` / `pollLast()` | Retrieves and removes the last element. (`removeLast` throws `NoSuchElementException`, `pollLast` returns null).    | O(1)                      |                                                                                                                                                                        |
| `getFirst()` / `peekFirst()` | Retrieves, but does not remove, the first element. (`getFirst` throws `NoSuchElementException`, `peekFirst` returns null). | O(1)                      | Same as `element()` / `peek()` for `Queue` interface when used as a queue.                                                                                           |
| `getLast()` / `peekLast()` | Retrieves, but does not remove, the last element. (`getLast` throws `NoSuchElementException`, `peekLast` returns null). | O(1)                      |                                                                                                                                                                        |
| `push(E e)`               | Pushes an element onto the stack represented by this deque (equivalent to `addFirst`). | O(1)                      | Use when using Deque as a Stack.                                                                                                                                       |
| `pop()`                   | Pops an element from the stack represented by this deque (equivalent to `removeFirst`). | O(1)                      | Use when using Deque as a Stack.                                                                                                                                       |
| `isEmpty()`               | Returns `true` if this deque contains no elements.                       | O(1)                      |                                                                                                                                                                        |
| `size()`                  | Returns the number of elements in the deque.                             | O(1)                      |                                                                                                                                                                        |

---

## 8. `java.util.Stack` (Class - LIFO)

A legacy class (part of the original Java Collection Framework) that represents a last-in-first-out (LIFO) stack of objects. It extends `Vector` and is generally **discouraged in favor of `ArrayDeque`** for better performance and API consistency.

| Method       | Description                                              | Time Complexity (Typical) | Notes                                                                               |
| :----------- | :------------------------------------------------------- | :------------------------ | :---------------------------------------------------------------------------------- |
| `push(E item)` | Pushes an item onto the top of this stack.             | O(1) (amortized)          |                                                                                     |
| `pop()`      | Removes the object at the top of this stack and returns that object. | O(1)                      | Throws `EmptyStackException` if stack is empty.                                     |
| `peek()`     | Looks at the object at the top of this stack without removing it. | O(1)                      | Throws `EmptyStackException` if stack is empty.                                     |
| `isEmpty()`  | Tests if this stack is empty.                            | O(1)                      |                                                                                     |
| `size()`     | Returns the number of items in the stack.                | O(1)                      | Inherited from `Vector`.                                                            |
| `search(Object o)` | Returns the 1-based position where an object is on this stack. | O(N)                      | Less common for abstract stack usage. `1` is the top, `2` is the next, etc.         |

---

## 9. `java.util.PriorityQueue` (Class - Heap-based)

An unbounded priority queue based on a priority heap. Elements are ordered according to their natural ordering or by a `Comparator` provided at construction time. The "head" of the queue is the least element based on priority.

| Method          | Description                                                              | Time Complexity (Typical) | Notes                                                                            |
| :-------------- | :----------------------------------------------------------------------- | :------------------------ | :------------------------------------------------------------------------------- |
| `add(E e)`      | Inserts the specified element into this priority queue.                  | O(log N)                  |                                                                                  |
| `offer(E e)`    | Inserts the specified element into this priority queue. Returns `true` on success. | O(log N)                  | Same functionality as `add` for `PriorityQueue` as it's unbounded.               |
| `remove()`      | Retrieves and removes the head of this queue. Throws `NoSuchElementException` if empty. | O(log N)                  | Removes the element with the highest priority (or lowest value in min-heap).     |
| `poll()`        | Retrieves and removes the head of this queue. Returns `null` if empty.   | O(log N)                  | Preferred over `remove` for graceful handling.                                   |
| `element()`     | Retrieves, but does not remove, the head of this queue. Throws `NoSuchElementException` if empty. | O(1)                      |                                                                                  |
| `peek()`        | Retrieves, but does not remove, the head of this queue. Returns `null` if empty. | O(1)                      |                                                                                  |
| `isEmpty()`     | Returns `true` if this priority queue contains no elements.              | O(1)                      |                                                                                  |
| `size()`        | Returns the number of elements in the priority queue.                    | O(1)                      |                                                                                  |
| `contains(Object o)` | Returns `true` if this queue contains the specified element.             | O(N)                      | Searching requires linear scan as heap structure is not designed for fast lookup. |

---

## 10. `java.util.Set` (Interface - Unique Elements)

A collection that contains no duplicate elements. It models the mathematical set abstraction. `HashSet` provides unordered, fast access; `LinkedHashSet` maintains insertion order; `TreeSet` stores elements in sorted order.

| Method                | Description                                                              | Time Complexity (`HashSet`/`LinkedHashSet`/`TreeSet`) | Notes                                                          |
| :-------------------- | :----------------------------------------------------------------------- | :---------------------------------------------------- | :------------------------------------------------------------- |
| `add(E e)`            | Adds the specified element to this set if it is not already present.     | O(1) avg / O(1) avg / O(log N)                        | Returns `true` if element was added, `false` otherwise.        |
| `remove(Object o)`    | Removes the specified element from this set if it is present.            | O(1) avg / O(1) avg / O(log N)                        | Returns `true` if element was removed, `false` otherwise.      |
| `contains(Object o)`  | Returns `true` if this set contains the specified element.               | O(1) avg / O(1) avg / O(log N)                        |                                                                |
| `isEmpty()`           | Returns `true` if this set contains no elements.                         | O(1) / O(1) / O(1)                                    |                                                                |
| `size()`              | Returns the number of elements in this set.                              | O(1) / O(1) / O(1)                                    |                                                                |
| `clear()`             | Removes all of the elements from this set.                               | O(N) / O(N) / O(N)                                    |                                                                |
| `iterator()`          | Returns an iterator over the elements in this set.                       | O(1) (creation)                                       | Iteration order varies (`HashSet` is unordered, `LinkedHashSet` is insertion-ordered, `TreeSet` is sorted). |
| `addAll(Collection<? extends E> c)` | Adds all elements in the specified collection to this set.       | Varies (N * avg_add_time)                             |                                                                |
| `removeAll(Collection<?> c)` | Removes from this set all of its elements that are contained in the specified collection. | Varies (N * avg_remove_time)                          |                                                                |
| `retainAll(Collection<?> c)` | Retains only the elements in this set that are contained in the specified collection. | Varies (N * avg_contains_time)                        | Set intersection.                                              |

---

## 11. `java.util.Map` (Interface - Key-Value Pairs)

An object that maps keys to values. A map cannot contain duplicate keys; each key can map to at most one value. `HashMap` provides unordered, fast access; `LinkedHashMap` maintains insertion order; `TreeMap` stores mappings in sorted key order.

| Method                   | Description                                                              | Time Complexity (`HashMap`/`LinkedHashMap`/`TreeMap`) | Notes                                                               |
| :----------------------- | :----------------------------------------------------------------------- | :---------------------------------------------------- | :------------------------------------------------------------------ |
| `put(K key, V value)`    | Associates the specified `value` with the specified `key` in this map.   | O(1) avg / O(1) avg / O(log N)                        | If key already exists, old value is replaced. Returns old value.    |
| `get(Object key)`        | Returns the `value` to which the specified `key` is mapped, or `null` if no mapping. | O(1) avg / O(1) avg / O(log N)                        |                                                                     |
| `remove(Object key)`     | Removes the mapping for a key from this map if it is present.            | O(1) avg / O(1) avg / O(log N)                        | Returns the removed value, or `null` if key not found.              |
| `containsKey(Object key)`| Returns `true` if this map contains a mapping for the specified key.     | O(1) avg / O(1) avg / O(log N)                        |                                                                     |
| `containsValue(Object value)` | Returns `true` if this map maps one or more keys to the specified value. | O(N) / O(N) / O(N)                                    | Requires iterating through values, which is O(N).                   |
| `isEmpty()`              | Returns `true` if this map contains no key-value mappings.             | O(1) / O(1) / O(1)                                    |                                                                     |
| `size()`                 | Returns the number of key-value mappings in this map.                    | O(1) / O(1) / O(1)                                    |                                                                     |
| `clear()`                | Removes all of the mappings from this map.                               | O(N) / O(N) / O(N)                                    |                                                                     |
| `keySet()`               | Returns a `Set` view of the keys contained in this map.                  | O(1) (view)                                           | Iterating over the `keySet` is O(N).                                |
| `values()`               | Returns a `Collection` view of the values contained in this map.         | O(1) (view)                                           | Iterating over the `values` is O(N).                                |
| `entrySet()`             | Returns a `Set` view of the mappings (key-value pairs) contained in this map. | O(1) (view)                                           | Each element in the `Set` is a `Map.Entry<K, V>`. Iteration is O(N). |
| `forEach(BiConsumer action)` | Performs the given action for each entry in this map until all entries have been processed or the action throws an exception. | O(N)                      | Java 8+ lambda-friendly method for iteration.                       |
| `getOrDefault(Object key, V defaultValue)` | Returns the value to which the specified key is mapped, or `defaultValue` if this map contains no mapping for the key. | O(1) avg / O(1) avg / O(log N)                        | Java 8+ method.                                                     |

---

## 12. `java.util.Collections` (Utility Class for Collection Operations)

This class consists exclusively of static methods that operate on or return collections. It provides algorithms for sorting, searching, and manipulating collections, as well as "wrappers" that provide thread-safe or unmodifiable views.

| Method                          | Description                                                                                             | Time Complexity (Typical) | Notes                                                            |
| :------------------------------ | :------------------------------------------------------------------------------------------------------ | :------------------------ | :--------------------------------------------------------------- |
| `sort(List list)`               | Sorts the specified list into ascending order, according to the natural ordering of its elements.       | O(N log N)                | List must implement `Comparable` or provide a `Comparator`.      |
| `sort(List list, Comparator c)` | Sorts the specified list according to the order induced by the specified comparator.                    | O(N log N)                |                                                                  |
| `binarySearch(List list, key)`  | Searches the specified sorted list for the specified object using the binary search algorithm.          | O(log N)                  | List **must be sorted**.                                         |
| `reverse(List list)`            | Reverses the order of the elements in the specified list.                                             | O(N)                      |                                                                  |
| `shuffle(List list)`            | Randomly permutes the specified list using a default source of randomness.                              | O(N)                      |                                                                  |
| `fill(List list, Object obj)`   | Replaces all of the elements of the specified list with the specified element.                          | O(N)                      |                                                                  |
| `copy(List dest, List src)`     | Copies all of the elements from one list into another. `dest` must be at least as large as `src`.     | O(N)                      | Overwrites elements in `dest`.                                   |
| `min(Collection coll)`          | Returns the minimum element of the given collection, according to the natural ordering of its elements. | O(N)                      |                                                                  |
| `max(Collection coll)`          | Returns the maximum element of the given collection, according to the natural ordering of its elements. | O(N)                      |                                                                  |
| `frequency(Collection coll, Object o)` | Returns the number of elements in the specified collection equal to the specified object.             | O(N)                      |                                                                  |
| `disjoint(Collection c1, Collection c2)` | Returns `true` if the two specified collections have no elements in common.                    | O(N + M)                  |                                                                  |
| `addAll(Collection c, T... elements)` | Adds all of the specified elements to the specified collection.                                 | O(M) (M elements)         | Useful for adding multiple elements at once.                     |
| `emptyList()` / `emptySet()` / `emptyMap()` | Returns immutable empty instances of `List`, `Set`, `Map`.                              | O(1)                      | Good for returning empty collections instead of `null`.          |
| `singletonList(T o)` / `singleton(T o)` / `singletonMap(K key, V value)` | Returns immutable collections containing only the specified element(s). | O(1)                      |                                                                  |
| `synchronizedList(List list)` / `synchronizedSet(Set s)` / `synchronizedMap(Map m)` | Returns a synchronized (thread-safe) view of the specified collection.  | O(1) (wrapper)            | Useful for multi-threaded environments where direct synchronization is needed. |
| `unmodifiableList(List list)` / `unmodifiableSet(Set s)` / `unmodifiableMap(Map m)` | Returns an unmodifiable view of the specified collection. Any attempt to modify it will throw `UnsupportedOperationException`. | O(1) (wrapper)            | Provides read-only access.                                       |

---
