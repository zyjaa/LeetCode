[75. 颜色分类](https://leetcode.cn/problems/sort-colors/)

给定一个包含红色、白色和蓝色、共 `n` 个元素的数组 `nums` ，**[原地](https://baike.baidu.com/item/原地算法)** 对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

我们使用整数 `0`、 `1` 和 `2` 分别表示红色、白色和蓝色。



必须在不使用库内置的 sort 函数的情况下解决这个问题。

 

**示例 1：**

```
输入：nums = [2,0,2,1,1,0]
输出：[0,0,1,1,2,2]
```



### 1、3指针

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int n=nums.size()-1;
        // j:0
        // k:2
        for(int i=0,j=0,k=n;i<=k;){
            if(nums[i]==0)swap(nums[i++],nums[j++]);// 当前数为0，扔到i
            else if(nums[i]==2)swap(nums[i],nums[k--]);// 当前数为2，扔到k
            else i++;
        }
    }
};
```

- 时间：n
- 空间：1