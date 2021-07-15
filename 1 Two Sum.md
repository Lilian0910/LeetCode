## Question Link:
https://leetcode.com/problems/print-in-order/

## Question type: 
Data Structure/ Array/ Hash Table

## Question:
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

## Solution
1. brute force (O(n^2))   
  two for-loops--> two pointers
```java
Arrays.sort(nums)
for (int i...){
  for (int j...){
    if(v1+v2>target) break;  
  }
}
```
2. binary search (O(n*logn))
```java
Arrays.sort(nums)
for (int i...){
  binary_search(target-nums[i])
}
```
3. hash map (O(n))
```java
class Solution {   
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> m=new HashMap<Integer, Integer>();
        int[] res=new int[2];
        for(int i=0; i<nums.length; i++){
            if(m.containsKey(nums[i])){
                res[0]=m.get(nums[i]);
                res[1]=i;
            } else{
               m.put((target-nums[i]), i); 
            }
        }
        return res;
    }
}
```
        
