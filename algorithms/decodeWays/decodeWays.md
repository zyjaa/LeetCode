[91. 解码方法](https://leetcode.cn/problems/decode-ways/)

"1" -> 'A'
 "2" -> 'B'

**示例 1：**

```
输入：s = "12"
输出：2
解释：它可以解码为 "AB"（1 2）或者 "L"（12）。
```



### 1、模拟

f(i)：前i位有多少类

```cpp
class Solution {
public:
    int numDecodings(string s) {
        // 前i位有多少类
        s=' '+s;
        int n=s.size();
        vector<int>f(n);
        f[0]=1;
        for(int i=1;i<n;i++){
            if(s[i]>='1' && s[i]<='9')f[i]+=f[i-1];// s[i]单独作为1个
            if(i>1){
                int t=(s[i-1]-'0')*10+(s[i]-'0');
                if(t>=10 && t<=26)f[i]+=f[i-2];//s[i-1]和s[i]组合作为一个
            }
        }
        return f[n-1];
    }
};
```

- 时间：n
- 空间：n