### 1、模拟

```cpp 
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n = gas.size(); // 加油站的数量
        for (int i = 0, j = 0; i < n;) {//遍历所有起点
            int s = 0; // 当前油量
            for (j = 0; j < n; j++) {
                int t = (i + j) % n; // 当前加油站索引（循环）
                s += gas[t] - cost[t]; // 加油并消耗
                if (s < 0) break; // 如果油量不足，退出内层循环
            }
            if (j == n) return i; // 如果成功绕完所有加油站，返回起点 i
            i = i + j + 1; // 否则，从下一个可能的起点开始
        }
        return -1; // 如果没有找到起点，返回 -1
    }
};
```

- 时间：n
- 空间：1
