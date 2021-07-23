## Question Link:
https://leetcode.com/problems/roman-to-integer/

## Question type: 
String/Hash Table/Math

## Question:
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

* I can be placed before V (5) and X (10) to make 4 and 9. 
* X can be placed before L (50) and C (100) to make 40 and 90. 
* C can be placed before D (500) and M (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.

**Example 1:**
```
Input: s = "III"
Output: 3
```
**Example 2:**
```
Input: s = "IV"
Output: 4
```
**Example 3:**
```
Input: s = "IX"
Output: 9
```
**Example 4:**
```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```
**Example 5:**
```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```
## Solution
main idea:
 1. use map to store the sybol value
 2. traverse the string from back to front:
    1) if curr_value<curr_symbol, curr_value += curr_symbol
    2) if curr_value>curr_symbol, curr_value -= curr_symbol

```java
class Solution {
    public int romanToInt(String s) {
        HashMap<Character, Integer> check=new HashMap<>();
        check.put('I',1);
        check.put('V',5);
        check.put('X',10);
        check.put('L',50);
        check.put('C',100);
        check.put('D',500);
        check.put('M',1000);
        
        char[] chs=s.toCharArray();
        int num=check.get(chs[chs.length-1]);
        
        if(chs.length==1) return num;
        for(int i=chs.length-2; i>=0; i--){
            if(chs[i]==chs[i+1]) num+=check.get(chs[i]);
            else{
                if(num<check.get(chs[i])) num+=check.get(chs[i]);
                else num-=check.get(chs[i]);
            }
        }
        return num;
    }
}
```
