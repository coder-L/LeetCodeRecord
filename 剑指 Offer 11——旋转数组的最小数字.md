# 题目
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

* 示例：

>输入：[3,4,5,1,2]<br>
输出：1

>输入：[2,2,2,0,1]<br>
输出：0


* 思路1：暴力法，找到第一个小于数组中第一个元素的值即为最小值，否则返回第一个元素


* 代码1：
    ```C++
    class Solution {
    public:
        int minArray(vector<int>& numbers) {
            int length = numbers.size();
            if(length ==0)
            {
                return 0;
            }
            int min = numbers[0];
            for(int n=1;n<length;++n)
            {
                if(numbers[n]<min)
                {
                    return numbers[n];
                }
            }
            return min;
        }
    };
    ```

* 思路2：二分查找,将mid和right比较，如果mid<right，说明mid到right为增序，则最小元素在[left,mid]中，则令right=mid，如果mid>right，说明left到mid为增序，且大于mid到right中的元素，则最小元素包含在[mid+1,right],则令left=mid+1，如果mid==right，则right位置无作用，则令right--；
    1. 和传统二分查找区别1：不是和target比较，是和right对应元素比较
    2. 区别2：传统二分查找可能找不到值，即返回-1，而在这里一定存在一个最小值，我们要保证最小值一直在查找的区间中，因此当mid<right时，mid可能是数组中的最小元素，因此不能令right = mid-1，而是right=mid，而当mid>right时，mid不可能是元素中的最小元素，因此令left=mid+1
    3. 区别3：由于元素不确定且一定存在，最后一定会达到终止条件left==right,因此最后返回left或right对应的元素即可


* 代码2：
    ```C++
    class Solution {
    public:
        int findMin(vector<int>& nums) {
            int left = 0;
            int right = nums.size()-1;
            int mid;
            while(left<right)
            {
                mid = left +(right-left)/2;
                if(nums[mid]>nums[right])
                {
                    left = mid +1;
                }
                else if(nums[mid]<nums[right])
                {
                    right = mid;
                }
                else
                {
                    --right;
                }
            }
            return nums[left];
        }
    };
    ```