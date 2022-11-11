```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        next_permutation(nums.begin(), nums.end());
    }
};
```
### next_permutation 會找出下一個升序排列
### Ex: Permutation of [1, 2, 3]
```
1, 2, 3
1, 3, 2
2, 1, 3
2, 3, 1
3, 1, 2
3, 2, 1
```

https://medium.com/@ChYuan/leetcode-no-31-132-pattern-%E5%BF%83%E5%BE%97-medium-e02ecf53817f
https://github.com/YuTing-Fang1999/CPE/tree/main/UVA12218
### next_permutation
```
string str="abcd";
do{
  ...
}while(next_permutation(str.begin(),str.end()));
```
結果
```
abcd
abdc
acbd
acdb
adbc
adcb
bacd
badc
bcad
bcda <=如果str為"bcda"，那麼會從這裡開始列(個數為15)
bdac
bdca
cabd
cadb
cbad
cbda
cdab
cdba
dabc
dacb
dbac
dbca
dcab
dcba <=如果str為"dcba"，那麼會從這裡開始(個數為1)
24
```
