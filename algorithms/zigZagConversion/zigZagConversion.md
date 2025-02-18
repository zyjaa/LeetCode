**题意**：看例子，按z字形，排到numRows就变换，然后变换后每行输出

**例 1：**

```
输入：s = "PAYPALISHIRING", numRows = 3
输出："PAHNAPLSIIGYIR"
```

```
P   A   H   N
A P L S I I G
Y   I   R
```





### 法一：模拟

- i为0，P与A距离为2*numRows-2（0+2\*3-2=4）（f(x)=f(x+T)=f(x+(2\*n-2))
- i为最后一行：和0一样
- 中间的：A(1)和P(3)：你看ALIG和i也是T为2*n-2，PSI也是2\*n-2,，所以交替加上，j从i开始，k(P)从2\*n-2-i开始，每次加T（2\*n-2-i，为什么-i，因为第一列每次+1，那P对应的下标也应该-1）

```cpp
class Solution {
public:
    string convert(string s, int n) {
        string res;
        if(n==1)return s;
        for(int i=0;i<n;i++){
            if(!i || i==n-1){
                for(int j=i;j<s.size();j+=2*n-2)res+=s[j];
            }else{
                for(int j=i,k=2*n-2-i;j<s.size() || k<s.size();j+=2*n-2,k+=2*n-2){
                    if(j<s.size())res+=s[j];
                    if(k<s.size())res+=s[k];
                }
            }
        }
        return res;
    }
};
```

- 时间复杂度：O(N)，s遍历一遍
- 空间复杂度：O(1)