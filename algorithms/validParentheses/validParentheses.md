**20、题意**：括号是否有效

定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串 `s` ，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。
3. 每个右括号都有一个对应的相同类型的左括号。

 

**示例 1：**

**输入**：s = "()"

**输出**：true

**示例 2**：

**输入**：s = "()[]{}"

**输出**：true



### 法一：栈

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> stk;
        for(auto x:s){
            if(x=='(' || x=='{' || x=='[')stk.push(x);
            else{
                if(stk.size() && abs(stk.top()-x)<=2)stk.pop();
                else return false;
            }
        }
        return stk.empty();
    }
};
```

- 时间复杂度：O($$n$$)
- 空间复杂度：O($$n$$)