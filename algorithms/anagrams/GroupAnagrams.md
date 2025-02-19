[49. 字母异位词分组](https://leetcode.cn/problems/group-anagrams/)

给你一个字符串数组，请你将 **字母异位词** 组合在一起。可以按任意顺序返回结果列表。

**字母异位词** 是由重新排列源单词的所有字母得到的一个新单词。

 

**示例 1:**

```
输入: strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
输出: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

**示例 2:**

```
输入: strs = [""]
输出: [[""]]
```



### 法一：hash表

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string,vector<string>> map;
        for(auto& str:strs){
            auto a=str;
            sort(str.begin(),str.end());
            map[str].push_back(a);
        }
        vector<vector<string>> res;
        for(auto& it:map){
            res.push_back(it.second);
        }
        return res;
    }
};
```

- 时间：$$n*klogk$$
- 空间：$$n*k$$
  - 字符串的平均长度为 k
  - n：多少个字符串

