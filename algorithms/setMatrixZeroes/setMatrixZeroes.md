[73. 矩阵置零](https://leetcode.cn/problems/set-matrix-zeroes)

给定一个 `*m* x *n*` 的矩阵，如果一个元素为 **0** ，则将其所在行和列的所有元素都设为 **0** 。请使用 **[原地](http://baike.baidu.com/item/原地算法)** 算法**。**



 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```
输入：matrix = [[1,1,1],[1,0,1],[1,1,1]]
输出：[[1,0,1],[0,0,0],[1,0,1]]
```



### 1、模拟

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int n=matrix.size(),m=matrix[0].size();
        int rz=1,cz=1;
        for(int i=0;i<m;i++)
            if(!matrix[0][i])rz=0;// 第0行有0
        for(int i=0;i<n;i++)
            if(!matrix[i][0])cz=0;// 第0列有0
        for(int i=1;i<n;i++)
            for(int j=1;j<m;j++)
                if(!matrix[i][j]){
                    matrix[0][j]=0;// 存在0，这一行、一列都归零
                    matrix[i][0]=0;
                }
        for(int i=1;i<m;i++){
            if(!matrix[0][i])// 这一列归零
                for(int j=1;j<n;j++)matrix[j][i]=0;
        }
        for(int i=1;i<n;i++)
            if(!matrix[i][0])// 这一行归零
                for(int j=1;j<m;j++)matrix[i][j]=0;
        
        // 第0行、第0列全部归零
        if(!rz)
            for(int i=0;i<m;i++)matrix[0][i]=0;
        if(!cz)
            for(int i=0;i<n;i++)matrix[i][0]=0;
    }
};
```

- 时间：m*n
- 空间：1





代码已经非常高效，但可以通过以下方式提高可读性：

1. 使用更清晰的变量名。
2. 将重复的逻辑提取为函数。

```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int n = matrix.size(), m = matrix.size();
        bool firstRowZero = false, firstColZero = false;

        // Check if first row needs to be zeroed
        for (int j = 0; j < m; j++) {
            if (matrix[j] == 0) {
                firstRowZero = true;
                break;
            }
        }

        // Check if first column needs to be zeroed
        for (int i = 0; i < n; i++) {
            if (matrix[i] == 0) {
                firstColZero = true;
                break;
            }
        }

        // Mark rows and columns to be zeroed
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i] = 0;
                    matrix[j] = 0;
                }
            }
        }

        // Zero marked rows
        for (int i = 1; i < n; i++) {
            if (matrix[i] == 0) {
                for (int j = 1; j < m; j++) matrix[i][j] = 0;
            }
        }

        // Zero marked columns
        for (int j = 1; j < m; j++) {
            if (matrix[j] == 0) {
                for (int i = 1; i < n; i++) matrix[i][j] = 0;
            }
        }

        // Zero first row if needed
        if (firstRowZero) {
            for (int j = 0; j < m; j++) matrix[j] = 0;
        }

        // Zero first column if needed
        if (firstColZero) {
            for (int i = 0; i < n; i++) matrix[i] = 0;
        }
    }
};
```



