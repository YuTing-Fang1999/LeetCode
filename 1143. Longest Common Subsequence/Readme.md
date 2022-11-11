## 1143. Longest Common Subsequence

## Description
### Example 1:
```
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```
### Example 2:
```
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
```

## Solution
```
X = <x1, x2, ...xi > i characters
Y = <y1, y2, ...yj > j characters
//c[i,j] = LCS(xi, yj) 
if xi==yj: c[i, j] = c[i-1, j-1]+1 (add characters at the same time)
if xi!=yj: c[i, j] = max(c[i, j-1], c[i-1, j]) (characters from X or characters from Y)
```
### Example
```
X = ABCDC
Y = ACCBD
c[2, 3] = LCS(AB, ACC) = max(LCS(A, ACC), LCS(AB, AC)) (add x2 or add y3)
c[2, 4] = LCS(AB, ACCB) = LCS(A, ACC)+1 = c[1, 3]+1
```
有點像是coin exchange逆推的概念  

### Code
```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        //c[i,j] = LCS(xi, yj)
        int c[text1.size()+1][text2.size()+1];
        memset(c, 0, sizeof(c));
        for(int i=1;i<=text1.size();++i){
            for(int j=1;j<=text2.size();++j){
                if(text1[i-1]==text2[j-1]){
                    c[i][j] = c[i-1][j-1]+1;
                }
                else{
                    c[i][j]  = max(c[i-1][j], c[i][j-1]);
                }
            }
        }
        return c[text1.size()][text2.size()];
    }
};
```
