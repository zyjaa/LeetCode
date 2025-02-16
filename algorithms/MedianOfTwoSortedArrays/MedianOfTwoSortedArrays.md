**题意**：寻找两个正序数组合并后的中位数，算法的时间复杂度应该为 `O(log (m+n))` 


示例 1：

```
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
```

**示例 2：**

```
输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
```

 

 

**提示：**

- `nums1.length == m`
- `nums2.length == n`
- `0 <= m <= 1000`
- `0 <= n <= 1000`
- `1 <= m + n <= 2000`
- `-106 <= nums1[i], nums2[i] <= 106`



### 法一：二分+分治

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int n=nums1.size()+nums2.size();
        if(n%2){
            return find(nums1,0,nums2,0,n/2+1);
        }else{
            int l=find(nums1,0,nums2,0,n/2);
            int r=find(nums1,0,nums2,0,n/2+1);
            return (l+r)/2.0;
        }
    }
    
    // 找第
    int find(vector<int>& nums1,int i,vector<int>& nums2,int j,int k){
        if(nums1.size()-i>nums2.size()-j)return find(nums2,j,nums1,i,k);
        if(k==1){
            if(i==nums1.size())return nums2[j];
            return min(nums1[i],nums2[j]);
        }
        if(i==nums1.size())return nums2[j+k-1];
        int si=min((int)nums1.size(),i+k/2),sj=j+k/2;
        if(nums1[si-1]>nums2[sj-1])return find(nums1,i,nums2,sj,k-(sj-j));
        return find(nums1,si,nums2,j,k-(si-i));
    }
};
```

每次递归调用通过比较两个数组中第 `k/2` 个元素，排除其中一个数组的前 `k/2` 个元素



- 时间复杂度：O(log(min(m, n)))，由于每次递归 `k` 减少约一半，最多递归 `logk` 次。对于中位数问题，`k` 最大为 `(m+n)/2 +1`，因此时间复杂度为 `O(log(m+n))`。但通过优先处理较短的数组（`nums1` 长度 ≤ `nums2`），实际时间复杂度优化为 **O(log(min(m, n)))**。
- 空间复杂度：O(log(min(m, n)))，递归深度与 `k` 的对数相关，最大深度为 `O(log(min(m, n)))`，因此空间复杂度为 **O(log(min(m, n)))**。若使用迭代实现，可优化至O(1)



**迭代优化**

```cpp
class Solution {
    public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size() + nums2.size();
        auto findKth = [&](int k) { // 封装为内部函数
            int i = 0, j = 0;
            while (true) {
                // 确保 nums1 剩余长度更短 (优化关键点)
                if (nums1.size() - i > nums2.size() - j) swap(nums1, nums2), swap(i, j);

                // 处理 nums1 耗尽的情况
                if (i == nums1.size()) return nums2[j + k - 1];

                // 直接返回条件
                if (k == 1) return min(nums1[i], nums2[j]);

                // 计算排除位置 (注意防越界)
                int offset = k / 2;
                int ni = min(i + offset, (int)nums1.size());
                int nj = j + offset;

                // 排除较小段并更新 k
                if (nums1[ni - 1] <= nums2[nj - 1]) {
                    k -= ni - i;
                    i = ni;
                } else {
                    k -= nj - j;
                    j = nj;
                }
            }
        };

        if (n % 2) return findKth(n / 2 + 1);
        return (findKth(n / 2) + findKth(n / 2 + 1)) / 2.0;
    }
};
```









