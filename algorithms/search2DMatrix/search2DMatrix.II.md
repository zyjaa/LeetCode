### 1、二分

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int n=matrix.size(),m=matrix[0].size();
        int i=0,j=m-1;
        while(i<n && j>=0){
            int x=matrix[i][j];//最后一列
            if(x==target)return true;
            else if(x<target)i++;//当前行最后一列小于target，下一行
            else j--;//当前行最有一列大于target，往前面的列找找，一定在这行，因为target肯定大于上一行，小于这一列
        }
        return false;
    }
};
```

- 时间复杂度

  - 从矩阵的右上角开始查找，每次循环要么向下移动一行，要么向左移动一列。

  - 最多需要移动 `n` 行和 `m` 列。

  - 因此，时间复杂度为 O(n+m)。
