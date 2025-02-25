###  1、拓扑排序

```cpp
class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        queue<int> q; // 用来存储入度为0的课程
        int cnt = 0; // 用来记录已经处理的课程数
        vector<vector<int>> g(numCourses); // 邻接表，表示课程的依赖关系
        vector<int> d(numCourses); // 记录每门课程的入度
        for (auto x : prerequisites) { // 遍历所有先修关系
            int a = x, b = x; // a是b的先修课程
            g[a].push_back(b); // 修完a后可以修b
            d[b]++; // b的入度加1
        }
        for (int i = 0; i < numCourses; i++) // 把所有入度为0的课程加入队列
            if (!d[i]) q.push(i);
        while (q.size()) { // 开始拓扑排序
            auto t = q.front(); // 取出队首课程
            q.pop();
            cnt++; // 处理的课程数加1
            for (auto x : g[t]) { // 遍历t能解锁的课程
                if (--d[x] == 0) q.push(x); // 解锁课程x的入度减1，如果入度为0，加入队列
            }
        }
        return cnt == numCourses; // 判断是否处理了所有课程
    }
};
```



