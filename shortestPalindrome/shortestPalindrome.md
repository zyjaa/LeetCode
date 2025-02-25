### 1、KMP

```
class Solution {
public:
    string shortestPalindrome(string s) {
        string t(s.rbegin(), s.rend()); // 反转s，得到t
        int n = s.size(); // 原字符串的长度
        s = ' ' + s + '#' + t; // 构造新字符串，中间用'#'分隔
        vector<int> ne(2 * n + 2); // next数组，大小是2*n+2

        // KMP算法计算next数组
        for (int i = 2, j = 0; i <= 2 * n + 1; i++) {
            while (j && s[i] != s[j + 1]) j = ne[j]; // 如果不匹配，回退到next[j]
            if (s[i] == s[j + 1]) j++; // 如果匹配，j++
            ne[i] = j; // 记录next[i]
        }

        int len = ne[2 * n + 1]; // 最长回文前缀的长度
        string left = s.substr(1, len); // 最长回文前缀
        string right = s.substr(len + 1, n - len); // 剩余部分

        // 构造最短回文串
        return string(right.rbegin(), right.rend()) + left + right;
    }
};
```

### 时间复杂度：

1. **反转字符串**：O(n)。
2. **KMP算法**：O(n)。
3. **构造最短回文串**：O(n)。

- 总时间复杂度是 O(n)。
