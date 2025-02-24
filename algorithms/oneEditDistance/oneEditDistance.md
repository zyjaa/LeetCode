题目：https://blog.csdn.net/qq_29051413/article/details/108304028

### 1、双指针

```cpp
class Solution {
public:
    bool isOneEditDistance(string s, string t) {
        int n = s.size(), m = t.size();

        // 如果长度差大于 1，直接返回 false
        if (abs(n - m) > 1) return false;

        // 遍历字符串，找到第一个不匹配的字符
        int i = 0, j = 0;
        while (i < n && j < m && s[i] == t[j]) {
            i++;
            j++;
        }

        // 根据长度关系判断是否可以通过一次编辑操作
        if (n == m) {
            // 替换操作
            i++;
            j++;
        } else if (n < m) {
            // 插入操作
            j++;
        } else {
            // 删除操作
            i++;
        }

        // 继续遍历剩余部分
        while (i < n && j < m) {
            if (s[i] != t[j]) return false;
            i++;
            j++;
        }

        return true;
    }
};
```

 n,1
