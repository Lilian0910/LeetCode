## Question Link:
https://leetcode.com/problems/binary-tree-inorder-traversal/

## Question type: 
DFS/ Binary Tree/ Stack
## Question:
Given the root of a binary tree, return the inorder traversal of its nodes' values.

**Example 1:**  
![img1](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)
```
Input: root = [1,null,2,3]
Output: [1,3,2]
```
**Example 2:**
```
Input: root = []
Output: []
```
**Example 3:**
```
Input: root = [1]
Output: [1]
```
**Example 4:**
![img2](https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg)
```
Input: root = [1,2]
Output: [2,1]
```
**Example 5:**
![image](https://user-images.githubusercontent.com/59671980/128639142-0395cb78-f7df-44fb-83ab-8e7a1ac8a74c.png)

```
Input: root = [1,null,2]
Output: [1,2]
```
## Solution

```java
//recursion
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res=new ArrayList<>();
        helper(root, res);
        return res;
    }
    public static void helper(TreeNode root, List res){
        if (root != null) {
            helper(root.left, res);
            res.add(root.val);
            helper(root.right, res);
        }
    }
}

//iteration
public List<Integer> inorderTraversal(TreeNode root) {
   Stack<TreeNode> stack = new Stack<>();
   List<Integer> ret = new ArrayList<>();
   while (true) {
       while (root != null) {
           stack.push(root);
           root = root.left;
       }
       if (stack.isEmpty()) {
           break;  // no node left
       }
       TreeNode node = stack.pop();
       ret.add(node.val);
       root = node.right;
   }
   return ret;
}
```
