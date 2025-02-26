### 1、数学

```cpp
class Solution {
public:
    int countDigitOne(int n) {
        if (n <= 0) return 0;

        int res = 0;
        long long p = 1; // 用于计算权重

        while (p <= n) {
            int left = n / (p * 10); // 当前位左侧的数字
            int right = n % p;       // 当前位右侧的数字
            int x = (n / p) % 10;    // 当前位的数字

            if (x == 0) res += left * p;
            else if (x == 1) res += left * p + right + 1;
            else res += (left + 1) * p;

            p *= 10; // 更新权重
        }

        return res;
    }
};
```

- 时间：O($$log_{10}n$$)
- 空间：1
