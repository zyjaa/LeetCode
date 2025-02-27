### 1、对顶堆

```cpp
class MedianFinder {
private:
    priority_queue<int> max_heap;  // 存储较小的一半数字（最大堆）
    priority_queue<int, vector<int>, greater<int>> min_heap;  // 存储较大的一半数字（最小堆）

public:
    MedianFinder() {
        // 构造函数，无需额外操作
    }

    void addNum(int num) {
        if (max_heap.empty() || num <= max_heap.top()) {
            // 如果 num 小于等于 max_heap 的堆顶元素，插入 max_heap
            max_heap.push(num);
            if (max_heap.size() > min_heap.size() + 1) {
                // 如果 max_heap 的大小超过 min_heap 的大小加 1，平衡两个堆
                min_heap.push(max_heap.top());
                max_heap.pop();
            }
        } else {
            // 否则，插入 min_heap
            min_heap.push(num);
            if (min_heap.size() > max_heap.size()) {
                // 如果 min_heap 的大小超过 max_heap 的大小，平衡两个堆
                max_heap.push(min_heap.top());
                min_heap.pop();
            }
        }
    }

    double findMedian() {
        if (max_heap.size() > min_heap.size()) {
            // 如果 max_heap 的大小更大，返回 max_heap 的堆顶元素
            return max_heap.top();
        } else {
            // 否则，返回两个堆顶元素的平均值
            return (max_heap.top() + min_heap.top()) / 2.0;
        }
    }
};
```

### **复杂度分析**

1. **`addNum(int num)`**：
   - 插入堆：`O(log n)`，其中 `n` 是堆的大小。
   - 平衡堆：`O(log n)`。
   - 总时间复杂度：`O(log n)`。
2. **`findMedian()`**：
   - 访问堆顶元素：`O(1)`。
   - 总时间复杂度：`O(1)`。
3. **空间复杂度**：
   - 使用了两个堆，空间复杂度为 `O(n)`，其中 `n` 是数据流中的元素个数。
