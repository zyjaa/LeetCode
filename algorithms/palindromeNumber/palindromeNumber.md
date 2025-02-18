**题意**：判断一个数是否是回文数

**示例 1：**

```
输入：x = 121
输出：true
```

**示例 2：**

```
输入：x = -121
输出：false
解释：从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

- `-231 <= x <= 231 - 1`



### 法一：模拟

```cpp
class Solution {
public:
    bool isPalindrome(int x) {
        if(x<0)return false;//负数直接就滚了
        long long a=0;
        int b=x;
        while(b){
            a=a*10+b%10;
            b/=10;
        }
        return a==x;
    }
};
```

- 时间复杂度：O($$lgx$$)
- 空间复杂度：O(1)