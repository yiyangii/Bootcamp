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

## [Medium] 429. N-ary Tree Level Order Traversal
**Link** : https://leetcode.com/problems/n-ary-tree-level-order-traversal/description/
```
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        Queue<Node> queue = new LinkedList();
        List<List<Integer>> result = new ArrayList();
        if(root == null){
            return result;
        } 
        queue.offer(root);
        while(!queue.isEmpty()){
            List<Integer> temp = new ArrayList();
            int length = queue.size();
            
            
            while(length > 0){
                Node node = queue.poll();
                temp.add(node.val);
                for(Node child : node.children){
                    queue.offer(child);
                }
                length--;
            }
            result.add(temp);

        }

        return result;
    }
}

```
## [Medium] 515. Find Largest Value in Each Tree Row
https://leetcode.com/problems/find-largest-value-in-each-tree-row/description/
```
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList();
        List<Integer> result = new ArrayList();
        if(root == null){
            return result;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            int max = Integer.MIN_VALUE;
            while(size > 0){
                TreeNode node = queue.poll();
                if(node.val > max){
                    max = node.val;
                }
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
                size--;
            }
            result.add(max);
        }
        return result;
    }
}
```


## [Medium] 116. Populating Next Right Pointers in Each Node
**Link** : https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/
```
class Solution {
    public Node connect(Node root) {
        if(root == null){
            return root;
        }
        Queue<Node> queue = new LinkedList();
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            Node current = queue.poll();   
            if(current.left != null){
                queue.offer(current.left);
            } 
            if(current.right != null){
                queue.offer(current.right);
            }
            for(int i = 1;i < size;i++){
                Node next = queue.poll();
                if(next.left != null){
                    queue.offer(next.left);
                }
                if(next.right != null){
                    queue.offer(next.right);
                }
                current.next = next;
                current = next;
            }
            
        }
        return root;
    }
}
```

## [Medium] 117. Populating Next Right Pointers in Each Node II
**Link** : https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/description/
```
class Solution {
    public Node connect(Node root) {
        if(root == null){
            return root;
        }
        Queue<Node> queue = new LinkedList();
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            Node current = queue.poll();   
            if(current.left != null){
                queue.offer(current.left);
            } 
            if(current.right != null){
                queue.offer(current.right);
            }
            for(int i = 1;i < size;i++){
                Node next = queue.poll();
                if(next.left != null){
                    queue.offer(next.left);
                }
                if(next.right != null){
                    queue.offer(next.right);
                }
                current.next = next;
                current = next;
            }
            
        }
        return root;
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
===================================================================================
```
## [Easy] 404. Sum of Left Leaves
**Link** : https://leetcode.com/problems/sum-of-left-leaves/description/
```
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        int result = 0;
        Queue<TreeNode> queue = new LinkedList();
        if(root == null){
            return 0;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int len = queue.size();
            while(len > 0){
                TreeNode node = queue.poll();
                

                if(node.left != null ){
                    queue.offer(node.left);
                    if(node.left.left == null && node.left.right == null){
                        result += node.left.val;
                    }
                }if(node.right != null){
                    queue.offer(node.right);
                }
                len--;
            }
        }
        return result;
    }
}
```

## [Easy] 110. Balanced Binary Tree
**Link** : https://leetcode.com/problems/balanced-binary-tree/description/
```
class Solution {
    public boolean isBalanced(TreeNode root) {

        if(root == null){
            return true;
        }
        Stack<TreeNode> stack = new Stack();
        TreeNode prev = null;
        
        while(root != null || !stack.isEmpty()){
            while(root != null){
                stack.push(root);
                root = root.left;
            }
            TreeNode inNode = stack.peek();
            if(inNode.right == null || inNode.right ==  prev){
                if(Math.abs(getHeight(inNode.right) - getHeight(inNode.left)) > 1){
                    return false;
                    
                }
                stack.pop();
                root = null;
                prev = inNode;
            }else{
                root = inNode.right;
            }
        }
        return true;
    }

    public int getHeight(TreeNode root){
        int height = 0;
        Queue<TreeNode> queue = new LinkedList();
        if(root == null){
            return 0;
        }

        queue.offer(root);

        while(!queue.isEmpty()){
            int length = queue.size();
            height = height + 1;
            while(length > 0){
                TreeNode node = queue.poll();
                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
                length--;
            }
            
        }
        return height;

        
    }
}

```

## [Easy]257. Binary Tree Paths
**Link** : https://leetcode.com/problems/binary-tree-paths/description/
```
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> result = new ArrayList();
        if(root == null){
            return result;
        }
        List<Integer> path = new ArrayList();

        backtracking(root,path,result);
        return result;
    }

    void backtracking(TreeNode root,List<Integer> path,List<String> result){
        path.add(root.val);
        if(root.left == null && root.right == null){
            StringBuilder sb = new StringBuilder();
            for(int i = 0;i < path.size() - 1;i++){
                sb.append(path.get(i) + "->");
            }
            sb.append(path.get(path.size() - 1));
            result.add(sb.toString());
            return;
        }

        if(root.left != null){
            backtracking(root.left,path,result);
            path.remove(path.size() - 1);
        }
        if(root.right != null){
            backtracking(root.right,path,result);
            path.remove(path.size() - 1);
        }
    }
}
```
========================================================================================================
## [Medium] 513. Find Bottom Left Tree Value
**Link** : https://leetcode.com/problems/find-bottom-left-tree-value/description/
```
class Solution {
    public int findBottomLeftValue(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList();
        int result = 0;
        if(root == null){
            return result;
        }
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            int temp = size;
            while(size > 0){
                TreeNode node = queue.poll();

                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }

                if(size == temp && node.left == null && node.right == null){
                    result = node.val;
                }
                size--;
            }
        }
        return result;
    }    
}
```
## [Easy] 112. Path Sum
**Link** : https://leetcode.com/problems/path-sum/description/
```
class Solution {
    int result = 1;
    public boolean hasPathSum(TreeNode root, int targetSum) {
        return backtracking(root,targetSum);
        
    }

    boolean backtracking(TreeNode root,int targetSum){
        
        if(root == null){
            return false;
        }

        targetSum = targetSum - root.val;

        if(root.left == null & root.right == null){
            return targetSum == 0;
        }
        if(root.left != null){
            boolean left = backtracking(root.left,targetSum);
            if(left) {
                return true;
            }

        }
        if(root.right != null){
            boolean right = backtracking(root.right,targetSum);
            if(right) {
                return true;
            }
            
        }
        return false;
    }
}
```
## [Medium] 113. Path Sum II
https://leetcode.com/problems/path-sum-ii/description/
```
class Solution {
    List<List<Integer>> result = new ArrayList();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        if(root == null){
            return result;
        }
        backtracking(root,targetSum,new ArrayList());
        return result;
    }

    public void backtracking(TreeNode root, int targetSum,List<Integer> path){
        path.add(root.val);
        if(root.left == null && root.right == null){
            if(targetSum - root.val == 0){
                result.add(new ArrayList(path));
            }
        }

        if(root.left != null){
            backtracking(root.left,targetSum - root.val,path);
            path.remove(path.size() - 1);
        }
        
        if(root.right != null){
            backtracking(root.right,targetSum - root.val,path);
            path.remove(path.size() - 1);
        }
    }
}
```
## [Medium] 106. Construct Binary Tree from Inorder and Postorder Traversal
**Link** : https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/
```
class Solution {
    Map<Integer,Integer> map;
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        map = new HashMap();
        for(int i = 0;i < inorder.length;i++){
            map.put(inorder[i],i);
        }
        return findNum(inorder,0,inorder.length,postorder,0,postorder.length);


    }
    public TreeNode findNum(int[] inorder,int inBegin,int inEnd,
    int[] postorder,int postBegin,int postEnd){
        if(inBegin >= inEnd || postBegin >= postEnd){
            return null;
        }
        int rootIndex = map.get(postorder[postEnd - 1]);
        TreeNode root = new TreeNode(inorder[rootIndex]);
        int leftNodeLeft = rootIndex - inBegin;
        root.left = findNum(inorder,inBegin,rootIndex,postorder,postBegin,postBegin + leftNodeLeft);
        root.right = findNum(inorder,rootIndex + 1,inEnd,postorder,postBegin + leftNodeLeft, postEnd - 1);
        return root;
    }
}
```
## [Medium] 105. Construct Binary Tree from Preorder and Inorder Traversal
**Link** : https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/
```
class Solution {
    int preIndex;
    Map<Integer,Integer> inorderMap;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        preIndex = 0;
        inorderMap = new HashMap();
        for(int i = 0; i < inorder.length;i++){
            inorderMap.put(inorder[i],i);
        }
        return toTree(inorder,0,inorder.length,preorder,0,preorder.length);

    }

    public TreeNode toTree(int[] inorder,int inBegin, int inEnd,int[] preorder,int preBegin,int preEnd){
        if(inBegin >= inEnd || preBegin >= preEnd){
            return null;
        }
        int rootindex = inorderMap.get(preorder[preBegin]);
        TreeNode root = new TreeNode(inorder[rootindex]);
        int nodeCount = rootindex - inBegin;
        root.left = toTree(inorder,inBegin,rootindex,preorder,preBegin + 1,preBegin + nodeCount + 1);
        root.right = toTree(inorder,rootindex + 1,inEnd,preorder,preBegin + nodeCount + 1,preEnd);
        return root;
    }
}
```
===============================================================================================================================
## [Medium] 654. Maximum Binary Tree
**Link** : https://leetcode.com/problems/maximum-binary-tree/description/
```
class Solution {
    public TreeNode constructMaximumBinaryTree(int[] nums) {
        return findNum(nums,0,nums.length);
    }

    public TreeNode findNum(int[] nums,int left,int right){

        if(right - left < 1){
            return null;
        }

        if(right - left == 1){
            return new TreeNode(nums[left]);
        }
        int maxIndex = left;
        int maxValue = nums[left];

        for(int i = left + 1;i < right;i++){
            if(nums[i] > maxValue){
                maxValue = nums[i];
                maxIndex = i;
            }
        }

        TreeNode root = new TreeNode(maxValue);
        root.left = findNum(nums,left,maxIndex);
        root.right = findNum(nums,maxIndex + 1,right);
        return root;
    }
}
```
## [Easy] 700. Search in a Binary Search Tree
**Link** : https://leetcode.com/problems/search-in-a-binary-search-tree/description/
```
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if(root == null){
            return root;
            
        }

        if(root.val == val){
            return root;
        }
        TreeNode result = null;

        if(root.val > val){
            return searchBST(root.left,val);
        }
        return searchBST(root.right,val);
    }
}
```
