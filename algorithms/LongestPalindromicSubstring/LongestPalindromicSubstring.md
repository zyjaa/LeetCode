**题意**：最长回文子串



**示例 1：**

```
输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
```

**示例 2：**

```
输入：s = "cbbd"
输出："bb"
```

 

**提示：**

- `1 <= s.length <= 1000`
- `s` 仅由数字和英文字母组成



### 法一：双指针

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        string res;
        int n=s.size();
        for(int i=0;i<s.size();i++){
            int l=i-1,r=i;//偶回文串
            while(l>=0 && l<n && r<n && s[l]==s[r])l--,r++;
            if(res.size()<r-l-1)res=s.substr(l+1,r-l-1);

            l=i-1,r=i+1;//奇回文串
            while(l>=0 && l<n && r<n && s[l]==s[r])l--,r++;
            if(res.size()<r-l-1)res=s.substr(l+1,r-l-1);
        }
        return res;
    }
};
```

- 时间复杂度：O(n²)，每次可以拓展n个字符
- 空间复杂度：O(1)





## 法二：Manacher

- 时间复杂度：O(n)
- 空间复杂度：O(1)

