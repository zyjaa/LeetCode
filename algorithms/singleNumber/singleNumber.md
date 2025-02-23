### 1、异或

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res=0;
        for(auto x:nums)res^=x;
        return res;
        //0^x=x
    }
};
```

n，1



后面可能有出现2次，利用不同位数

出现只有一个出现k次的数，用哈希表统计下，k次就是哈希表里有k次
