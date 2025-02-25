### 1、线性筛法

```cpp
class Solution {
public:
    int countPrimes(int n) {
        vector<int> primes; // 用来存储质数
        vector<int> st(n + 1); // 用来标记合数
        for (int i = 2; i < n; i++) { // 从2开始遍历
            if (!st[i]) primes.push_back(i); // 如果i没有被标记为合数，说明i是质数
            for (int j = 0; i * primes[j] < n; j++) { // 用i和已有的质数标记合数
                st[i * primes[j]] = true; // 标记i * primes[j]为合数
                if (i % primes[j] == 0) break; // 如果i能被primes[j]整除，退出内层循环
            }
        }
        return primes.size(); // 返回质数的个数
    }
};
```

 n,n
