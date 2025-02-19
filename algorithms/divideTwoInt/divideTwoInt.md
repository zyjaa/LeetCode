**29、两数相除**

给你两个整数，被除数 `dividend` 和除数 `divisor`。将两数相除，要求 **不使用** 乘法、除法和取余运算。

整数除法应该向零截断，也就是截去（`truncate`）其小数部分。例如，`8.345` 将被截断为 `8` ，`-2.7335` 将被截断至 `-2` 。

返回被除数 `dividend` 除以除数 `divisor` 得到的 **商** 。

**注意：**假设我们的环境只能存储 **32 位** 有符号整数，其数值范围是 `[−2^31, 2^31 − 1]` 。本题中，如果商 **严格大于** `2^31− 1` ，则返回 `2^31− 1` ；如果商 **严格小于** `-2^31` ，则返回 `-2^31` 。

 

**示例 1:**

```
输入: dividend = 10, divisor = 3
输出: 3
解释: 10/3 = 3.33333.. ，向零截断后得到 3 。
```

**示例 2:**

```
输入: dividend = 7, divisor = -3
输出: -2
解释: 7/-3 = -2.33333.. ，向零截断后得到 -2 。
```



### 法一：倍增

任何整数可以表示为 **2 的幂次方的和**，不做解释，自行搜索

```cpp
class Solution {
public:
    int divide(int x, int y) {
        typedef long long ll;
        bool minus=false;
        if(x>0 && y<0 || x<0 && y>0) minus=true;
        ll a=abs((ll)x),b=abs((ll)y);
        vector<ll> exp;// 记录b的2^i倍数
        for(ll i=b;i<=a;i+=i)exp.push_back(i);
        ll res=0;
        for(int i=exp.size()-1;i>=0;i--)
            if(a>=exp[i]){// b*2^i存在
                a-=exp[i];
                res+=1ll<<i;
            }
        if(minus)res=-res;        
        if(res>INT_MAX)res=INT_MAX;
        if(res<INT_MIN)res=INT_MIN;
        return res;
    }
};
```

- 时间：O($$log(a/b)$$)
- 空间：O($$log(a/b)$$)，exp数组