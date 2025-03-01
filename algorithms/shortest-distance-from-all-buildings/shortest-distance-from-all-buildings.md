### 1、BFS

- 对每个建筑物，使用 **广度优先搜索（BFS）** 计算它到所有空地的距离。
- 对于每个空地，累加所有建筑物到它的距离。
- 找到距离之和最小的空地。

```
#include <vector>
#include <queue>
#include <climits>
using namespace std;

class Solution {
public:
    int shortestDistance(vector<vector<int>>& grid) {
        int m = grid.size(); // 网格的行数
        int n = grid.size() ? grid.size() : 0; // 网格的列数
        vector<vector<int>> totalDist(m, vector<int>(n, 0)); // 存储每个空地的距离之和
        int minDist = INT_MAX; // 最小距离之和
        int buildings = 0; // 建筑物的数量
        int dx[] = {-1, 1, 0, 0}; // 方向数组
        int dy[] = {0, 0, -1, 1};

        // 遍历网格，统计建筑物的位置
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    buildings++;
                    // 对每个建筑物进行 BFS
                    queue<pair<int, int>> q;
                    q.push({i, j});
                    vector<vector<int>> dist(m, vector<int>(n, INT_MAX)); // 当前建筑物到各空地的距离
                    dist[i][j] = 0; // 建筑物到自身的距离为 0

                    while (!q.empty()) {
                        auto curr = q.front();
                        q.pop();
                        int x = curr.first, y = curr.second;

                        // 遍历四个方向
                        for (int k = 0; k < 4; k++) {
                            int nx = x + dx[k], ny = y + dy[k];
                            if (nx >= 0 && nx < m && ny >= 0 && ny < n && grid[nx][ny] == 0 && dist[nx][ny] == INT_MAX) {
                                dist[nx][ny] = dist[x][y] + 1; // 更新距离
                                q.push({nx, ny});
                            }
                        }
                    }

                    // 将当前建筑物的距离累加到 totalDist
                    for (int x = 0; x < m; x++) {
                        for (int y = 0; y < n; y++) {
                            if (grid[x][y] == 0 && dist[x][y] != INT_MAX) {//当前空地与此建筑的距离
                                totalDist[x][y] += dist[x][y];
                            }
                        }
                    }
                }
            }
        }

        // 找到最小距离之和
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 0 && totalDist[i][j] < minDist) {
                    minDist = totalDist[i][j];
                }
            }
        }

        return minDist == INT_MAX ? -1 : minDist; // 返回结果
    }
};
```

1. **时间复杂度**：O(m2⋅n2)，其中 m*m* 和 n*n* 是网格的行数和列数。每个建筑物需要一次 BFS，时间复杂度为 O(m⋅n)*O*(*m*⋅*n*)。
2. **空间复杂度**：O(m⋅n)，用于存储距离数组和 BFS 队列。
