## Question Link:
https://leetcode.com/problems/subtree-of-another-tree/

## Question type: 
DFS/ Binary Tree/ Hash Function/ String Matching
## Question:
Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

**Example 1:**  
![image](https://user-images.githubusercontent.com/59671980/128645755-d1b9101d-14e6-4228-a649-f76b75386f55.png)
```
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true
```
**Example 2:**
![image](https://user-images.githubusercontent.com/59671980/128645758-2216de8e-755d-4626-9f53-1f253e89a135.png)
```
Input: root = [3,4,5,1,2,null,null,null,null,0], subRoot = [4,1,2]
Output: false
```
**Constraints:**
* The number of nodes in the root tree is in the range [1, 2000].
* The number of nodes in the subRoot tree is in the range [1, 1000].
* -104 <= root.val <= 104
* -104 <= subRoot.val <= 104
## Solution
main idea:
1. Two trees are said to be identical if their **root values are same** and **their left and right subtrees are identical**.
2. compare left child and right child with subRoot
```java
//recursion
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if(root==null) return false;
        if (isSame(root, subRoot)) return true;
        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);
    }
    public boolean isSame(TreeNode root, TreeNode subRoot){
        if(root==null || subRoot==null) return root==subRoot;
        if(root.val != subRoot.val) return false;
        return isSame(root.left,subRoot.left) && isSame(root.right, subRoot.right);
    }
}
```
