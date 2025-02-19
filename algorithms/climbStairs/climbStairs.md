[70. 爬楼梯](https://leetcode.cn/problems/climbing-stairs/)

**示例 1：**

```
输入：n = 2
输出：2
解释：有两种方法可以爬到楼顶。
1. 1 阶 + 1 阶
2. 2 阶
```



### 1、模拟

```cpp
class Solution {
public:
    int climbStairs(int n) {
        int a=1,b=1;
        while(--n){
            int c=a+b;
            a=b;
            b=c;
        }
        return b;
    }
};
```

- 时间：n
- 空间：1