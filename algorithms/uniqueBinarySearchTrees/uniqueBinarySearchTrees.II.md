[95. 不同的二叉搜索树 II](https://leetcode.cn/problems/unique-binary-search-trees-ii/)

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```
输入：n = 3
输出：[[1,null,2,null,3],[1,null,3,2],[2,1,3],[3,1,null,null,2],[3,2,null,1]]
```





### 1、DFS

暴搜所有结果

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<TreeNode*> generateTrees(int n) {
        // C2n n /n+1
        if(!n)return {};
        return dfs(1,n);
    }
    vector<TreeNode*> dfs(int l, int r) {
        if (l > r) return {NULL}; // 如果左边界大于右边界，返回包含 NULL 的列表
        vector<TreeNode*> res; // 存储当前范围内的所有 BST
        for (int i = l; i <= r; i++) { // 枚举根节点的值
            auto left = dfs(l, i - 1); // 递归生成左子树
            auto right = dfs(i + 1, r); // 递归生成右子树
            for (auto l : left) { // 遍历所有左子树
                for (auto r : right) { // 遍历所有右子树
                    auto root = new TreeNode(i); // 创建当前根节点
                    root->left = l; // 连接左子树
                    root->right = r; // 连接右子树
                    res.push_back(root); // 将当前树加入结果列表
                }
            }
        }
        return res; // 返回当前范围内的所有 BST
    }
};
```

- 时间：O($$C_{n}$$)（卡特兰数）
  - 每层枚举一个根节点，递归树深度为n
  - 递归树节点数位卡特兰数
  - 每次生成左右子树时间复杂度为O($$C_{k}$$)和O($$C_{n-k-1}$$)
- 空间：O($$n*C_{n}$$)
  - 结果的 BST 数量为卡特兰数 Cn*C**n*。
  - 每个 BST 的节点数为 `n`，因此结果存储空间复杂度为 O(n⋅Cn)*O*(*n*⋅*C**n*)。

