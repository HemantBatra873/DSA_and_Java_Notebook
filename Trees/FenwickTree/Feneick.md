# Generic Class use Anywhere

```java
static class FenwickTree {
    private final int size;
    private final long[] tree;

    public FenwickTree(int size) {
        this.size = size;
        this.tree = new long[size + 1];
    }

    // Add delta to the value at index.
    public void update(int index, long delta) {
        while (index <= size) {
            tree[index] += delta;
            index += index & -index;
        }
    }

    // Returns sum of values from 1 to index.
    public long query(int index) {
        long sum = 0;

        while (index > 0) {
            sum += tree[index];
            index -= index & -index;
        }

        return sum;
    }

    // Returns sum of values from left to right, inclusive.
    public long rangeQuery(int left, int right) {
        return query(right) - query(left - 1);
    }

    // Returns the value at a single index.
    public long pointQuery(int index) {
        return rangeQuery(index, index);
    }
}
```