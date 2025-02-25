```
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        return q_sort(nums,0,nums.size()-1,k);   
    }
    int q_sort(vector<int>& nums,int l,int r,int k){
        if(l>=r)return nums[l];
        int x=nums[l+r>>1],i=l-1,j=r+1;
        while(i<j){
            do i++;while(nums[i]>x);
            do j--;while(nums[j]<x);
            if(i<j)swap(nums[i],nums[j]);
        }
        if((j-l+1)>=k)return q_sort(nums,l,j,k);
        return q_sort(nums,j+1,r,k-(j-l+1));
    }
};
```

 
