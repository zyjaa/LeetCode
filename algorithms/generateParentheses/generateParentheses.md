**22、题意**

数字 `n` 代表生成括号的对数，请你设计一个函数，用于能够生成所有可能的并且 **有效的** 括号组合。

 

**示例 1：**

```
输入：n = 3
输出：["((()))","(()())","(())()","()(())","()()()"]
```

**示例 2：**

```
输入：n = 1
输出：["()"]
```

 

**提示：**

- `1 <= n <= 8`





### 法一：dfs

根据（和）的数量进行判定

```cpp
class Solution {
public:
    vector<string> res;
    vector<string> generateParenthesis(int n) {
        // )()
        dfs(n,0,0,"");
        return res;
    }
    void dfs(int n,int lc,int rc,string path){
        if(lc==n && rc==n)res.push_back(path);
        else{
            if(lc<n)dfs(n,lc+1,rc,path+"(");
            if(rc<n && rc<lc)dfs(n,lc,rc+1,path+")");
        }
    }
};
```

- 时间：O($$4^n/\sqrt(n)$$)，这是卡特兰数的渐近上界。生成的有效括号组合的数量是卡特兰数
  - $$\binom{n}{2n}/(n+1)$$
  - $$C_{2n}^n/(n+1)$$
- 空间：O($$n$$)，主要是递归调用栈的空间开销，递归的深度最大为2n。