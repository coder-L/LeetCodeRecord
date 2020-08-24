# 题目
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

* 示例：

>输入：n = 2<br>
输出：2

>输入：n = 7<br>
输出：21

>输入：n = 0<br>
输出：1

提示：

    0 <= n <= 100


* 思路：动态规划，由于只和之前两个结果有关系，因此可以只保存之前的两个结果，节省空间
* 代码：
    ```C++
    class Solution {
    public:
        int numWays(int n) {
            int prepre=1;
            int pre=2;
            if(n==1)
            {
                return prepre;
            }
            if(n==2)
            {
                return pre;
            }
            int result=1;
            for(int i=3;i<=n;++i)
            {
                result = (prepre%1000000007+pre%1000000007)%1000000007;
                prepre = pre%1000000007;
                pre = result;
            }
            return result;
        }
    };
    ```