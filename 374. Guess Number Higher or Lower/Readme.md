## 374. Guess Number Higher or Lower

## Description
We are playing the Guess Game. The game is as follows:

I pick a number from `1` to `n`. You have to guess which number I picked.

Every time you guess wrong, I will tell you whether the number I picked is higher or lower than your guess.

You call a pre-defined API `int guess(int num)`, which returns three possible results:

* -1: Your guess is higher than the number I picked (i.e. num > pick).
* 1: Your guess is lower than the number I picked (i.e. num < pick).
* 0: your guess is equal to the number I picked (i.e. num == pick).
Return the number that I picked.

```cpp
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

class Solution {
public:
    int guessNumber(int n) {
        long long int low=1, high=n;
        long long int mid=(low+high)/2;
        int res=guess(mid);
        while(res!=0){
            if(res==1) low=mid+1;
            else high=mid-1;
            mid=(low+high)/2;
            res=guess(mid);
        }
        return mid;
    }
};
```
