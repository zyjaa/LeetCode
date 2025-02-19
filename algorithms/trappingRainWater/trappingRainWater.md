[42. 接雨水](https://leetcode.cn/problems/trapping-rain-water)

给定 `n` 个非负整数表示每个宽度为 `1` 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rainwatertrap.png)

```
输入：height = [0,1,0,2,1,0,1,3,2,1,2,1]
输出：6
解释：上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 
```

**示例 2：**

```
输入：height = [4,2,0,3,2,5]
输出：9
```



### 法一：贪心

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int n=height.size();
        vector<int>l(n),r(n);
        l[0]=height[0],r[n-1]=height[n-1];
        for(int i=1;i<n;i++)l[i]=max(l[i-1],height[i]);
        for(int i=n-2;i>=0;i--)r[i]=max(r[i+1],height[i]);
        int ans=0;
        //左边右边的最小值-自己高度就自己高度能盛的最大水量
        for(int i=0;i<n;i++)ans+=min(l[i],r[i])-height[i];
        return ans;
    }
};
```

- 时间：O($$n$$)
- 空间：O($$n$$)，2数组

