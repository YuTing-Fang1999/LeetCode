## 215. Kth Largest Element in an Array
## Description
Given an integer array nums and an integer k, return the kth largest element in the array.  

Note that it is the kth largest element in the sorted order, not the kth distinct element.  

You must solve it in `O(n)` time complexity.  

Example 1:
```
Input: nums = [3,2,1,5,6,4], k = 2
Output: 5
```

## Solution 
### Quick Select (Quick Sort的變形)
1. random chose a pivot O
2. Quick Sort
3. [ , , , ,O, , , ,] left<O and O<right
4. if O == k return
5. else if O < k, find right part, if  O > k, find left part      

https://www.youtube.com/watch?v=zOmIKYKpzB4   

Input: nums = [3,2,1,5,6,4], k = 2  
```
k = 2 (從右數到左第2個) 
idx = nums.size()-k = 4 (從左數到右第5個)

O  >       <
[3,2,1,5,6,4]
O    >   <
[3,2,1,5,6,4]
O      x
[3,2,1,5,6,4]
 O   <   >
[3,2,1,5,6,4] 
right<left, swap(O, <)
[1,2,3,5,6,4]

< = 2, find right part
       O > <
[1,2,3,5,6,4]
       O < >
[1,2,3,5,4,6]
swap(O, <)
[1,2,3,4,5,6]
< = 5, return
```
Input: nums = [3,3,3,3,4,3,3,3,3], k = 3
```
k = 9-3=6

range = [0,8]
 O >             <
[3,3,3,3,4,3,3,3,3] 1 8
 O   >         <
[3,3,3,3,4,3,3,3,3] 2 7
 O     >     <
[3,3,3,3,4,3,3,3,3] 3 6
 O       > <
[3,3,3,3,4,3,3,3,3] 4 5
 O       x 
[3,3,3,3,4,3,3,3,3] 4 4
 O     < > 
[3,3,3,3,4,3,3,3,3] 4 3
pos = 3

range = [4,8]
         O >     < 
[3,3,3,3,4,3,3,3,3] 5 8
         O   >   < 
[3,3,3,3,4,3,3,3,3] 6 8
         O     > <   
[3,3,3,3,4,3,3,3,3] 7 8
         O       x   
[3,3,3,3,4,3,3,3,3] 8 8
         O       < >   
[3,3,3,3,4,3,3,3,3] 8 9
pos = 8

range = [4,7]
         O
[3,3,3,3,4,3,3,3,3]

         O >   <
[3,3,3,3,4,3,3,3,3]
         O   > <
[3,3,3,3,4,3,3,3,3]
         O     x
[3,3,3,3,4,3,3,3,3]
         O     < >
[3,3,3,3,4,3,3,3,3]
pos = 7

range = [4,6]
         O > <
[3,3,3,3,4,3,3,3,3]
...
         O   < >
[3,3,3,3,4,3,3,3,3]
pos = 6
return nums[pos]
```

## Code
```cpp
class Solution {
 public :
     int findKthLargest(vector< int >& nums, int k) {
         // kth from right to left
         // nums.size()-k+1 = kth from left to right (left begin from 1)
         // nums.size()-k = kth from left to right (left begin from 0)
         k = nums.size()-k;
         int left = 0 , right = nums.size() - 1 ;
         int pos = partition(nums, left, right);
         // change the range of left and right
         while (pos != k) {
             if(pos < k) left = pos+1;
             else right = pos-1;
             pos = partition(nums, left, right);
        }
        return nums[pos];
    }
    //[less, O, larger]
    int partition(vector< int >& nums, int left, int right) {
         int pivot = nums[left]; 
         int pivot_idx = left;
         
         ++left;
         while(left<=right){
             if(nums[left] > pivot && nums[right] < pivot){
                 swap(nums[left], nums[right]);
                 left++;
                 right--;
             }
             
             if(nums[left] <= pivot) left++;
             if(nums[right] >= pivot) right--;
         }
         swap(nums[pivot_idx], nums[right]);
         return right;
    }
};
```
debug de 超久==  
left和right的範圍要改!!!
```cpp
\\原bug
while (pos != k) {
     if(pos < k) pos = partition(nums, pos+1, right);
     else pos = partition(nums, left, pos-1);
}
\\這樣範圍不會縮小!
```
