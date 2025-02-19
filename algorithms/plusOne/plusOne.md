[66. 加一](https://leetcode.cn/problems/plus-one/)

**示例 1：**

```
输入：digits = [1,2,3]
输出：[1,2,4]
解释：输入数组表示数字 123。
```



### 1、模拟

```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        reverse(digits.begin(),digits.end());
        int t=1;
        for(auto& x:digits){
            t+=x;
            x=t%10;
            t/=10;
        }
        if(t)digits.push_back(1);
        reverse(digits.begin(),digits.end());
        return digits;
    }
};
```

- 时间：n
- 空间：1