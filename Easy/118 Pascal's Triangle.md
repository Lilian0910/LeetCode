## Question Link:
https://leetcode.com/problems/pascals-triangle/

## Question type: 
Array/ Dynamic Programming
## Question:
Given an integer numRows, return the first numRows of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:
![image](https://user-images.githubusercontent.com/59671980/129096806-6ea39e0d-3cf9-4a65-8621-865e0acde4cc.png)

**Example 1:**  

```
Input: numRows = 5
Output: [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]
```
**Example 2:**
```
Input: numRows = 1
Output: [[1]]
```


## Solution
Main idea:
![image](https://user-images.githubusercontent.com/59671980/129097234-5fbf191b-916f-4368-8f32-819d18f1ca45.png)
```java
class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        if (numRows==0) return res;
        
        ArrayList<Integer> row = new ArrayList<Integer>();
        for(int i=0; i<numRows; i++){
            row.add(0,1); //insert 1 in the front of list
            for(int j=1; j<i; j++){ 
            //change val to sum from the second
            //j can't point to the last num
                row.set(j, row.get(j)+row.get(j+1));
            }
            res.add(new  ArrayList<Integer>(row));
        }
        return res;
    }
}
```
