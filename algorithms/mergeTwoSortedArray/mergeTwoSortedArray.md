[88. 合并两个有序数组](https://leetcode.cn/problems/merge-sorted-array/)

**示例 1：**

```
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
解释：需要合并 [1,2,3] 和 [2,5,6] 。
合并结果是 [1,2,2,3,5,6] ，其中斜体加粗标注的为 nums1 中的元素。
```



### 1、模拟

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int k=m+n-1;
        int x=m-1,y=n-1;
        while(x>=0 && y>=0){
            if(nums1[x]>=nums2[y])nums1[k--]=nums1[x--];
            else nums1[k--]=nums2[y--];
        }
        while(y>=0)nums1[k--]=nums2[y--];
    }
};
```

- 时间：n
- 空间：1