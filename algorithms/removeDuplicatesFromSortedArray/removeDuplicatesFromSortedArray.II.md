[80. 删除有序数组中的重复项 II](https://leetcode.cn/problems/remove-duplicates-from-sorted-array-ii/)

给你一个有序数组 `nums` ，请你**[ 原地](http://baike.baidu.com/item/原地算法)** 删除重复出现的元素，使得出现次数超过两次的元素**只出现两次** ，返回删除后数组的新长度。

不要使用额外的数组空间，你必须在 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组** 并在使用 O(1) 额外空间的条件下完成。



### 1、模拟

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int k=0;
        for(auto& x:nums){
            //小于2个直接进
            //左边第1个不等于当前数
            //左边第2个不等于当前数
            //再多就超了，不加入
            if(k<2 || (nums[k-1]!=x || nums[k-2]!=x))nums[k++]=x;
        }
        return k;
    }
};
```

- 时间：n
- 空间：1