**28、找出字符串中第一个匹配项的下标**

**例 1：**

```
输入：haystack = "sadbutsad", needle = "sad"
输出：0
解释："sad" 在下标 0 和 6 处匹配。
第一个匹配项的下标是 0 ，所以返回 0 。
```

**示例 2：**

```
输入：haystack = "leetcode", needle = "leeto"
输出：-1
解释："leeto" 没有在 "leetcode" 中出现，所以返回 -1 。
```



### 法一：kmp

```cpp
class Solution {
public:
    int strStr(string s, string p) {
        int n=s.size(),m=p.size();
        s=' '+s,p=' '+p;
        vector<int> ne(m+1);
        for(int i=2,j=0;i<=m;i++){
            while(j && p[i]!=p[j+1])j=ne[j];
            if(p[i]==p[j+1])j++;
            ne[i]=j;
        }
        for(int i=1,j=0;i<=n;i++){
            while(j && s[i]!=p[j+1])j=ne[j];
            if(s[i]==p[j+1])j++;
            if(j==m)return i-m;
        }
        return -1;
    }
};
```

- 时间：O($$n+m$$)
  - 预处理模式串：`O(m)`，其中 `m` 是模式串的长度。
  - 匹配过程：`O(n)`，其中 `n` 是主串的长度。
- 空间：O($$n+m$$)
  - 修改相当于新建了新的字符串是吧