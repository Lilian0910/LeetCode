## Question Link:
https://leetcode.com/problems/minimum-distance-between-bst-nodes/

## Question type: 
DFS/ Binary Tree/ BFS
## Question:
Given the root of a Binary Search Tree (BST), return the minimum difference between the values of any two different nodes in the tree.

**Example 1:**  
![image](https://user-images.githubusercontent.com/59671980/128949975-a7a844ec-f48b-4e3b-b5a6-6f52d1e8c660.png)

```
Input: root = [4,2,6,1,3]
Output: 1
```
**Example 2:**
![image](https://user-images.githubusercontent.com/59671980/128949988-b10ff72f-13b8-44a7-89ee-7decf11b3e30.png)

```
Input: root = [1,0,48,null,null,12,49]
Output: 1
```

## Solution
Use inOrder traverse the tree and compare the delta between each of the adjacent values. 
It's guaranteed to have the correct answer because it is a BST thus inOrder traversal values are sorted.
1. it will go left first untill get to the leaf, since it doesn't have left child. (in example 1, it's Node(1))
    1)  since now the value of `val` is still null 
    2)  it will skip the second if condition and give `left_leaf.val` to `val`
    3)  then it will return to the second if condition and the `val` will be `left_leaf.val`. 
2. When it goes to right, `val` will be `preRoot.val`

```java
class Solution {
    Integer val=null, min=Integer.MAX_VALUE;
    public int minDiffInBST(TreeNode root) {
        if (root.left != null) minDiffInBST(root.left);
        if (val != null) min = Math.min(min, root.val - val);
        val = root.val;
        if (root.right != null) minDiffInBST(root.right);
        return min;
    }
    
}
```
