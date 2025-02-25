###  1、预处理+堆

```cpp
class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        vector<vector<int>> res; // 存储结果
        vector<pair<int, int>> events; // 存储事件

        // 处理建筑物的左右边界
        for (auto& b : buildings) {
            events.push_back({b, -b}); // 左边界，高度增加
            events.push_back({b, b}); // 右边界，高度减少
        }

        // 按x坐标排序
        sort(events.begin(), events.end());

        // 优先队列（堆），存储当前所有高度
        priority_queue<int> heap;
        heap.push(0); // 初始高度为0
        int prevMax = 0; // 前一个最大高度

        // 扫描线算法
        for (auto& e : events) {
            int x = e.first; // 当前x坐标
            int h = e.second; // 当前高度变化

            if (h < 0) {
                heap.push(-h); // 左边界，高度增加
            } else {
                // 右边界，高度减少
                auto it = heap.find(h);
                if (it != heap.end()) heap.erase(it);
            }

            int currMax = heap.top(); // 当前最大高度
            if (currMax != prevMax) { // 如果最大高度发生变化
                res.push_back({x, currMax}); // 记录关键点
                prevMax = currMax; // 更新前一个最大高度
            }
        }

        return res; // 返回结果
    }
};
```

### 时间复杂度：

1. **排序事件**：O(n log n)，其中 `n` 是建筑物的数量。
2. **扫描线算法**：O(n log n)，每个事件的处理时间为 O(log n)。
3. **总时间复杂度**：O(n log n)。
