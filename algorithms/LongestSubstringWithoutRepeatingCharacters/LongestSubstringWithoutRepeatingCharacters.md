**题意**：求最长无重复字符子串



**示例 1:**

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

 

**提示：**

- `0 <= s.length <= 5 * 104`
- `s` 由英文字母、数字、符号和空格组成



### 法一：滑动窗口

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int ans=0;
        unordered_map<char,int> map;
        for(int j=0,i=0;i<s.size();i++){
            map[s[i]]++;
            while(map[s[i]]>1)map[s[j++]]--;
            ans=max(ans,i-j+1);
        }
        return ans;
    }
};
```

- 时间复杂度：O(N)，左右指针都会遍历一遍数组
- 空间复杂的：O(128)，ASCll字符集的数量，最多128个







