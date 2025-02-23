- `nums` 中，除某个元素仅出现 **一次** 外，其余每个元素都恰出现 **三次**

 

### 1、模拟

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        // %3==0  %3==1
        int n=nums.size();
        int res=0;
        for(int i=0;i<32;i++){
            int c=0;
            for(int j=0;j<n;j++)c+=nums[j]>>i&1;
            res+=(c%3)<<i;//出现3次就是0，出现1次就是这个数，可能都有1，那就是4，%3也是1
        }
        return res;
    }
};
```

n,1
