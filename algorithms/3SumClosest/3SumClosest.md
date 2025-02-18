**题意**：最接近target的三数之和

**示例 1：**

```
输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2)。
```

**示例 2：**

```
输入：nums = [0,0,0], target = 1
输出：0
解释：与 target 最接近的和是 0（0 + 0 + 0 = 0）。
```



### 法一：排序+3指针

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(),nums.end());
        pair<int,int> res(INT_MAX,INT_MAX);
        for(int i=0;i<nums.size();i++){
            for(int j=i+1,k=nums.size()-1;j<k;j++){
                while(j<k-1 && nums[i]+nums[j]+nums[k-1]>=target)k--;
                int s=nums[i]+nums[j]+nums[k];
                res=min(res,make_pair(abs(target-s),s));
                if(j<k-1){
                    s=nums[i]+nums[j]+nums[k-1];
                    res=min(res,make_pair(abs(target-s),s));
                }
            }
        }
        return res.second;
    }
};
```

- 时间复杂度：O($$N^2$$)
- 空间复杂的：O($$logN$$)