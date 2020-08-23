# 题目
输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

 

* 示例：
>前序遍历 preorder = [3,9,20,15,7]<br>
中序遍历 inorder = [9,3,15,20,7]<br>
返回如下的二叉树：

        3
       / \
      9  20
        /  \
       15   7


限制：

0 <= 节点个数 <= 5000
* 思路：在先序遍历中，第一个节点即为当前的根节点，在中序遍历中找到这个节点，则在中序这个节点左侧的节点为左子树的节点，右侧的节点为右子树的节点，即可以确定左右子树的节点个数l，r，而在先序遍历中，当前节点之后的l个节点即为左子树的节点，剩下的r个节点为右子树的节点，则可以递归调用获得左右子树的根节点得到最终结果
* 代码：
    ```C++
    /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     TreeNode *left;
   *     TreeNode *right;
   *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
   * };
   */
  class Solution {
  public:
      TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
          int length = preorder.size();
          if(preorder.size()==0)
          {
              return nullptr;
          }
          else
          {
              return SubBuildTree(preorder,0,inorder,0,length);
          }
      }

      TreeNode* SubBuildTree(vector<int>& preorder,int preBegin,vector<int>& inorder,int inBegin,int length)
      {
          if(length<1)
          {
              return nullptr;
          }
          if(length==1)
          {
              return new TreeNode(preorder[preBegin]);
          }
          else
          {
              TreeNode* nowroot = new TreeNode(preorder[preBegin]);
              int index = inBegin;
              while(index<inBegin+length && preorder[preBegin]!=inorder[index])
              {
                  ++index;
              }
              nowroot->left = SubBuildTree(preorder,preBegin+1,inorder,inBegin,index-inBegin);
              nowroot->right = SubBuildTree(preorder,preBegin+index-inBegin+1,inorder,index+1,length-index+inBegin-1);
              return nowroot;
          }
          
      }
  };
    ```