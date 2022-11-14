## 947. Most Stones Removed with Same Row or Column

## Description
* **A stone can be removed if it shares either the same row or the same column as another stone that has not been removed.**

* Given an array stones of length n where `stones[i] = [xi, yi]` represents the location of the ith stone, return the largest possible number of stones that can be removed.  

Example 1:
```
Input: stones = [[0,0],[0,1],[1,0],[1,2],[2,1],[2,2]]
Output: 5
Explanation: One way to remove 5 stones is as follows:
1. Remove stone [2,2] because it shares the same row as [2,1].
2. Remove stone [2,1] because it shares the same column as [0,1].
3. Remove stone [1,2] because it shares the same row as [1,0].
4. Remove stone [1,0] because it shares the same column as [0,0].
5. Remove stone [0,1] because it shares the same row as [0,0].
Stone [0,0] cannot be removed since it does not share a row/column with another stone still on the plane.
```
Example 2:
```
Input: stones = [[0,0],[0,2],[1,1],[2,0],[2,2]]
Output: 3
Explanation: One way to make 3 moves is as follows:
1. Remove stone [2,2] because it shares the same row as [2,0].
2. Remove stone [2,0] because it shares the same column as [0,0].
3. Remove stone [0,2] because it shares the same row as [0,0].
Stones [0,0] and [1,1] cannot be removed since they do not share a row/column with another stone still on the plane.
```
Example 3:
```
Input: stones = [[0,0]]
Output: 0
Explanation: [0,0] is the only stone on the plane, so you cannot remove it.
```
Example 4:
```
Input: stones = stones = [[0,1],[1,0],[1,1]]
Output: 2
```

## Solution
https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/solutions/787296/c-dfs-solution-18-lines-so-simple-explanations/
* Use `DFS` or `BFS` to find connectivity.   
* Consider indexes of each stone as an ID number.  
* Visit each ID if it hasn't been visited.(Note that we can go from stone A to stone B if and only if A and B have common row or column)
* Number of visited stones is the answer.  

## Code
```cpp
class Solution {
public:
    int DFS(vector<vector<int>>& stones, vector< bool > &visited, int idx, int n){
        visited[idx] = true;
        int cnt=0;
        for(int i=0;i<n;++i){
            // if connect with idx
            if(!visited[i] &&
                (stones[idx][0]==stones[i][0] || stones[idx][1]==stones[i][1]))
            {
                cnt+=(DFS(stones, visited, i, n)+1);
            }
        }
        return cnt;
    }
    int removeStones(vector<vector<int>>& stones) {
        vector< bool > visited(stones.size(), false);
        int n = stones.size();
        int cnt = 0;
        for(int i=0;i<n;++i){
            if(!visited[i]){
                cnt+=DFS(stones, visited, i, n);
            }
        }
        return cnt;
    }
};
```
