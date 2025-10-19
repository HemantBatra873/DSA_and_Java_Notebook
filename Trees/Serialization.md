# 🟩 1. Serialize & Deserialize a **Binary Tree**

This is the **general case** (used in LeetCode 297 — *Serialize and Deserialize Binary Tree*).

We use **preorder traversal** and explicitly include `"null"` markers.

---

### ✅ Code (Binary Tree)

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

public class BinaryTreeCodec {

    // SERIALIZE (Tree -> String)
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        serializeHelper(root, sb);
        return sb.toString();
    }

    private void serializeHelper(TreeNode node, StringBuilder sb) {
        if (node == null) {
            sb.append("null,");
            return;
        }
        sb.append(node.val).append(",");
        serializeHelper(node.left, sb);
        serializeHelper(node.right, sb);
    }

    // DESERIALIZE (String -> Tree)
    public TreeNode deserialize(String data) {
        Queue<String> nodes = new LinkedList<>(Arrays.asList(data.split(",")));
        return deserializeHelper(nodes);
    }

    private TreeNode deserializeHelper(Queue<String> nodes) {
        String val = nodes.poll();
        if (val.equals("null")) return null;

        TreeNode node = new TreeNode(Integer.parseInt(val));
        node.left = deserializeHelper(nodes);
        node.right = deserializeHelper(nodes);
        return node;
    }

    // Test
    public static void main(String[] args) {
        BinaryTreeCodec codec = new BinaryTreeCodec();
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.right.left = new TreeNode(4);
        root.right.right = new TreeNode(5);

        String serialized = codec.serialize(root);
        System.out.println("Serialized: " + serialized);

        TreeNode deserialized = codec.deserialize(serialized);
        System.out.println("Deserialized Root: " + deserialized.val);
    }
}
```

### 🧠 Key points:

* Uses **"null"** placeholders.
* Works for **any** binary tree shape.
* Deserialization is recursive and follows preorder order.

---

# 🟨 2. Serialize & Deserialize a **Binary Search Tree (BST)**

BSTs follow ordering property, so we can serialize **without nulls** — just store preorder traversal.
(Used in LeetCode 449 — *Serialize and Deserialize BST*.)

---

### ✅ Code (BST)

```java
import java.util.*;

class BSTCodec {

    // SERIALIZE: Preorder traversal (no nulls)
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        preorder(root, sb);
        return sb.toString().trim();
    }

    private void preorder(TreeNode node, StringBuilder sb) {
        if (node == null) return;
        sb.append(node.val).append(" ");
        preorder(node.left, sb);
        preorder(node.right, sb);
    }

    // DESERIALIZE: Rebuild using BST property
    public TreeNode deserialize(String data) {
        if (data.isEmpty()) return null;
        Queue<Integer> q = new LinkedList<>();
        for (String s : data.split(" ")) {
            q.offer(Integer.parseInt(s));
        }
        return build(q, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }

    private TreeNode build(Queue<Integer> q, int lower, int upper) {
        if (q.isEmpty()) return null;
        int val = q.peek();
        if (val < lower || val > upper) return null;

        q.poll();
        TreeNode node = new TreeNode(val);
        node.left = build(q, lower, val);
        node.right = build(q, val, upper);
        return node;
    }

    // Test
    public static void main(String[] args) {
        BSTCodec codec = new BSTCodec();

        TreeNode root = new TreeNode(8);
        root.left = new TreeNode(5);
        root.left.left = new TreeNode(1);
        root.left.right = new TreeNode(7);
        root.right = new TreeNode(10);
        root.right.right = new TreeNode(12);

        String serialized = codec.serialize(root);
        System.out.println("Serialized: " + serialized);

        TreeNode deserialized = codec.deserialize(serialized);
        System.out.println("Deserialized Root: " + deserialized.val);
    }
}
```

---

# 🔍 Comparison Summary

| Aspect                    | Binary Tree                                 | BST                                  |
| ------------------------- | ------------------------------------------- | ------------------------------------ |
| Serialization output      | `"1,2,null,null,3,4,null,null,5,null,null"` | `"8 5 1 7 10 12"`                    |
| Uses `"null"` markers     | ✅ Yes                                       | ❌ No                                 |
| Relies on BST property    | ❌ No                                        | ✅ Yes                                |
| Deserialization logic     | Recursive preorder with nulls               | Recursive preorder with value bounds |
| Works for arbitrary trees | ✅                                           | ❌ Only BSTs                          |
