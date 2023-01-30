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
## 【Easy】 94. Binary Tree Inorder Traversal
**Link** : https://leetcode.com/problems/binary-tree-inorder-traversal/description/
```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList();
        inorder(root,result);
        return result;
        
    }
    public void inorder(TreeNode root,List<Integer> result){
        if(root != null){
            inorder(root.left,result);
            result.add(root.val);
            inorder(root.right,result);
        }
    }
}
```
## 【Easy】 102. Binary Tree Level Order Traversal
**Link** : https://leetcode.com/problems/binary-tree-inorder-traversal/description/

```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(root == null){
            return result;
        }
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        while(!queue.isEmpty()){
            List<Integer> temp = new ArrayList();
            int length = queue.size();
            while(length > 0){
                TreeNode node = queue.poll();
                temp.add(node.val);
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
                length--;
            }
            result.add(temp);
        }

        return result;
        
    }
    
}
```
## 【Medium】 107. Binary Tree Level Order Traversal II
**Link** : https://leetcode.com/problems/binary-tree-level-order-traversal-ii/description/
```
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> result = new ArrayList();
        if(root == null){
            return result;
        }
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        while(!queue.isEmpty()){
            List<Integer> temp = new ArrayList();
            int length = queue.size();

            while(length > 0){
                TreeNode node = queue.poll();
                temp.add(node.val);
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
                length--;
            }
            result.add(temp);
        }
        List<List<Integer>> result1 = new ArrayList();
        for(int i = result.size() - 1;i >= 0;i--){
            result1.add(result.get(i));
        }
        return result1;
    }
}
```
## [Medium] 199. Binary Tree Right Side View
**Link** : https://leetcode.com/problems/binary-tree-right-side-view/description/
```
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result = new ArrayList();

        if(root == null){
            return result;
        }
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        while(!queue.isEmpty()){
            
            
            
            int length = queue.size();
            while(length > 0){
                TreeNode node = queue.poll();
                if(node.left != null){
                    queue.add(node.left);
                }
                if(node.right != null){
                    queue.add(node.right);
                }
                
                if(length == 1){
                    result.add(node.val);
                }
                length--;
                
                
            }
            

        }
        return result;
    }   
}
```

## [Easy] 637. Average of Levels in Binary Tree
**Link** : https://leetcode.com/problems/average-of-levels-in-binary-tree/
```
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        List<Double> result = new ArrayList();
        if(root == null){
            return result;
        }
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        while(!queue.isEmpty()){
            int length = queue.size();
            double count = length;
            double sum = 0;
            while(length > 0){
                
                TreeNode node = queue.poll();
                sum = sum + node.val;
                if(node.left != null){
                    queue.add(node.left);
                }
                if(node.right != null){
                    queue.add(node.right);
                }
                length--;

                if(length == 0){
                    result.add(sum / count);
                }
            }
        }
        return result;
    }
}
```

## [Easy] 226. Invert Binary Tree
**Link** : https://leetcode.com/problems/invert-binary-tree/description/
```
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null){
            return root;
        }
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        while(!queue.isEmpty()){
            int length = queue.size();
            while(length > 0){
                TreeNode node = queue.poll();
                
                swap(node);
                if(node.right != null){
                    queue.offer(node.right);
                }
                if(node.left != null){
                    queue.offer(node.left);
                }
                
                length--;
            }
 
        }

        return root;
    }

    public void swap(TreeNode root){
        TreeNode temp = root.right;
        root.right = root.left;
        root.left = temp;
    }
}
```

## [Easy] 101. Symmetric Tree
**Link** : https://leetcode.com/problems/symmetric-tree/description/
```
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
        
        Deque<TreeNode> queue = new LinkedList();
        queue.offer(root.left);
        queue.offer(root.right);
        while(!queue.isEmpty()){
            TreeNode left = queue.pollFirst();
            TreeNode right = queue.pollLast();

            if(left == null && right == null){
                continue;
            }
            if(left == null || right == null || right.val != left.val){
                return false;
            }
            queue.offerFirst(left.left);
            queue.offerFirst(left.right);
            queue.offerLast(right.right);
            queue.offerLast(right.left);
            
        }
        return true;
    }
    
    
}
```
## [Easy] 104. Maximum Depth of Binary Tree
**Link** : https://leetcode.com/problems/maximum-depth-of-binary-tree/description/
```
class Solution {
    public int maxDepth(TreeNode root) {

        Queue<TreeNode> queue = new LinkedList();
        int result = 0;
        if(root == null){
            return result;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            result = result + 1;
            while(size > 0){
                TreeNode node = queue.poll();
                
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
                size--;
            }
            
        }
        return result;
    }
}
```
## [Easy] 111. Minimum Depth of Binary Tree
**Link** : https://leetcode.com/problems/minimum-depth-of-binary-tree/submissions/887840502/
```
class Solution {
    public int minDepth(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList();
        int result = 0;
        if(root == null){
            return result;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            result = result + 1;
            while(size > 0){
                TreeNode node = queue.poll();
                if(node.left == null && node.right == null){
                    return result;
                }
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
                size--;
            }
            
        }
        return result;
    }
}
```
## [Medium] 222. Count Complete Tree Nodes
**Link** : https://leetcode.com/problems/count-complete-tree-nodes/description/
```
class Solution {
    public int countNodes(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList();
        int result = 0;
        if(root == null){
            return result;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            
            while(size > 0){
                TreeNode node = queue.poll();
                result = result + 1;
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
                size--;
            }
        }
        return result;
    }
}
```
