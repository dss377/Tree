题目：
==
Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.
```
Example:
Input:

   1
    \
     3
    /
   2

Output:
1
Explanation:
The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).
```

分析：
==
题目给出了一棵二叉搜索树，值都是非负数，让我们求任意两个节点值之间的最小绝对差。由于二叉搜索树的性质可知，左<根<右，如果按照中序遍历会得到一个有序数组，那么最小的绝对值得差肯定在相邻的两个节点值之间产生。所以我们的做法就是对BST进行中序遍历，然后当前节点值和之前节点值求绝对差并更新结果ret。在这里需要注意的就是在处理第一个节点值时，由于其没有前节点，所以不能求绝对差。这里我们用变量pre来表示前节点值，而且题目中说了节点值不为负数，所以我们给pre初始化-1即可，这样我们就知道pre是否存在。

代码：
==
```C++
class Solution {
public:
    int getMinimumDifference(TreeNode* root) {
        int ret=INT_MAX,pre=-1;
        inorder(root,pre,ret);
        return ret;
    }
    void inorder(TreeNode* root, int& pre, int& ret) {
        if (!root) return;
        inorder(root->left, pre, ret);
        if (pre!=-1) ret= min(ret, root->val-pre);
        pre=root->val;
        inorder(root->right, pre, ret);
    }
};
```

感受：
==
放假后的第一次写代码，也是第一次做二叉搜索树，脑子还是懵懵的，决定接下来就主要练习二叉树的题目了，讲真，还是有些理解困难的，慢慢来吧。参考的知识来源：
https://blog.csdn.net/xiaoquantouer/article/details/65631708        https://blog.csdn.net/qq_37887537/article/details/75647670


