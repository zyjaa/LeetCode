###  1、DP

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        int n = s.size(); // 字符串的长度
        unordered_set<string> hash; // 用哈希表存储字典中的单词
        for (auto x : wordDict) hash.insert(x);

        // f[i] 表示 s 的前 i 个字符是否可以被拆分
        vector<bool> f(n + 1, false); // 初始化动态规划数组
        f[0] = true; // 空字符串可以被拆分

        // 动态规划求解
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                // 如果 s[0..j] 可以被拆分，且 s[j..i] 在字典中，则 s[0..i] 可以被拆分
                if (hash.count(s.substr(j, i - j)) && f[j]) {
                    f[i] = true;
                    break; // 找到一个满足条件的分割点即可
                }
            }
        }

        return f[n]; // 返回 s 是否可以被拆分
    }
};
```

- 时间：O($$n^2$$)
- 空间：n
