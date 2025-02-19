[67. 二进制求和](https://leetcode.cn/problems/add-binary/)

给你两个二进制字符串 `a` 和 `b` ，以二进制字符串的形式返回它们的和。

 

**示例 1：**

```
输入:a = "11", b = "1"
输出："100"
```



### 1、模拟

```cpp
class Solution {
public:
    string addBinary(string a, string b) {
        string c;
        reverse(a.begin(),a.end());
        reverse(b.begin(),b.end());
        int t=0;
        for(int i=0;i<a.size() || i<b.size() || t;i++){
            if(i<a.size())t+=a[i]-'0';
            if(i<b.size())t+=b[i]-'0';
            c+=to_string(t%2);
            t/=2;
        }
        reverse(c.begin(),c.end());
        return c;
    }
};
```

- 时间：max(m,n)
- 空间：max(m,n)