### 1、摩尔投票

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int cur=0,cnt=0;
        for(auto x:nums){
            if(!cnt)cur=x,cnt++;
            else if(cur!=x)cnt--;
            else cnt++;
        }
        return cur;
    }
};
```

