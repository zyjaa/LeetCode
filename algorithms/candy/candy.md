### 1、贪心

- 每个孩子至少分配到 `1` 个糖果。
- 相邻两个孩子评分更高的孩子会获得更多的糖果。

左一趟右一趟

```cpp
class Solution {
public:
    int candy(vector<int>& a) {
        int n=a.size();
        vector<int> l(n),r(n);
        for(int i=0;i+1<n;i++){
            if(a[i+1]>a[i])l[i+1]=l[i]+1;//比左边孩子多1个
        }
        for(int i=n-1;i-1>=0;i--){
            if(a[i-1]>a[i])r[i-1]=r[i]+1;//比右边孩子多1个
        }
        int res=0;
        for(int i=0;i<n;i++)res+=max(l[i],r[i])+1;//每个孩子至少1个，所以加1
        return res;
    }
};
```

- 时间：n
- 空间：n

注：不用过于关注LeetCode难度如何，很多是虚标的，把困难题当简单题做就好了
