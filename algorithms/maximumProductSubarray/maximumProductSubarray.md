 最大值=max(最小值\*cur，最大值\*cur，cur)

最小值=min(cur,最小值\*cur,最大值\*cur)

```cpp
class Solution {
public:
    int maxProduct(vector<int>& a) {
        // 最大值，最小值
        int res=a[0];
        int maxn=res,minn=res;
        for(int i=1;i<a.size();i++){
            int t=maxn;
            maxn=max(a[i],max(maxn*a[i],minn*a[i]));
            minn=min(a[i],min(t*a[i],minn*a[i]));
            res=max(res,maxn);
        }
        return res;
    }
};
```

n,1
