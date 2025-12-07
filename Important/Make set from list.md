## HashSet from List

Instead of doing this 

```java
Set<String> words = new HashSet<>();
for(String word : wordDict) words.add(word);
```

You can do this

```java
Set<Integer> set = new HashSet<>(list);
```

This only works with list and not arrays. Specially int[] because int is a primitive data type and not a collection like 
List , Set and Map.   
Never try to convert int arrays to list it will just put the entire array as one object in the list and give unwanted behaviour.
