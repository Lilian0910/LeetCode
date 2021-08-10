## Question Link:
https://leetcode.com/problems/binary-tree-right-side-view/

## Question type: 
DFS/ Binary Tree/ BFS
## Question:
Given the root of a binary tree, imagine yourself standing on the **right side** of it, return the values of the nodes you can see ordered from top to bottom.

**Example 1:**  
![image](https://user-images.githubusercontent.com/59671980/128879267-c164778b-5f10-4f1a-ab38-ef7f8dfa0384.png)
```
Input: root = [1,2,3,null,5,null,4]
Output: [1,3,4]
```
**Example 2:**
```
Input: root = [1,null,3]
Output: [1,3]
```
**Example 3:**
```
Input: root = []
Output: []
```

## Solution
Main idea:
1. checks the RIGHT node first and then the LEFT
2. the line to check `level == result.size()` makes sure the first element of that level will be added to the result list
3. if reverse the visit order, that is first LEFT and then RIGHT, it will return the left view of the tree.
```java
public class Solution {
    List<Integer> result = new ArrayList<Integer>();
    
    public List<Integer> rightSideView(TreeNode root) {
        rightView(root, 0);
        return result;
    }
    
    public void rightView(TreeNode root, int level){
        if(root == null) return;
        if(level == result.size()) result.add(root.val);
        
        rightView(root.right, level + 1);
        rightView(root.left, level + 1);      
    }
}
```
