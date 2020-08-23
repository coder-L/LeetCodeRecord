# 题目
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 

* 示例：

>输入：<br>
["CQueue","appendTail","deleteHead","deleteHead"]<br>
[[],[3],[],[]]<br>
输出：[null,null,3,-1]

>输入：<br>
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]<br>
[[],[],[5],[2],[],[]]<br>
输出：[null,-1,null,null,5,2]

提示：

    1 <= values <= 10000
    最多会对 appendTail、deleteHead 进行 10000 次调用


* 思路：使用两个栈存储数据，其中一个栈用于插入数据，另外一个栈用于输出数据
* 代码：
    ```C++
    class CQueue {
    public:
        CQueue() {

        }
        
        void appendTail(int value) {
            while(!outputs.empty())
            {
                inserts.push(outputs.top());
                outputs.pop();
            }
            inserts.push(value);
        }
        
        int deleteHead() {
            int result = -1;
            if(!outputs.empty())
            {
                result = outputs.top();
                outputs.pop();
            }
            else if(!inserts.empty())
            {
                while(!inserts.empty())
                {
                    outputs.push(inserts.top());
                    inserts.pop();
                }
                result = outputs.top();
                outputs.pop();
            }
            return result;
            
        }
        stack<int> inserts;
        stack<int> outputs;
    };

    /**
    * Your CQueue object will be instantiated and called as such:
    * CQueue* obj = new CQueue();
    * obj->appendTail(value);
    * int param_2 = obj->deleteHead();
    */
    ```

