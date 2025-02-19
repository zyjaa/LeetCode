[69. x 的平方根 ](https://leetcode.cn/problems/sqrtx/)

**示例 1：**

```
输入：x = 4
输出：2
```

**示例 2：**

```
输入：x = 8
输出：2
解释：8 的算术平方根是 2.82842..., 由于返回类型是整数，小数部分将被舍去。
```



### 1、二分

```cpp
class Solution {
public:
    int mySqrt(int x) {
        int l=1,r=x;
        while(l<r){
            long long m=1ll+l+r>>1;
            if(m*m<=x)l=m;
            else r=m-1;
        }
        return r;
    }
};
```

- 时间：O($$logx$$)
- 空间：1





### 2、袖珍计算器算法

$$x^{1/2}$$= $$e^{(1/2)lnx}$$

ans+1，ans有一个是答案

```cpp
class Solution {
public:
    int mySqrt(int x) {
        if (x == 0) {
            return 0;
        }
        int ans = exp(0.5 * log(x));
        return ((long long)(ans + 1) * (ans + 1) <= x ? ans + 1 : ans);
    }
};

```

- 时间：1
- 空间：1



### 3、牛顿迭代

