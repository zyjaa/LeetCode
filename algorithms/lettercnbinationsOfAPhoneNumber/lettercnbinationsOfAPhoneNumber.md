**17、题意**

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。答案可以按 **任意顺序** 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/11/09/200px-telephone-keypad2svg.png)

 

**示例 1：**

```
输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**示例 2：**

```
输入：digits = ""
输出：[]
```

**示例 3：**

```
输入：digits = "2"
输出：["a","b","c"]
```

 

**提示：**

- `0 <= digits.length <= 4`
- `digits[i]` 是范围 `['2', '9']` 的一个数字。





### 法一：dfs

```cpp
class Solution {
public:
    string nums[10] = {
        "","","abc","def",
        "ghi","jkl","mno",
        "pqrs","tuv","wxyz"
    };
    vector<string> res;
    vector<string> letterCombinations(string digits) {
        if(digits.empty())return {};
        dfs(digits,0,"");
        return res;
    }
    void dfs(string& digits,int u,string path){
        if(u==digits.size())res.push_back(path);
        else{
            for(auto num:nums[digits[u]-'0'])
                dfs(digits,u+1,path+num);
        }
    }
};
```

- 时间复杂度：O()
- 空间复杂度：O(1)