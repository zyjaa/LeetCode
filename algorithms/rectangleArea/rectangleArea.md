1. **计算两个矩形的面积**：
   - 第一个矩形的面积：`(ay2 - ay1) * (ax2 - ax1)`。
   - 第二个矩形的面积：`(by2 - by1) * (bx2 - bx1)`。
2. **计算重叠部分的面积**：
   - 重叠部分的宽度：`x = max(0ll, min(ax2, bx2) - max(ax1, bx1))`。//左边选大的，右边选小的
   - 重叠部分的高度：`y = max(0ll, min(ay2, by2) - max(ay1, by1))`。//上边选小的，下边选大的
   - 重叠部分的面积：`x * y`。
3. **计算覆盖的总面积**：
   - 总面积 = 第一个矩形的面积 + 第二个矩形的面积 - 重叠部分的面积。

 

```
using ll = long long; // 定义别名 ll 为 long long 类型

class Solution {
public:
    int computeArea(ll ax1, ll ay1, ll ax2, ll ay2, ll bx1, ll by1, ll bx2, ll by2) {
        // 计算重叠部分的宽度 x
        ll x = max(0ll, min(ax2, bx2) - max(ax1, bx1));
        // 计算重叠部分的高度 y
        ll y = max(0ll, min(ay2, by2) - max(ay1, by1));
        // 总面积 = 第一个矩形的面积 + 第二个矩形的面积 - 重叠部分的面积
        return (ay2 - ay1) * (ax2 - ax1) + (by2 - by1) * (bx2 - bx1) - x * y;
    }
};
```

