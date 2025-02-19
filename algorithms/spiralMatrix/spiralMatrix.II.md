[59. 螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/)

给你一个正整数 `n` ，生成一个包含 `1` 到 `n^2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
```



### 1、模拟一

```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> f(n,vector<int>(n));
        int dx[4]={0,1,0,-1},dy[4]={1,0,-1,0};
        for(int i=1,x=0,y=0,d=0;i<=n*n;i++){
            f[x][y]=i;
            int a=x+dx[d],b=y+dy[d];
            if(a<0 || a>=n || b<0 || b>=n || f[a][b]){
                d=(d+1)%4;
                a=x+dx[d],b=y+dy[d];
            }
            x=a,y=b;
        }
        return f;
    }
};
```

- 时间：O($$n^2$$)
- 空间：O($$n^2$$)



### 2、模拟二

```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> f(n, vector<int>(n)); // 初始化 n x n 的二维数组
        int num = 1; // 当前填充的数字
        int left = 0, right = n - 1, top = 0, bottom = n - 1; // 定义四个边界

        while (left <= right && top <= bottom) {
            // 从左到右填充上边界
            for (int i = left; i <= right; i++) {
                f[top][i] = num++;
            }
            top++;

            // 从上到下填充右边界
            for (int i = top; i <= bottom; i++) {
                f[i][right] = num++;
            }
            right--;

            // 从右到左填充下边界
            if (top <= bottom) {
                for (int i = right; i >= left; i--) {
                    f[bottom][i] = num++;
                }
                bottom--;
            }

            // 从下到上填充左边界
            if (left <= right) {
                for (int i = bottom; i >= top; i--) {
                    f[i][left] = num++;
                }
                left++;
            }
        }

        return f;
    }
};
```

- 时间：O($$n^2$$)
- 空间：O($$n^2$$)

就少了个边界检查