# getOrDefault() vs computeIfAbsent()

| Feature          | `getOrDefault(key, defaultValue)`                                                                                  | `computeIfAbsent(key, mappingFunction)`                                                                                     |
| ---------------- | ------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| **Purpose**      | Returns the value for the key if present; otherwise returns the given default (without adding it).                 | Returns the existing value for the key or, if absent, computes it using the given function and **inserts** it into the map. |
| **Map Mutation** | ❌ Does **not modify** the map.                                                                                     | ✅ **Modifies** the map if the key is absent.                                                                                |
| **When to Use**  | When you just want to *read* a value or use a default temporarily.                                                 | When you want to *initialize and store* a missing value automatically.                                                      |
| **Example**      | `List<String> list = map.getOrDefault(key, new ArrayList<>());` → list not added to map unless you do it manually. | `List<String> list = map.computeIfAbsent(key, k -> new ArrayList<>());` → new list created **and stored** if key missing.   |

## More Functions 

| Situation                                            | Best Choice          |
| ---------------------------------------------------- | -------------------- |
| Only want to read, not modify map                    | `getOrDefault()`     |
| Want to create and store default value automatically | `computeIfAbsent()`  |
| Want to modify value if key exists                   | `computeIfPresent()` |
| Want to always compute new value (exists or not)     | `compute()`          |
