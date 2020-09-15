# 题目
小扣在秋日市集选择了一家早餐摊位，一维整型数组 staple 中记录了每种主食的价格，一维整型数组 drinks 中记录了每种饮料的价格。小扣的计划选择一份主食和一款饮料，且花费不超过 x 元。请返回小扣共有多少种购买方案。

注意：答案需要以 1e9 + 7 (1000000007) 为底取模，如：计算初始结果为：1000000008，请返回 1

* 示例：

>输入：staple = [10,20,5], drinks = [5,5,2], x = 15<br>
输出：6<br>
解释：小扣有 6 种购买方案，所选主食与所选饮料在数组中对应的下标分别是：<br>
第 1 种方案：staple[0] + drinks[0] = 10 + 5 = 15；<br>
第 2 种方案：staple[0] + drinks[1] = 10 + 5 = 15；<br>
第 3 种方案：staple[0] + drinks[2] = 10 + 2 = 12；<br>
第 4 种方案：staple[2] + drinks[0] = 5 + 5 = 10；<br>
第 5 种方案：staple[2] + drinks[1] = 5 + 5 = 10；<br>
第 6 种方案：staple[2] + drinks[2] = 5 + 2 = 7。

>输入：staple = [2,1,1], drinks = [8,9,5,1], x = 9<br>
输出：8<br>
解释：小扣有 8 种购买方案，所选主食与所选饮料在数组中对应的下标分别是：<br>
第 1 种方案：staple[0] + drinks[2] = 2 + 5 = 7；<br>
第 2 种方案：staple[0] + drinks[3] = 2 + 1 = 3；<br>
第 3 种方案：staple[1] + drinks[0] = 1 + 8 = 9；<br>
第 4 种方案：staple[1] + drinks[2] = 1 + 5 = 6；<br>
第 5 种方案：staple[1] + drinks[3] = 1 + 1 = 2；<br>
第 6 种方案：staple[2] + drinks[0] = 1 + 8 = 9；<br>
第 7 种方案：staple[2] + drinks[2] = 1 + 5 = 6；<br>
第 8 种方案：staple[2] + drinks[3] = 1 + 1 = 2；

提示：

    1 <= staple.length <= 10^5
    1 <= drinks.length <= 10^5
    1 <= staple[i],drinks[i] <= 10^5
    1 <= x <= 2*10^5
* 思路1：对staple做记录，记录价格小于等于n的个数放在record中，则遍历drinks获取小于等于剩余价格的个数即可，注意事项为x-drinks[n]可能大于1e5，因为1 <= x <= 2*10^5，则需要判断x-drinks是否大于1e5，如果是的话则全部主食都可以点。
* 代码1：
    ```C++
    class Solution {
    public:
        int breakfastNumber(vector<int>& staple, vector<int>& drinks, int x) {
            const int largest = 1e5;
            const int mo = 1000000007;
            vector<int> record(largest+1,0);
            sort(staple.begin(),staple.end());
            int count = 0;
            int index = 0;
            int length2 = staple.size();
            for(int n=1;n<=largest;++n)
            {
                while(index<length2 && n>=staple[index])
                {
                    ++count;
                    ++index;
                }
                record[n]=count;
            }
            int length = drinks.size();
            long long result=0;
            int re;
            for(int n=0;n<length;++n)
            {
                re = x - drinks[n];
                if(re>=largest)
                {
                    result = (result + record[largest])%mo;
                }
                else if(re>0)
                {
                    result = (result + record[re])%mo;
                }
                
            }
            return result;
        }
    };
    ```
* 思路2：双指针，对主食和饮品进行排序，对主食从头到尾遍历，同时对饮品从后向前遍历，如果当前饮品能够和主食组合，则当前主食可以和比当前饮品便宜的所有饮品组合，则result = result + indexd+1,遍历主食，当indexd<0时则比当前主食更贵的主食不可能有饮品可以组合，直接break
* 代码2：
    ```C++
    class Solution {
    public:
        int breakfastNumber(vector<int>& staple, vector<int>& drinks, int x) {
            sort(staple.begin(),staple.end());
            sort(drinks.begin(),drinks.end());
            int length = staple.size();
            int indexd = drinks.size()-1;
            long long result=0;
            const int mo = 1e9+7;
            for(int n=0;n<length;++n)
            {
                while(indexd>=0 && (x-staple[n])<drinks[indexd])
                {
                    --indexd;
                }
                if(indexd<0)
                {
                    break;
                }
                result = (result+indexd+1)% mo;
            }
            return result;
        }
    };
    ```

* 思路3：双指针+二分查找，在查找时不是顺序遍历饮品，而是二分查找最大的能够满足要求的饮品，可以实现加速

* 代码3：
    ```C++
    class Solution {
    public:
        int binarysearch(vector<int>& data,int left,int right,int target)
        {
            if(data[left]>target)
            {
                return -1;
            }
            else if(data[right]<target)
            {
                return right;
            }
            else
            {
                int mid;
                while(left<right)
                {
                    mid = left + (right-left)/2+1;
                    if(data[mid]<=target)
                    {
                        left = mid;
                    }
                    else
                    {
                        right = mid-1;
                    }
                }
                return right;
                }
        }

        int breakfastNumber(vector<int>& staple, vector<int>& drinks, int x) {
            sort(staple.begin(),staple.end());
            sort(drinks.begin(),drinks.end());
            int length = staple.size();
            int indexd = drinks.size()-1;
            long long result=0;
            const int mo = 1e9+7;
            int laststaple = -1;
            for(int n=0;n<length;++n)
            {
                if((x-staple[n])<drinks[0])
                {
                    break;
                }
                if(laststaple != staple[n])
                {
                    indexd = binarysearch(drinks,0,indexd,x-staple[n]); 
                }
                result = (result+indexd+1)% mo;
            }
            return result;
        }
    };
    ```

* 代码4：排序+二分
    ```C++
    class Solution {
    public:
        int breakfastNumber(vector<int>& staple, vector<int>& drinks, int x) {
            sort(drinks.begin(),drinks.end());
            int mod=1e9+7;
            int cnt=0;
            int m=staple.size(),n=drinks.size();
            for(int i=0;i<m;++i){
                int lo=0;
                int hi=n;
                int target=x-staple[i];
                if(target<=0) continue;
                while(lo<hi){
                    int mid=(lo+hi)/2;
                    if(drinks[mid]>target) hi=mid;
                    else lo=mid+1;
                    
                }
                cnt+=lo;
                cnt%=mod;
            }
            cnt%=mod;
            return cnt;
            
        }
    };
    ```