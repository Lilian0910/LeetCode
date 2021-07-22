## Question Link:
https://leetcode.com/problems/longest-common-prefix/

## Question type: 
String

## Question:
Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

## Solution
main idea:
 1. choose the first string
 2. see the subtring exits in the other string or not-->string2.indexOf(substring)
    1) if not (the index is -1) then reduce the substring from the end
    2) if exits ( the incex is 0) check the next string
 3. return the substring if exits
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0)    return "";
        String pre = strs[0]; //the substring
        int i = 1;
        while(i < strs.length){
            while(strs[i].indexOf(pre) != 0) //if the next string doesn't contains the same substring
                pre = pre.substring(0,pre.length()-1); //reduce the substring from the end by one character each time
            i++;
        }
    return pre;
    }
}
```
