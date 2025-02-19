[56. 合并区间](https://leetcode.cn/problems/merge-intervals/)：能合并的合并

**示例 1：**

```
输入：intervals = [[1,3],[2,6],[8,10],[15,18]]
输出：[[1,6],[8,10],[15,18]]
解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
```



### 1、模拟

- 按左端点排序合并就完了

- **默认排序规则**：按左端点排序，左端点相同则按右端点排序。

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(),intervals.end());
        vector<vector<int>> res;
        int l=intervals[0][0],r=intervals[0][1];
        for(int i=1;i<intervals.size();i++){
            if(intervals[i][0]>r){// 合并不了
                res.push_back({l,r});
                l=intervals[i][0], r=intervals[i][1];
            }else{
                r=max(intervals[i][1],r);
            }
        }
        res.push_back({l,r});
        return res;
    }
};
```

- 时间：O(n)，区间个数
- 空间：O(n)