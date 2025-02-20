[76. 最小覆盖子串](https://leetcode.cn/problems/minimum-window-substring)

 

**示例 1：**

```
输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"
解释：最小覆盖子串 "BANC" 包含来自字符串 t 的 'A'、'B' 和 'C'。
```



### 1、滑动窗口+哈希表

- 使用双指针 `i` 和 `j` 表示窗口的左右边界。
- 移动右指针 `i`，扩展窗口，并更新 `hs` 和 `cnt`（匹配字符的数量）。
- 当 `cnt == t.size()` 时，表示当前窗口包含了 `t` 的所有字符，尝试缩小窗口以找到更小的子串。
- 移动左指针 `j`，缩小窗口，同时更新 `hs`。

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        string res;
        unordered_map<char,int> hs,ht;
        for(auto x:t)ht[x]++;
        int cnt=0;
        for(int j=0,i=0;i<s.size();i++){
            hs[s[i]]++;
            if(hs[s[i]]<=ht[s[i]])cnt++;//匹配的数量
            while(hs[s[j]]>ht[s[j]])hs[s[j++]]--;//左指针右移
            if(cnt==t.size()){//完全匹配
                if(res.empty() || i-j+1<res.size())res=s.substr(j,i-j+1);
            }
        }
        return res;
    }
};
```

- 时间：n
  - 右指针 `i` 从左到右遍历 `s`，时间复杂度为 `O(n)`，其中 `n` 是 `s` 的长度。
  - 左指针 `j` 最多移动 `n` 次，时间复杂度为 `O(n)`。
- 空间：m



**优化**

- 如果 `s` 的长度小于 `t` 的长度，直接返回空字符串，避免不必要的计算。
- 在缩小窗口时，可以直接判断 `hs[s[j]] == ht[s[j]]`，避免频繁更新 `hs`。
- 使用 `start` 和 `minLen` 记录最小窗口的起始位置和长度，避免频繁调用 `s.substr`。

```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        if (s.size() < t.size()) return ""; // 提前返回

        unordered_map<char, int> hs, ht;
        for (auto x : t) ht[x]++; // 记录t的字符频率

        int cnt = 0; // 匹配字符的数量
        int start = 0, minLen = INT_MAX; // 最小窗口的起始位置和长度
        for (int j = 0, i = 0; i < s.size(); i++) {
            hs[s[i]]++; // 扩展窗口
            if (hs[s[i]] <= ht[s[i]]) cnt++; // 更新匹配字符数量

            // 缩小窗口
            while (hs[s[j]] > ht[s[j]]) {
                hs[s[j]]--;
                j++;
            }

            // 更新最小窗口
            if (cnt == t.size() && i - j + 1 < minLen) {
                minLen = i - j + 1;
                start = j;
            }
        }

        return minLen == INT_MAX ? "" : s.substr(start, minLen);
    }
};
```

- 时间：n
- 空间：m