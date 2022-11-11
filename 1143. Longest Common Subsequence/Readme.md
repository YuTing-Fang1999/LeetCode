## 1143. Longest Common Subsequence

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
if xi==yj: c[i, j] = c[i-1, j-1]+1 (Add characters at the same time)
if xi!=yj: c[i, j] = max(c[i, j-1], c[i-1, j]) (Drop characters of X Drop characters of Y)
```
### Example
```
X = ABCDC
Y = ACCBD
c[2, 2] = LCS(AB, AC) = 1
c[3, 3] = c[2, 2]+1 = 2 = LCS(ABC, ACC)
```


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
