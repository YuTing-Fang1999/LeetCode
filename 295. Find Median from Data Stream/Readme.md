## 295. Find Median from Data Stream

### Description
For example, for arr = `[2,3,4]`, the median is `3`.  
For example, for arr = `[2,3]`, the median is `(2 + 3) / 2 = 2.5`.   

### Solution
Seperate arr to left and right.  
```
left = 1...median  
right = median....

left.top() = max(1...median) = median
right.top() = top = min(median....) = median
```
```cpp
void addNum(int num) {
    if(num > minimum of right) 
          1. add num to right
          2. move minimum of right to left
}
```

### Code
```cpp
class MedianFinder {
public:
    priority_queue< int > left; //top = max(1...median) 
    priority_queue< int, vector< int >, greater< int > > right; //top = min(median....)
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        (!right.empty() && num>right.top()) ? right.push(num) : left.push(num);
        while(left.size()+1 > right.size()){
            right.push(left.top());
            left.pop();
        }
        while(left.size()+1 <= right.size()){
            left.push(right.top());
            right.pop();
        }
    }
    double findMedian() {
        return (left.size() == right.size()) ? (left.top()+right.top())/2.0 : left.top();
    }
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```
