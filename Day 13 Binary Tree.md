## 【Easy】 144. Binary Tree Preorder Traversal
**Link** : https://leetcode.com/problems/binary-tree-preorder-traversal/description/
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        preorder(result,root);
        return result;
    }

    void preorder(List<Integer> result,TreeNode root){
        if(root == null){
            return;
        }

        result.add(root.val);
        preorder(result,root.left);
        preorder(result,root.right);
    }
}
```
## 【Easy】 145. Binary Tree Postorder Traversal
**Link** : https://leetcode.com/problems/binary-tree-postorder-traversal/description/
```
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        postorder(result,root);
        return result;
    }

    public void postorder(List<Integer> result,TreeNode root){
        if(root == null){
            return;
        }


        postorder(result,root.left);
        postorder(result,root.right);
        result.add(root.val);

    }
}
```
