# Level Order Traversal
Traverse the tree level by level.
```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new ArrayList<>();
        if(root == null) return ans;
        helper(root , 1 , ans);
        return ans;
    }

    public void helper(TreeNode root , int level , List<List<Integer>> ans){
        if(root == null) return;
        if(level > ans.size()) ans.add(new ArrayList<>());
        ans.get(level - 1).add(root.val);
        helper(root.left , level + 1 , ans);
        helper(root.right , level + 1 , ans);
    }
}
```
