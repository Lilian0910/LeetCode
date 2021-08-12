## Question Link:
https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/

## Question type: 
DFS/ Binary Tree/ BFS
## Question:
Given the root of a binary tree, the value of a target node target, and an integer k, return an array of the values of all nodes that have a distance k from the target node.

You can return the answer in any order.

**Example 1:**  
<img src="https://user-images.githubusercontent.com/59671980/129122781-f31449eb-f7f5-494d-849e-230fb1342911.png" width="40%" height="40%">
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, k = 2
Output: [7,4,1]
Explanation: The nodes that are a distance 2 from the target node (with value 5) have values 7, 4, and 1.
```
**Example 2:**
```
Input: root = [1], target = 1, k = 3
Output: []
```

## Solution
Main idea:    
**Method 1: use HashMap**
1. build a undirected graph using treenodes as vertices, and the parent-child relation as edges
2. do BFS with source vertice (target) to find all vertices with distance K to it.
![image](https://user-images.githubusercontent.com/59671980/129122592-7fd563d1-66b1-4f52-94eb-c68064cc477d.png)
```java
//a Queue will make a BFS, a Stack will make a DFS
class Solution {
    Map<TreeNode, List<TreeNode>> map = new HashMap();
    public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
        List<Integer> res = new ArrayList<Integer> ();
        if (root == null || K < 0) return res;
        buildMap(root, null); 
        if (!map.containsKey(target)) return res;
        Set<TreeNode> visited = new HashSet<TreeNode>();
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(target);
        visited.add(target);
        while (!q.isEmpty()) {
            int size = q.size();
            if (K == 0) {
                for (int i = 0; i < size ; i++) res.add(q.poll().val);
                return res;
            }
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                for (TreeNode next : map.get(node)) {
                    if (visited.contains(next)) continue;
                    visited.add(next);
                    q.add(next);
                }
            }
            K--;
        }
        return res;
    }
    
    private void buildMap(TreeNode node, TreeNode parent) {
        if (node == null) return;
        if (!map.containsKey(node)) {
            map.put(node, new ArrayList<TreeNode>());
            if (parent != null)  { map.get(node).add(parent); map.get(parent).add(node) ; }
            buildMap(node.left, node);
            buildMap(node.right, node);
        }
    }    
}
```
**Method 2: No HashMap**    
kind of like clone the tree, in the meanwhile add a parent link to the node
```java
class Solution {
    private GNode targetGNode;
    
    private class GNode {
        TreeNode node;
        GNode parent, left, right;
        GNode (TreeNode node) {
            this.node = node;
        }
    }           
    
    public List<Integer> distanceK(TreeNode root, TreeNode target, int K) {
        List<Integer> res = new ArrayList<Integer> ();
        if (root == null || K < 0) return res;
        cloneGraph(root, null, target);
        if (targetGNode == null) return res;
        Set<GNode> visited = new HashSet<GNode>();
        Queue<GNode> q = new LinkedList<GNode>();
        q.add(targetGNode);
        visited.add(targetGNode);
        while (!q.isEmpty()) {
            int size = q.size();
            if (K == 0) {
                for (int i = 0; i < size ; i++) res.add(q.poll().node.val);
                return res;
            }
            for (int i = 0; i < size; i++) {
                GNode gNode = q.poll();
                if (gNode.left != null && !visited.contains(gNode.left)) { visited.add(gNode.left); q.add(gNode.left); }
                if (gNode.right != null && !visited.contains(gNode.right)) { visited.add(gNode.right); q.add(gNode.right); }
                if (gNode.parent != null && !visited.contains(gNode.parent)) { visited.add(gNode.parent); q.add(gNode.parent); }
            }
            K--;
        }
        return res;
    }
    
    private GNode cloneGraph(TreeNode node, GNode parent, TreeNode target) {
        if (node == null) return null;
        GNode gNode = new GNode(node);
        if (node == target) targetGNode = gNode;
        gNode.parent = parent;
        gNode.left = cloneGraph(node.left, gNode, target);
        gNode.right = cloneGraph(node.right, gNode, target);
        return gNode;
    }
}
```
