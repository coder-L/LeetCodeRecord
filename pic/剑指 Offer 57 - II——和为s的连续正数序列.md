# 题目
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。


* 示例：
>输入：target = 9<br>
输出：[[2,3,4],[4,5]]

输入：target = 15<br>
输出：[[1,2,3,4,5],[4,5,6],[7,8]]

* 思路：假设n为正整数序列和的起点，向后找正整数序列和的终点，如果找到和等于target，则加入到结果中，并将起点右移一位。如果和大于target，则直接将起点右移一位继续寻找。

* 代码:
    ```C++
    class Solution {
    public:
        vector<vector<int>> findContinuousSequence(int target) {
            vector<vector<int>> result;
            if(target<=1)
            {
                return result;
            }
            for(int n=1;n<target/2+1;++n)
            {
                for(int m=n+1;true;++m)
                {
                    if((n+m)*(m-n+1)/2==target)
                    {
                        vector<int> tmp;
                        for(int i=n;i<=m;++i)
                        {
                            tmp.push_back(i);
                        }
                        result.push_back(tmp);
                        break;
                    }
                    else if((n+m)*(m-n+1)/2>target)
                    {
                        break;
                    }
                }
            }
            return result;
        }
    };
    ```