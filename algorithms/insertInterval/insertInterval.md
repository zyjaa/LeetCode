[57. 插入区间](https://leetcode.cn/problems/insert-interval/)

**示例 1：**

```
输入：intervals = [[1,3],[6,9]], newInterval = [2,5]
输出：[[1,5],[6,9]]
```



### 1、模拟

```cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& a, vector<int>& b) {
        vector<vector<int>> res;
        int k=0;
        while(k<a.size() && a[k][1]<b[0])res.push_back(a[k++]);// 将所有在新区间 b 之前的区间加入结果
        if(k<a.size()){
            b[0]=min(b[0],a[k][0]);// b左端点取最小值，因为a可能在b区间里面
            // 找到b右端点小于后面的左端点的最右边的一个区间
            while(k<a.size() && b[1]>=a[k][0])b[1]=max(b[1],a[k++][1]);
        }
        res.push_back(b);
        while(k<a.size())res.push_back(a[k++]);
        return res;
    }
};
```

- 时间：O(n)，遍历所有区间
- 空间：O(n)