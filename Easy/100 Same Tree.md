## Question Link:
https://leetcode.com/problems/same-tree/

## Question type: 
DFS/ Binary Tree/ BFS
## Question:
Given the roots of two binary trees p and q, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

**Example 1:**  
![image](https://user-images.githubusercontent.com/59671980/128877856-ae1125e1-70de-4645-9a41-58bfe8c108ca.png)
```
Input: p = [1,2,3], q = [1,2,3]
Output: true
```
**Example 2:**
![image](https://user-images.githubusercontent.com/59671980/128877900-a3e88c82-016e-4989-b117-cb3091e81603.png)
```
Input: p = [1,2], q = [1,null,2]
Output: false
```
**Example 3:**
![image](https://user-images.githubusercontent.com/59671980/128877990-1d895e2b-2f46-467f-ad7a-f193a03fa42d.png)
```
Input: p = [1,2,1], q = [1,1,2]
Output: false
```

## Solution
Main idea:
1. base case: if one of the nodes is null, check if they are the same-->same return true, different return false
2. check whether p.val==q.val, if same check left child and right child; if not, return false.
```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null || q==null) return p==q;
        if(p.val == q.val)
            return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
        return false;
    }
}
```
