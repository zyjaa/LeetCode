[96. 不同的二叉搜索树](https://leetcode.cn/problems/unique-binary-search-trees/)

**示例 1：**

![img](https://assets.leetcode.com/uploads/2021/01/18/uniquebstn3.jpg)

```
输入：n = 3
输出：5
```



### 1、DP

- `f[i]` 表示由 `i` 个节点组成的不同 BST 的数量。
- 空树也是1种情况
- 

```cpp
class Solution {
public:
    int numTrees(int n) {
        // f(i)  1-i
        vector<int> f(n+1);
        f[0]=1;
        for(int i=1;i<=n;i++){
            for(int j=1;j<=i;j++){// j为根节点
                f[i]+=f[i-j]*f[j-1];// 左子树情况*右子树情况
            }
        }
        return f[n];
    }
};
```

- 时间：O($$n^2$$)
- 空间：O($$n$$)