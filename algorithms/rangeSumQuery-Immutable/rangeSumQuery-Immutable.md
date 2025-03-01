### 1、前缀和

```
class NumArray {
public:
    vector<int> s;
    NumArray(vector<int>& nums) {
        int n=nums.size();
        s.resize(n);
        s[0]=nums[0];
        for(int i=1;i<n;i++)s[i]=s[i-1]+nums[i];
    }
    
    int sumRange(int left, int right) {
        if(left)return s[right]-s[left-1];
        return s[right];
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray* obj = new NumArray(nums);
 * int param_1 = obj->sumRange(left,right);
 */
```

