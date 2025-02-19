[47. 全排列 II](https://leetcode.cn/problems/permutations-ii/)

给定一个可包含重复数字的序列 `nums` ，***按任意顺序*** 返回所有不重复的全排列。

**示例 1：**

```
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```



### 法一：DFS

剪枝：重复的只取第一次的，相同就跳过

```cpp
class Solution {
public:
    vector<vector<int>> res; // 存储结果
    vector<int> path;        // 当前生成的排列
    vector<bool> st;         // 标记数组，记录数字是否被使用过

    vector<vector<int>> permuteUnique(vector<int>& nums) {
        sort(nums.begin(), nums.end()); // 排序，方便剪枝
        int n = nums.size();
        path = vector<int>(n); // 初始化当前排列
        st = vector<bool>(n, false); // 初始化标记数组

        dfs(nums, 0); // 从第 0 层开始回溯
        return res;
    }

    void dfs(vector<int>& nums, int u) {
        if (u == nums.size()) { // 如果当前排列长度等于 nums 的长度
            res.push_back(path); // 将当前排列加入结果
            return;
        }
        for (int i = 0; i < nums.size(); i++) { // 遍历 nums
            if (!st[i]) { // 如果数字未被使用过
                // 剪枝：如果当前数字与前一个数字相同，且前一个数字未被使用过，则跳过
                if (i && nums[i - 1] == nums[i] && !st[i - 1]) continue;
                path[u] = nums[i]; // 将数字加入当前排列
                st[i] = true;      // 标记数字已被使用
                dfs(nums, u + 1);  // 递归处理下一层
                st[i] = false;     // 回溯，取消标记
            }
        }
    }
};
```

- 时间：O($$n*n!$$)
  - 递归树节点数：全排列的数量为 n!，其中 n是数组长度。
  - 每个节点的操作：每次递归需要遍历数组，时间复杂度为 O(n)。
- 空间：O($$n*n!$$)
  - 递归栈深度：递归深度为 n，空间复杂度为 O(n)。
  - 存储结果：结果数量为 n!，每个排列长度为 n，空间复杂度为 O(n⋅n!)。
  - 标记数组 `st` 和当前排列 `path`：额外空间为 O(n)。