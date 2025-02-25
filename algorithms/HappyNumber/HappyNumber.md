### 1、快慢指针

```cpp 
class Solution {
public:
    int f(int n){
        int res=0;
        while(n){
            res+=(n%10)*(n%10);
            n/=10;
        }
        return res;
    }
    bool isHappy(int n) {
        // 99999999=810
        int slow=n,fast=f(n);
        while(slow!=fast){
            slow=f(slow);
            fast=f(f(fast));
        }
        return fast==1;
    } 
};
```

- 时间：O($$(logn)^2$$)，假设每个数字都是9，看收敛
  - `f(n)`：O($$(logn)$$)
  - **`f(n)` 的收敛速度**：
    - 每次调用 `f(n)`，`n` 的值都会显著减小。
    - 对于一个 `k` 位的数 `n`，`f(n)` 的值会迅速降到 `81k` 以下。
    - 比如 `n = 1000`，`f(n) = 1 + 0 + 0 + 0 = 1`，直接从4位数降到1位数。（logN）

