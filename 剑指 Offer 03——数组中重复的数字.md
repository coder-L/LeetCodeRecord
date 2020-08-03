# 题目
找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

* 示例：
输入：<br>
[2, 3, 1, 0, 2, 5, 3]<br>
输出：2 或 3 

>限制：<br>
2 <= n <= 100000

* 思路1：使用set记录访问过的元素
* 代码1：
    ```C++
    class Solution {
    public:
        int findRepeatNumber(vector<int>& nums) {
            set<int> record;
            for(auto n:nums)
            {
                if(record.count(n))
                {
                    return n;
                }
                else
                {
                    record.insert(n);
                }
            }
            return -1;
        }
    };
    ```
* 思路2：因为题中给出nums 里的所有数字都在 0～n-1 的范围内，可以将数字放到相等的下标中，判断要交换的下标中的数是否等于当前数即可
* 代码2：
    ```C++
    class Solution {
    public:
        int findRepeatNumber(vector<int>& nums) {
            int length = nums.size();
            for(int n=0;n<length;++n)
            {
                if(nums[n]!=n)
                {
                    if(nums[n]==nums[nums[n]])
                    {
                        return nums[n];
                    }
                    else
                    {
                        swap(nums[n],nums[nums[n]]);
                    }
                }
            }
            return -1;
        }
    };
    ```