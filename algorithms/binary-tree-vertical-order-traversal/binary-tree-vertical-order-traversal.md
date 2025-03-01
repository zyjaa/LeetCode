```
// 二叉树节点定义
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

class Solution {
public:
    vector<vector<int>> verticalOrder(TreeNode* root) {
        vector<vector<int>> result; // 存储最终结果
        if (!root) return result;

        // 哈希表，键是列号，值是该列的节点值列表
        map<int, vector<int>> columnTable;
        // 队列，存储节点及其列号
        queue<pair<TreeNode*, int>> q;
        q.push({root, 0}); // 根节点的列号为 0

        // 层序遍历
        while (!q.empty()) {
            auto node = q.front().first; // 当前节点
            int col = q.front().second; // 当前列号
            q.pop();

            // 将节点值存入哈希表对应的列
            columnTable[col].push_back(node->val);

            // 将左子节点和右子节点加入队列
            if (node->left) {
                q.push({node->left, col - 1}); // 左子节点列号减 1
            }
            if (node->right) {
                q.push({node->right, col + 1}); // 右子节点列号加 1
            }
        }

        // 按照列号从小到大输出结果
        for (const auto& pair : columnTable) {
            result.push_back(pair.second);
        }

        return result;
    }
};
```

