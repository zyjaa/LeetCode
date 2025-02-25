### 1、位运算

第1位不同的数开始向后都是0，比如011,101（011->101：011，100，101）

```cpp 
class Solution {
public:
    int rangeBitwiseAnd(int left, int right) {
        int res = 0; // 初始化结果为0
        for (int i = 30; i >= 0; i--) { // 从最高位（第30位）开始检查
            if ((left >> i) ^ (right >> i)) break; // 如果left和right在这一位不同，退出循环
            if (left >> i & 1) res |= 1 << i; // 如果left和right在这一位相同且为1，将结果中这一位设为1
        }
        return res; // 返回最终结果
    }
};
```

1，1



