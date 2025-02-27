1. 如果一个活细胞周围有 2 或 3 个活细胞，则它继续存活，否则死亡。
2. 如果一个死细胞周围恰好有 3 个活细胞，则它复活。
3. 其他情况下，细胞保持死亡状态。

```
class Solution {
public:
    void gameOfLife(vector<vector<int>>& board) {
        if (board.empty() || board.empty()) return;  // 边界检查

        int n = board.size(), m = board.size();

        // 遍历每个细胞
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                // 统计周围活细胞的数量
                int live_count = 0;
                for (int x = max(i - 1, 0); x <= min(i + 1, n - 1); x++) {
                    for (int y = max(j - 1, 0); y <= min(j + 1, m - 1); y++) {
                        if ((x != i || y != j) && (board[x][y] & 1)) {
                            live_count++;
                        }
                    }
                }

                // 计算下一状态
                int cur_state = board[i][j] & 1;  // 当前状态
                int next_state = 0;               // 下一状态
                if (cur_state) {
                    if (live_count == 2 || live_count == 3) {
                        next_state = 1;  // 存活
                    }
                } else {
                    if (live_count == 3) {
                        next_state = 1;  // 复活
                    }
                }

                // 将下一状态存储在第二位
                board[i][j] |= next_state << 1;
            }
        }

        // 更新所有细胞的状态
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                board[i][j] >>= 1;  // 右移一位，更新为下一状态
            }
        }
    }
};
```

