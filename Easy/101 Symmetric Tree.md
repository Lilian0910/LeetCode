## Question Link:
https://leetcode.com/problems/symmetric-tree/

## Question type: 
DFS/ Binary Tree/ BFS
## Question:
Given the root of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

**Example 1:**  
![image](https://user-images.githubusercontent.com/59671980/128645246-6e2950eb-2552-4ac2-b253-180a489b3096.png)
```
Input: root = [1,2,2,3,4,4,3]
Output: true
```
**Example 2:**
![image](https://user-images.githubusercontent.com/59671980/128645256-e4670f04-cc44-4650-9373-97779aae60bb.png)

```
Input: root = [1,2,2,null,3,null,3]
Output: false
```

## Solution
Main idea:
1. check left child & right child:
    1) if one of them is null but the other is not, then we should return false. If both of them are null, then we should return true.
    2) we also need the check the values of left child and right child
2. let left child goes left and right child goes right && left child goes right and right child goes left
```java
//recursion
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return root==null || helper(root.left, root.right);
    }
    public static boolean helper(TreeNode left, TreeNode right){
        if(left==null || right==null) return left==right;
        if(left.val != right.val) return false;
        return helper(left.left, right.right) && helper(left.right, right.left);
    }
}

//iteration
public boolean isSymmetric(TreeNode root) {
    if(root==null)  return true;
    
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode left, right;
    if(root.left!=null){
        if(root.right==null) return false;
        stack.push(root.left);
        stack.push(root.right);
    }
    else if(root.right!=null){
        return false;
    }
        
    while(!stack.empty()){
        if(stack.size()%2!=0)   return false;
        right = stack.pop();
        left = stack.pop();
        if(right.val!=left.val) return false;
        
        if(left.left!=null){
            if(right.right==null)   return false;
            stack.push(left.left);
            stack.push(right.right);
        }
        else if(right.right!=null){
            return false;
        }
            
        if(left.right!=null){
            if(right.left==null)   return false;
            stack.push(left.right);
            stack.push(right.left);
        }
        else if(right.left!=null){
            return false;
        }
    }
    
    return true;
}
```
