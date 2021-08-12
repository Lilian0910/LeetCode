## Question Link:
https://leetcode.com/problems/increasing-order-search-tree/

## Question type: 
DFS/ Binary Tree/ BFS
## Question:
Given the root of a binary search tree, rearrange the tree in in-order so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only one right child.
**Example 1:**      
<img src="https://user-images.githubusercontent.com/59671980/129123925-500a80cb-0a3a-41ac-8bf6-c4e53a465cf3.png" width="50%" height="50%">
```
Input: root = [5,3,6,2,4,null,8,1,null,null,null,7,9]
Output: [1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]
```
**Example 2:**    
<img src="https://assets.leetcode.com/uploads/2020/11/17/ex2.jpg" width="50%" height="50%">
```
Input: root = [5,1,7]
Output: [1,null,5,null,7]
```

## Solution
Main idea:
1. Recursively call function `increasingBST(TreeNode root, TreeNode tail)`,  `tail` is its next node in inorder
2. If root == null, the head will be `tail`, so we return `tail` directly.
3. we recursively call increasingBST(root.left, root), change left subtree into the linked list + current node.
4. we recursively call increasingBST(root.right, tail), change right subtree into the linked list + tail.
5. Since it's single linked list, so we set root.left = null.    
**Complexity**    
O(N) time traversal of all nodes    
O(height) space
```java
class Solution {
    public TreeNode increasingBST(TreeNode root) {
        return increasingBST(root, null);
    }

    public TreeNode increasingBST(TreeNode root, TreeNode tail) {
        if (root == null) return tail;
        TreeNode res = increasingBST(root.left, root);
        root.left = null;
        root.right = increasingBST(root.right, tail);
        return res;
    }

}
```
