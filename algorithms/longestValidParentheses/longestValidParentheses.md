32、最长有效括号

给你一个只包含 `'('` 和 `')'` 的字符串，找出最长有效（格式正确且连续）括号子串的长度。

 

**示例 1：**

```
输入：s = "(()"
输出：2
解释：最长有效括号子串是 "()"
```

**示例 2：**

```
输入：s = ")()())"
输出：4
解释：最长有效括号子串是 "()()"
```

**示例 3：**

```
输入：s = ""
输出：0
```



### 法一：栈

`stk` 记录括号索引，`start` 记录无效括号的起始位置

```cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> stk;
        int res=0;
        for(int i=0,start=-1;i<s.size();i++){
            if(s[i]=='(')stk.push(i);
            else{
                if(stk.size()){
                    stk.pop();
                    if(stk.size()){
                        res=max(res,i-stk.top());
                    }else{
                        res=max(res,i-start);
                    }
                }else{//如果栈为空且未匹配
                    start=i;
                }
            }
        }
        return res;
    }
};
```

- **时间复杂度**：O(n)，遍历一次字符串。
- **空间复杂度**：O(n)，栈的最大深度。