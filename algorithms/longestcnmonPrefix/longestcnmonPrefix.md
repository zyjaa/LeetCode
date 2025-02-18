**题意**：最长公共前缀

**示例 1：**

```
输入：strs = ["flower","flow","flight"]
输出："fl"
```

**示例 2：**

```
输入：strs = ["dog","racecar","car"]
输出：""
解释：输入不存在公共前缀。
```





### 法一：贪心

排序，看第一个string和最后一个string字符是否相同，相同就加进来

```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        sort(strs.begin(),strs.end());
        string res;
        for(int i=0;i<strs[0].size();i++){
            if(strs[0][i]==strs[strs.size()-1][i])res+=strs[0][i];
            else break;
        }
        return res;
    }
};
```

