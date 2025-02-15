 题意：找两个不同下标的数，相加为target，找出一个符合此条件的下标对

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

 

**提示：**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **只会存在一个有效答案**

 

**进阶**：你可以想出一个时间复杂度小于 `O(n2)` 的算法吗？





### 法一：暴力

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int i,j;
        for(i=0;i<nums.size()-1;i++){
            for(j=i+1;j<nums.size();j++){
                if(nums[i]+nums[j]==target){
                   return {i,j};
                }
            }
        }
        return {};
    };
};
```

- 时间复杂度：O(N)，两个1-n的循环
- 空间复杂度：O(1)





### 法二：哈希表

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> map;
        for(int i=0;i<nums.size();i++){
            if(map.count(target-nums[i]))return {i,map[target-nums[i]]};
            map[nums[i]]=i;
        }
        return {};
    }
};
```

- 时间复杂度：O(N)，1层循环，哈希表count/contains时间复杂度平均为O(1)

- 空间复杂度：O(N)，哈希表开销，存放nums的所有元素N













