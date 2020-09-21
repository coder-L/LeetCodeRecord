# 题目
实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。

 

* 示例:
>输入: 2.00000, 10<br>
输出: 1024.00000

>输入: 2.10000, 3<br>
输出: 9.26100

>输入: 2.00000, -2<br>
输出: 0.25000<br>
解释: 2-2 = 1/22 = 1/4 = 0.25

 

* 说明:
    -100.0 < x < 100.0
    n 是 32 位有符号整数，其数值范围是 [−2<sup>31</sup>, 2<sup>31</sup> − 1] 。

* 思路：分治，递归计算整数幂，同时注意n的取值范围，当n为负数时直接转为整数可能会有错误（负数的范围比整数的范围大1），因此需要特殊处理一下
* 代码:
    ```C++
    class Solution {
    public:
        double myPow(double x, int n) {
            if(n==0)
            {
                return 1.0;
            }
            if(n==1)
            {
                return x;
            }
            if(n<0)
            {
                ++n;
                n = -n;
                x = 1.0/x;
                double tmp = myPow(x,n/2);
                if(n%2==0)
                {
                    return tmp * tmp * x;
                }
                else
                {
                    return tmp*tmp*x*x;
                }
            }
            else
            {
                double tmp = myPow(x,n/2);
                if(n%2==0)
                {
                    return tmp * tmp;
                }
                else
                {
                    return tmp * tmp *x;
                }
            }
        }
    };
    ```

