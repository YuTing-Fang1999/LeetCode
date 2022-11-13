## 151. Reverse Words in a String
## Description
Example 1:
```
Input: s = "the sky is blue"
Output: "blue is sky the"
```
Example 2:
```
Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```
Example 3:
```
Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
 ```

Constraints:
```
1 <= s.length <= 104
s contains English letters (upper-case and lower-case), digits, and spaces ' '.
There is at least one word in s.
```

## Code
```cpp
class Solution {
public:
    string reverseWords(string s) {
        stringstream ss(s);
        string w;
        stack< string > words;
        while(ss>>w) words.push(w);

        string ans=words.top();
        words.pop();
        while(!words.empty()){
            ans+=" ";
            ans+=words.top();
            words.pop();
        }
        return ans;
    }
};
```
