## Question Link:
https://leetcode.com/problems/valid-parentheses/

## Question type: 
String/Stack

## Question:
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
 

**Example 1:**
```
Input: s = "()"
Output: true
```
**Example 2:**
```
Input: s = "()[]{}"
Output: true
```
**Example 3:**
```
Input: s = "(]"
Output: false
```
**Example 4:**
```
Input: s = "([)]"
Output: false
```
**Example 5:**
```
Input: s = "{[]}"
Output: true
```

## Solution
```java
class Solution {
    public boolean isValid(String s) {
        if (s.isEmpty()) return true;
        Stack<Character> stack = new Stack<Character>();
        for (int i=0; i<s.length(); i++){
            char c=s.charAt(i);
            if (c == '{' || c == '(' || c == '['){
                stack.push(c);
            }
            if (c == '}' || c == ')' || c == ']'){
                if(stack.isEmpty()) return false;
                char last=stack.peek();
                if ((c == '}' && last == '{') || (c == ']' && last == '[') || (c == ')' && last == '('))
                    stack.pop();
                else return false;
            }
        }
        return stack.isEmpty();
    }
}
```
