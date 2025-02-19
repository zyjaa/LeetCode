[50. Pow(x, n)](https://leetcode.cn/problems/powx-n/)

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 `x` 的整数 `n` 次幂函数（即，`xn` ）。

**示例 1：**

```
输入：x = 2.00000, n = 10
输出：1024.00000
```



### 法一：快速幂

```cpp
class Solution {
public:
    double qmi(double x,long long n){
        if(n<0)return 1/myPow(x,-n);
        if(n==0)return 1;
        double res=1;
        while(n){
            if(n&1)res*=x;
            x*=x;
            n>>=1;
        }
        return res;
    }
    double myPow(double x, long long n) {
        return qmi(x,n);
    }
};
```

- 时间：O($$logn$$)
- 空间：O($$1$$)

