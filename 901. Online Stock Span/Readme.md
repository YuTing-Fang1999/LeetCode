## 901. Online Stock Span
## Descroption
The span of the stock's price today is defined as the maximum number of consecutive days (starting from today and going backward) for which the stock price was less than or equal to today's price.  
* For example, if the price of a stock over the next 7 days were `[100,80,60,70,60,75,85]`,   
  then the stock spans would be `[1,1,1,2,1,4,6]`.   
* 從現在往前取，直到price大於我，所經過的span

## Solution
When I am the larger price, I will be the break point, so the price less than or equal to me can be delete.

## Code
```cpp
class StockSpanner {
public:
    int total_span = 0;
    stack< pair< int, int > > S;
    StockSpanner() {
        
    }
    //從現在往前取，直到price大於我，所經過的span
    int next(int price) {
        //比我小的資料可以捨去，因為之後會從我開始斷開
        //the price less than or equal to me can be delete
        while(!S.empty() && S.top().first <= price) S.pop();
        //如果還是有比我高的
        //have a price larger than me
        if(!S.empty()){
            int last_span = S.top().second;
            ++total_span;
            S.push({price, total_span});
            return total_span-last_span;
        }
        //我最高
        //I am the maximum
        ++total_span;
        S.push({price, total_span});
        return total_span;
    }
};

/**
 * Your StockSpanner object will be instantiated and called as such:
 * StockSpanner* obj = new StockSpanner();
 * int param_1 = obj->next(price);
 */

```
