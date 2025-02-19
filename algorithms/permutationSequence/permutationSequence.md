[60. 排列序列](https://leetcode.cn/problems/permutation-sequence/)

给出集合 `[1,2,3,...,n]`，其所有元素共有 `n!` 种排列。

按大小顺序列出所有排列情况，并一一标记，当 `n = 3` 时, 所有排列如下：

1. `"123"`
2. `"132"`
3. `"213"`
4. `"231"`
5. `"312"`
6. `"321"`

给定 `n` 和 `k`，返回第 `k` 个排列。

 

**示例 1：**

```
输入：n = 3, k = 3
输出："213"
```





### 1、DFS

```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        string res; // 存储结果
        vector<bool> used(n + 1, false); // 标记数字是否被使用
        dfs(n, k, used, res); // DFS搜索
        return res;
    }

private:
    void dfs(int n, int& k, vector<bool>& used, string& res) {
        if (res.size() == n) {
            // 找到一个排列，k减1
            k--;
            return;
        }

        for (int i = 1; i <= n; i++) {
            if (!used[i]) {
                used[i] = true; // 标记当前数字已被使用
                res.push_back('0' + i); // 将当前数字加入结果
                dfs(n, k, used, res); // 递归搜索下一层

                // 如果找到第k个排列，直接返回
                if (k == 0) return;

                // 回溯：撤销选择
                res.pop_back();
                used[i] = false;
            }
        }
    }
};
```

- 最坏情况下需要生成所有排列，时间复杂度为 **O(n!)**。
- 空间：O(n)





### 2、位运算

```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        vector<bool> st(n); // 标记数字是否被使用
        string res; // 存储结果

        // 从高位到低位依次确定每个数字
        for (int i = 0; i < n; i++) {
            int f = 1; // 计算当前分支的阶乘值 (n - 1 - i)!
            for (int j = 1; j <= n - 1 - i; j++) {
                f *= j;
            }

            // 遍历数字 1 到 n，找到第 k 个未使用的数字
            for (int j = 1; j <= n; j++) {
                if (!st[j]) {
                    if (f < k) {
                        k -= f; // 跳过当前分支
                    } else {
                        res += to_string(j); // 将数字加入结果
                        st[j] = true; // 标记为已使用
                        break;
                    }
                }
            }
        }

        return res;
    }
};
```

- 时间：O($$n^2$$)
- 空间：O($$n$$)



### 3、next_permutation

```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        string res;
        for (int i = 1; i <= n; i ++ ) res += to_string(i);
        for (int i = 0; i < k - 1; i ++ ) {
            next_permutation(res.begin(), res.end());
        }
        return res;
    }
};
```

- 时间：O(n*k)，k最坏为n!
  - 使用 `next_permutation` 函数生成下一个排列，重复 `k - 1` 次。
  - 每次调用 `next_permutation` 的时间复杂度为 **O(n)**。
- 空间：O(n)，res







