###  1、预处理+堆

```cpp
class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        vector<vector<int>> res; // 存储结果
        vector<pair<int, int>> events; // 存储事件

        // 处理建筑物的左右边界
        for (auto& b : buildings) {
            events.push_back({b[0], -b[2]}); // 左边界，高度增加
            events.push_back({b[1], b[2]}); // 右边界，高度减少
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

- 堆可以在 O(1) 时间内获取当前的最大高度。
- 使用优先队列（堆）维护当前的最大高度。
  - **插入操作**：每次插入的时间复杂度是 **O(log n)**。
  - **删除操作**：每次删除的时间复杂度是 **O(log n)**。
- 扫描线算法需要处理 `2n` 个事件（每个建筑物有 2 个事件），因此总时间复杂度是 **O(n log n)**。

- **左边界事件**：**判断是否需要记录关键点**：如果当前高度大于之前的最大高度，说明天际线高度发生了变化，记录关键点。
- **右边界事件**：**判断是否需要记录关键点**：如果移除高度后，堆顶的最大高度小于之前记录的最大高度，说明天际线高度发生了变化，记录关键点。



