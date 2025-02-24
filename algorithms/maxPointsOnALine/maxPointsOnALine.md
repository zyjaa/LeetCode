### 1、哈希表

```cpp
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        int res = 0; // 记录最终结果
        typedef long double ld; // 使用高精度的 long double 表示斜率

        // 遍历每个点作为基准点
        for (auto& p : points) {
            unordered_map<ld, int> cnt; // 哈希表，记录以 p 为基准点的直线的斜率及其对应的点数
            int a = 0, b = 0; // a 记录与 p 重合的点数，b 记录与 p 在同一垂直线上的点数

            // 遍历其他点
            for (auto& q : points) {
                if (p == q) {
                    a++; // 与 p 重合
                } else if (p[0] == q[0]) {
                    b++; // 与 p 在同一垂直线（斜率无穷大）
                } else {
                    // 计算斜率
                    ld k = (ld)(p[1] - q[1]) / (p[0] - q[0]);
                    cnt[k]++; // 统计该斜率对应的点数
                }
            }

            int c = b; // c 记录当前基准点的最大点数
            for (auto [k, v] : cnt) {
                c = max(c, v); // 更新 c 为斜率对应的最大点数
            }
            res = max(res, a + c); // 更新全局结果
        }
        return res;
    }
};
```

- 时间：O($$n^2$$)
- 空间：n，所有点在一条直线



用string代替ld，用分数形式表示解决高精度问题

```cpp
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        int res = 0;
        for (auto& p : points) {
            unordered_map<string, int> cnt;
            int a = 0; // 重合点数
            for (auto& q : points) {
                if (p == q) {
                    a++;
                } else {
                    int dx = q - p, dy = q - p;
                    int g = gcd(dx, dy); // 最大公约数
                    string k = to_string(dy / g) + "/" + to_string(dx / g); // 分数形式
                    cnt[k]++;
                }
            }
            int c = 0;
            for (auto [k, v] : cnt) c = max(c, v);
            res = max(res, a + c);
        }
        return res;
    }

    int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }
};
```

