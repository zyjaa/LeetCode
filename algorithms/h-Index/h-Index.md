```
class Solution {
public:
    int hIndex(vector<int>& citations) {
        // 将引用次数从大到小排序
        sort(citations.begin(), citations.end(), greater<int>());

        // 遍历可能的 h 值
        for (int h = citations.size(); h > 0; h--) {
            // 检查是否满足 H 指数的条件
            if (citations[h - 1] >= h) {
                return h;
            }
        }

        // 如果没有满足条件的 h，返回 0
        return 0;
    }
};
```

