```
#include <string>
#include <sstream>

using namespace std;

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Codec {
private:
    string serialized_path;  // 存储序列化后的字符串

    // 序列化辅助函数（DFS）
    void dfs_serialize(TreeNode* root) {
        if (!root) {
            serialized_path += "#,";  // 空节点用 "#," 表示
        } else {
            serialized_path += to_string(root->val) + ',';  // 将节点值转换为字符串
            dfs_serialize(root->left);   // 递归处理左子树
            dfs_serialize(root->right);  // 递归处理右子树
        }
    }

    // 反序列化辅助函数（DFS）
    TreeNode* dfs_deserialize(istringstream& iss) {
        string token;
        getline(iss, token, ',');  // 读取一个 token（以逗号分隔）
        if (token == "#") {
            return nullptr;  // 空节点返回 nullptr
        } else {
            TreeNode* root = new TreeNode(stoi(token));  // 创建节点
            root->left = dfs_deserialize(iss);   // 递归构建左子树
            root->right = dfs_deserialize(iss); // 递归构建右子树
            return root;
        }
    }

public:
    // 序列化：将二叉树转换为字符串
    string serialize(TreeNode* root) {
        serialized_path = "";  // 清空序列化字符串
        dfs_serialize(root);   // 调用 DFS 进行序列化
        return serialized_path;
    }

    // 反序列化：将字符串转换为二叉树
    TreeNode* deserialize(string data) {
        istringstream iss(data);  // 使用 istringstream 解析字符串
        return dfs_deserialize(iss);
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```

