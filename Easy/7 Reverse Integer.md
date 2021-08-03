## Question Link:
https://leetcode.com/problems/reverse-integer/

## Question type: 
Math

## Question:
Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range [-231, 231 - 1], then return 0.

Assume the environment does not allow you to store 64-bit integers (signed or unsigned).

**Example 1:**
```
Input: x = 123
Output: 321
```
**Example 2:**
```
Input: x = -123
Output: -321
```
**Example 3:**
```
Input: x = 120
Output: 21
```
**Example 4:**
```
Input: x = 0
Output: 0
```

## Solution
main idea:
 1. use variable rev to save successfully reversed integer
 2. check if the value to go outside the signed 32-bit integer range 
    1) if new reversed intgter go out side the range then (new_rev-unit_digit) != pre_rev \*10
    2) to prevent overflow, we do all the calculation on the left hand side

```java
class Solution {
    public int reverse(int x) {
        int pre=0, rev=0;
        while(x!=0){
            rev= rev*10 + x%10;
            if((rev - x%10) / 10 != pre) return 0;  
            pre=rev;
            x=x/10;
        }
    return rev;
    }
}
```
