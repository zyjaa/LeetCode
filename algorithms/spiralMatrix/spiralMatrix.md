[54. 螺旋矩阵](https://leetcode.cn/problems/spiral-matrix/)

给你一个 `m` 行 `n` 列的矩阵 `matrix` ，请按照 **顺时针螺旋顺序** ，返回矩阵中的所有元素。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```



### 1、模拟

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int n=matrix.size(),m=matrix[0].size();
        vector<vector<bool>> st(n,vector<bool>(m));
        int dx[4]={0,1,0,-1},dy[4]={1,0,-1,0};
        vector<int> res;
        for(int i=0,x=0,y=0,d=0;i<n*m;i++){
            res.push_back(matrix[x][y]);
            int a=x+dx[d],b=y+dy[d];
            st[x][y]=true;
            if(a<0 || a>=n || b<0 || b>=m || st[a][b]){
                d=(d+1)%4;// 换方向（顺时针）
                a=x+dx[d],b=y+dy[d];
            }
            x=a,y=b;
        }
        return res;
    }
};
```

- 时间：O($$n*m$$)，所有数都遍历一遍
- 空间：O($$n*m$$)，st数组





**优化空间**

- 可以去掉 `st` 数组，通过修改矩阵中的值（如设置为 `INT_MIN`）来标记已访问的位置。
- 使用四个变量（`left`、`right`、`top`、`bottom`）记录当前螺旋的边界，减少方向切换的判断。

```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int n = matrix.size(), m = matrix.size();
        vector<int> res;
        int left = 0, right = m - 1, top = 0, bottom = n - 1;

        while (left <= right && top <= bottom) {
            // 从左到右遍历上边界
            for (int i = left; i <= right; i++) {
                res.push_back(matrix[top][i]);
            }
            top++;

            // 从上到下遍历右边界
            for (int i = top; i <= bottom; i++) {
                res.push_back(matrix[i][right]);
            }
            right--;

            // 从右到左遍历下边界
            if (top <= bottom) {
                for (int i = right; i >= left; i--) {
                    res.push_back(matrix[bottom][i]);
                }
                bottom--;
            }

            // 从下到上遍历左边界
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    res.push_back(matrix[i][left]);
                }
                left++;
            }
        }

        return res;
    }
};
```

- 时间：O($$n*m$$)，所有数都遍历一遍
- 空间：O($$1$$)

