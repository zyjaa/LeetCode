[85. 最大矩形](https://leetcode.cn/problems/maximal-rectangle/)

给定一个仅包含 `0` 和 `1` 、大小为 `rows x cols` 的二维二进制矩阵，找出只包含 `1` 的最大矩形，并返回其面积。

 

**示例 1：**

![img](https://pic.leetcode.cn/1722912576-boIxpm-image.png)

```
输入：matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
输出：6
```



### 1、单调栈

一样的，以每行为基准向上的连续的1就是高度，以每行为基准从1-n找一遍，就找到最大的矩形

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n=heights.size();
        vector<int> l(n),r(n);
        stack<int> stk;
        for(int i=0;i<n;i++){
            while(stk.size() && heights[stk.top()]>=heights[i])stk.pop();
            if(stk.empty())l[i]=-1;
            else l[i]=stk.top();
            stk.push(i);
        }
        stk=stack<int>();
        for(int i=n-1;i>=0;i--){
            while(stk.size() && heights[stk.top()]>=heights[i])stk.pop();
            if(stk.empty())r[i]=n;
            else r[i]=stk.top();
            stk.push(i);
        }
        int res=0;
        for(int i=0;i<n;i++)res=max(res,heights[i]*(r[i]-l[i]-1));
        return res;
    }
    int maximalRectangle(vector<vector<char>>& matrix) {
        int n=matrix.size(),m=matrix[0].size();
        vector<vector<int>> f(n,vector<int>(m));
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(matrix[i][j]=='1'){
                    if(i)f[i][j]=f[i-1][j]+1;
                    else f[i][j]=1;
                }
            }
        }
        int res=0;
        for(int i=0;i<n;i++)res=max(res,largestRectangleArea(f[i]));
        return res;
    }
};
```

- 时间：m*n
- 空间：m*n