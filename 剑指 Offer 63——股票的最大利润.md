# 题目
假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？<br>

限制：<br>
0 <= 数组长度 <= 10^5

* 示例：

>输入: [7,1,5,3,6,4]<br>
输出: 5<br>
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。

>输入: [7,6,4,3,1]<br>
输出: 0<br>
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。


* 思路：记录每天股票价格的变化，则问题转化为求最大子数组问题


* 代码：
    ```C++
    class Solution {
    public:
        int maxProfit(vector<int>& prices) {
            int length1 = prices.size();
            if(length1 <2)
            {
                return 0;
            }
            int result = 0;
            vector<int> change(length1-1);
            int length2 = change.size();
            for(int n=0;n<length2;++n)
            {
                change[n] = prices[n+1]-prices[n];
            }
            int curmax= -1;
            for(int n=0;n<length2;++n)
            {
                if(curmax<0)
                {
                    curmax = change[n];
                }
                else
                {
                    curmax+=change[n];
                }
                if(curmax>result)
                {
                    result = curmax;
                }
            }
            return result;

        }
    };
    ```