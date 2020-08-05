# 题目
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

示例 1：

输入：head = [1,3,2]
输出：[2,3,1]
* 代码1：栈
    ```C++
    /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
    class Solution {
    public:
        vector<int> reversePrint(ListNode* head) {
            stack<int> s;
            while(head!=nullptr)
            {
                s.push(head->val);
                head = head->next;
            }
            vector<int> result;
            while(!s.empty())
            {
                result.push_back(s.top());
                s.pop();
            }
            return result;
        }
    };
    ```
* 代码2：用vector的reverse完成翻转
    ```C++
    /**
    * Definition for singly-linked list.
    * struct ListNode {
    *     int val;
    *     ListNode *next;
    *     ListNode(int x) : val(x), next(NULL) {}
    * };
    */
    class Solution {
    public:
        vector<int> reversePrint(ListNode* head) {
            vector<int> result;
            while(head!=nullptr)
            {
                result.push_back(head->val);
                head = head->next;
            }
            reverse(result.begin(),result.end());
            return result;
        }
    };
    ```