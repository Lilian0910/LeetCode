## Question Link:
https://leetcode.com/problems/range-sum-of-bst/

## Question type: 
Deep-first Search/BST

## Question:
Given the root node of a binary search tree and two integers `low` and `hig`h, return the sum of values of all nodes with a value in the inclusive range `[low, high]`.  

**Example 1:**
![img1](https://assets.leetcode.com/uploads/2020/11/05/bst1.jpg)
```
Input: root = [10,5,15,3,7,null,18], low = 7, high = 15
Output: 32
Explanation: Nodes 7, 10, and 15 are in the range [7, 15]. 7 + 10 + 15 = 32.
```
**Example 2:**
![img2](https://assets.leetcode.com/uploads/2020/11/05/bst2.jpg)
```
Input: root = [10,5,15,3,7,13,18,1,null,6], low = 6, high = 10
Output: 23
Explanation: Nodes 6, 7, and 10 are in the range [6, 10]. 6 + 7 + 10 = 23.
``` 
**Constraints:**
* The number of nodes in the tree is in the range [1, 2 * 104].
* 1 <= Node.val <= 105
* 1 <= low <= high <= 105
* All Node.val are unique.

## Solution
main idea:
 1. base case: root==null
 2. left branch and right branch condition
 3. return result

```java
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
    public int rangeSumBST(TreeNode root, int low, int high) {
        if (root == null) return 0; // base case.
        if (root.val < low) return rangeSumBST(root.right, low, high); // left branch excluded.
        if (root.val > high) return rangeSumBST(root.left, low, high); // right branch excluded.
        return root.val + rangeSumBST(root.right, low, high) + rangeSumBST(root.left, low, high); // count in both children.
    }
}
```
