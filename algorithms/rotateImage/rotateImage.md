[48. 旋转图像](https://leetcode.cn/problems/rotate-image/)

给定一个 *n* × *n* 的二维矩阵 `matrix` 表示一个图像。请你将图像顺时针旋转 90 度。

你必须在**[ 原地](https://baike.baidu.com/item/原地算法)** 旋转图像，这意味着你需要直接修改输入的二维矩阵。**请不要** 使用另一个矩阵来旋转图像。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)

```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[[7,4,1],[8,5,2],[9,6,3]]
```



### 法一：模拟

先按主对角线翻转，然后按中间的y轴对称翻转

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& f) {
        int n=f.size(),m=f[0].size();
        for(int i=0;i<f.size();i++){
            for(int j=0;j<i;j++)swap(f[i][j],f[j][i]);
        }
        for(int i=0;i<n;i++){
            for(int j=0,k=n-1;j<k;j++,k--)swap(f[i][j],f[i][k]);
        }
    }
};
```

- 时间：O($$n^2$$)
- 空间：O($$1$$)