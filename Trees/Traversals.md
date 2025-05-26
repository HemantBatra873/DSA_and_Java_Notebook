# Traversals

## Traversal Types:

1. Preorder (Root → Left → Right)
Pattern: Process root first, then recursively traverse left and right

2. Inorder (Left → Root → Right)
Pattern: Process left subtree, then root, then right subtree

3. Postorder (Left → Right → Root)
Pattern: Process both subtrees first, then root

## Code

The most important difference that you can find is the order in the helper method while traversing.

```
    
    /**
     * PREORDER TRAVERSAL (Root → Left → Right)
     * Time: O(n), Space: O(h) where h is height of tree
     */
    public static List<Integer> preorderTraversalRecursive(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        preorderHelper(root, result);
        return result;
    }
    
    private static void preorderHelper(TreeNode node, List<Integer> result) {
        if (node == null) return;
        
        result.add(node.val);           // Visit root
        preorderHelper(node.left, result);   // Traverse left subtree
        preorderHelper(node.right, result);  // Traverse right subtree
    }
    
    /**
     * INORDER TRAVERSAL (Left → Root → Right)
     * Time: O(n), Space: O(h)
     */
    public static List<Integer> inorderTraversalRecursive(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        inorderHelper(root, result);
        return result;
    }
    
    private static void inorderHelper(TreeNode node, List<Integer> result) {
        if (node == null) return;
        
        inorderHelper(node.left, result);    // Traverse left subtree
        result.add(node.val);                // Visit root
        inorderHelper(node.right, result);   // Traverse right subtree
    }
    
    /**
     * POSTORDER TRAVERSAL (Left → Right → Root)
     * Time: O(n), Space: O(h)
     */
    public static List<Integer> postorderTraversalRecursive(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        postorderHelper(root, result);
        return result;
    }
    
    private static void postorderHelper(TreeNode node, List<Integer> result) {
        if (node == null) return;
        
        postorderHelper(node.left, result);  // Traverse left subtree
        postorderHelper(node.right, result); // Traverse right subtree
        result.add(node.val);                // Visit root
    }
```
