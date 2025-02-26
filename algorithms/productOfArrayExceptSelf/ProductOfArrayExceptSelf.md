```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n=nums.size();
        vector<int> p(n,1);
        for(int i=1;i<n;i++)p[i]=p[i-1]*nums[i-1];//p[i]：不包含下标i
        int s=1;
        for(int i=n-1;i>=0;i--){
            p[i]*=s;
            s*=nums[i];
        }
        return p;
    }
};
```

 
