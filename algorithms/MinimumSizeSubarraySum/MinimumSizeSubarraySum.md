### 1、滑动窗口

```
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int res=INT_MAX;
        int s=0;
        for(int i=0,j=0;i<nums.size();i++){
            s+=nums[i];
            while(s-nums[j]>=target)s-=nums[j++];
            if(s>=target)res=min(res,i-j+1);
        }
        if(res==INT_MAX)return 0;
        return res;
    }
};
```

 
