题目：https://blog.csdn.net/qq_29051413/article/details/108679736

### 1、哈希表

```cpp
class TwoSum {
private:
    unordered_map<int, int> numCount; // 存储数字及其出现次数

public:
    // 添加一个数
    void add(int number) {
        numCount[number]++;
    }

    // 判断是否存在两个数，使得它们的和等于 value
    bool find(int value) {
        for (auto& [num, count] : numCount) {
            int target = value - num;
            if (numCount.find(target) != numCount.end()) {
                // 如果 target 等于 num，需要确保 num 至少出现两次
                if (target != num || count > 1) {
                    return true;
                }
            }
        }
        return false;
    }
};
```

###  **时间复杂度**：

1. - `add` 操作：**O(1)**。
   - `find` 操作：**O(n)**，其中 `n` 是哈希表中数字的数量。
2. **空间复杂度**：
   - 哈希表的空间复杂度为 **O(n)**。
