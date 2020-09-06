# 题目
实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

* 示例:
>输入: haystack = "hello", needle = "ll"<br>
输出: 2

>输入: haystack = "aaaaa", needle = "bba"<br>
输出: -1

说明:

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

* 思路：KMP


* 代码：
    ```C++
    class Solution {
    public:
        void getNext(string& P,vector<int>& next)
        {
            int i=0,j=-1;
            next[0]=-1;
            int length = P.size();
            while(i<length)
            {
                if(j==-1 || P[i]==P[j])
                {
                    ++i;
                    ++j;
                    next[i]=j;
                }
                else
                {
                    j = next[j];
                }
            }
            return;
        }
        
        int strStr(string haystack, string needle) {
            int length1 = haystack.size();
            int length2 = needle.size();
            if(length2==0)
            {
                return 0;
            }
            vector<int> next(length2+1,0);
            getNext(needle,next);
            int i=0,j=0;
            while(i<length1&&j<length2)
            {
                if(j==-1 || haystack[i]==needle[j])
                {
                    ++i;
                    ++j;
                }
                else
                {
                    j = next[j];
                }
            }
            if(j==length2)
            {
                return i-j;
            }
            else
            {
                return -1;
            }
        }

    };
    ```