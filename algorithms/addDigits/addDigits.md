```
class Solution {
public:
    int addDigits(int num) {
        if(!num)return 0;
        if(num%9)return num%9;
        return 9;
    }
};
```

### **数学原理**

数字根的计算可以通过以下数学公式实现：

- 如果 `num == 0`，数字根为 `0`。
- 如果 `num != 0`，数字根为 `9` 的余数，即 `num % 9`。如果 `num % 9 == 0`，则数字根为 `9`。

**推导**：

- 一个整数 `num` 可以表示为 `num = 9 * k + r`，其中 `k` 是整数，`r` 是余数（`0 <= r < 9`）。
- 数字根的计算过程等价于对 `9` 取余，但需要注意 `num % 9 == 0` 时数字根为 `9`。
