### 1、拓扑排序

```
class Solution {
public:
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        vector<int> d(numCourses); // 记录每门课程的入度
        vector<vector<int>> g(numCourses); // 邻接表，表示课程的依赖关系
        for (auto x : prerequisites) { // 遍历所有先修关系
            int a = x[1], b = x[0]; // a是b的先修课程
            g[a].push_back(b); // 修完a后可以修b
            d[b]++; // b的入度加1
        }
        vector<int> res; // 用来存储合法的学习顺序
        int cnt = 0; // 用来记录已经处理的课程数
        queue<int> q; // 用来存储入度为0的课程
        for (int i = 0; i < numCourses; i++) // 把所有入度为0的课程加入队列
            if (!d[i]) q.push(i);
        while (q.size()) { // 开始拓扑排序
            auto t = q.front(); // 取出队首课程
            q.pop();
            cnt++; // 处理的课程数加1
            res.push_back(t); // 把当前课程加入学习顺序
            //遍历边（O(E)
            for (auto x : g[t]) { // 遍历t能解锁的课程
                if (--d[x] == 0) q.push(x); // 解锁课程x的入度减1，如果入度为0，加入队列
            }
        }
        if (cnt == numCourses) return res; // 如果处理了所有课程，返回学习顺序
        return vector<int>(); // 否则返回空数组
    }
};
```

 时间复杂度：O(V + E)

- 建图：O(E)，其中E是先修关系的数量。
- 拓扑排序：O(V + E)，其中V是课程数，E是先修关系数。

空间复杂度是 O(V + E)。





### O(V + E) 的组成部分：

1. **初始化阶段**：
   - **统计入度**：`for (auto x : prerequisites)` 循环遍历所有的边（先修关系），时间复杂度是 **O(E)**。
   - **初始化队列**：`for (int i = 0; i < numCourses; i++)` 循环遍历所有的节点（课程），时间复杂度是 **O(V)**。
   - **总时间复杂度**：O(V) + O(E)。
2. **拓扑排序阶段**：
   - **处理队列**：`while (q.size())` 循环会处理所有的节点，每个节点只会被处理一次，时间复杂度是 **O(V)**。
   - **遍历边**：`for (auto x : g[t])` 循环会遍历所有的边，每条边只会被遍历一次，时间复杂度是 **O(E)**。
   - **总时间复杂度**：O(V) + O(E)。
3. **总时间复杂度**：
   - 初始化阶段：O(V) + O(E)。
   - 拓扑排序阶段：O(V) + O(E)。
   - 所以总时间复杂度是 **O(V + E)**。
