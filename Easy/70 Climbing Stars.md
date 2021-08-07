## Question Link:
https://leetcode.com/problems/climbing-stairs/

## Question type: 
Math/ Dynamic Programming/Memoization

## Question:
You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Example 1:**
```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
**Example 2:**
```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## Solution
main idea:
 1. base case:
    1) if n=0, there's 0 way-->return 0
    2) if n=1, there's 1 way--> return 1
    3) if n=2, there're 2 ways(2, 1+1)--> return 2
 2. the others are the combination of n=1 & n=2, beacause if we know the way to gent to the point n-1 & n-2 then the total way to get to the point n is n1 + n2. From the n-1 point, we can take one single step to reach n. And from the n-2 point, we could take two steps to get there.

```java
public class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n + 1];
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
          dp[i] = dp[i-1] + dp[i - 2];
        }
        return dp[n];
    }
}

```
