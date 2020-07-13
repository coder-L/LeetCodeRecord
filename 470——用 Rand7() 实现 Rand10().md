# 题目
已有方法 rand7 可生成 1 到 7 范围内的均匀随机整数，试写一个方法 rand10 生成 1 到 10 范围内的均匀随机整数。

不要使用系统的 Math.random() 方法。


* 思路1：将10表示为2进制位，如果rand7返回的结果不是7，则判断为奇数还是偶数，如果为奇数则对应位为0，否则对应位为1，最后判断result是否满足大于0小于10，满足则返回，否则重新计算
* 代码1：
    ```C++
    // The rand7() API is already defined for you.
    // int rand7();
    // @return a random integer in the range 1 to 7

    class Solution {
    public:
        int rand10() {
            map<int ,int> data;
            data[0]=1;
            data[1]=2;
            data[2]=4;
            data[3]=8;
            int result=0;
            for(int n=0;n<4;++n)
            {
                int rand=rand7();
                while(rand==7)
                {
                    rand=rand7();
                }
                result = rand%2==0?data[n]+result:result;
            }
            if(result<=10 && result >0)
            {
                return result;
            }
            else
            {
                return rand10();
            }
        }
    };
    ```

* 思路2：
>已知 rand_N() 可以等概率的生成[1, N]范围的随机数
那么：<br>
(rand_X() - 1) × Y + rand_Y() ==> 可以等概率的生成[1, X * Y]范围的随机数<br>
即实现了 rand_XY()。

则 (rand7()-1) × 7 + rand7()  ==> rand49()。将41到49的结果抛弃，剩余结果%10+1，则为要求的结果

* 代码:
    ```C++
    // The rand7() API is already defined for you.
    // int rand7();
    // @return a random integer in the range 1 to 7

    class Solution {
    public:
        int rand10() {
            int result;
            while(true)
            {
                result = (rand7()-1)*7+rand7();
                if(result<=40)
                {
                    return result%10 +1;
                }
            }
        }
    };
    ```
