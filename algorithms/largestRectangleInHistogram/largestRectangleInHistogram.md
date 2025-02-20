[84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/)

给定 *n* 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

 

**示例 1:**

![img](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

```
输入：heights = [2,1,5,6,2,3]
输出：10
解释：最大的矩形为图中红色区域，面积为 10
```



### 1、单调栈

```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n = heights.size();
        vector<int> l(n), r(n); // l[i] 和 r[i] 分别记录第 i 个柱子左边和右边第一个比它矮的柱子的下标
        stack<int> stk; // 单调栈，用于维护柱子的下标

        // 从左到右遍历，找到每个柱子左边第一个比它矮的柱子
        for (int i = 0; i < n; i++) {
            // 维护单调栈：栈顶元素对应的柱子高度 >= 当前柱子高度时，弹出栈顶
            while (stk.size() && heights[stk.top()] >= heights[i]) stk.pop();
            // 如果栈为空，说明左边没有比当前柱子矮的柱子，记为 -1
            if (stk.empty()) l[i] = -1;
            // 否则，栈顶就是左边第一个比当前柱子矮的柱子
            else l[i] = stk.top();
            // 将当前柱子下标入栈
            stk.push(i);
        }

        // 清空栈，准备从右到左遍历
        stk = stack<int>();

        // 从右到左遍历，找到每个柱子右边第一个比它矮的柱子
        for (int i = n - 1; i >= 0; i--) {
            // 维护单调栈：栈顶元素对应的柱子高度 >= 当前柱子高度时，弹出栈顶
            while (stk.size() && heights[stk.top()] >= heights[i]) stk.pop();
            // 如果栈为空，说明右边没有比当前柱子矮的柱子，记为 n
            if (stk.empty()) r[i] = n;
            // 否则，栈顶就是右边第一个比当前柱子矮的柱子
            else r[i] = stk.top();
            // 将当前柱子下标入栈
            stk.push(i);
        }

        // 计算最大矩形面积
        int res = 0;
        for (int i = 0; i < n; i++) {
            // 矩形面积 = 高度 * (右边界 - 左边界 - 1)
            res = max(res, heights[i] * (r[i] - l[i] - 1));
        }

        return res;
    }
};
```

- 时间：n
  - 遍历数组 `heights`，每个柱子最多入栈和出栈一次。因此，从左到右遍历的总时间复杂度是 O(n)。右遍历同理
  - 弹出去就弹出去了，非遍历数组一样可以重复使用，栈里的东西都是一次性用品
- 空间：n