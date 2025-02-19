[43. 字符串相乘](https://leetcode.cn/problems/multiply-strings)



**示例 1:**

```
输入: num1 = "2", num2 = "3"
输出: "6"
```

**示例 2:**

```
输入: num1 = "123", num2 = "456"
输出: "56088"
```





### 法一：模拟

```cpp
class Solution {
public:
    string multiply(string num1, string num2) {
        vector<int>A,B;
        int n=num1.size(),m=num2.size();
        for(int i=n-1;i>=0;i--)A.push_back(num1[i]-'0');
        for(int i=m-1;i>=0;i--)B.push_back(num2[i]-'0');
        vector<int> C(n+m);
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                C[i+j]+=A[i]*B[j];
            }
        }

        for(int i=0,t=0;i<C.size();i++){
            t+=C[i];
            C[i]=t%10;
            t/=10;
        }
         // 去除前导零并生成结果
        int k = C.size() - 1;
        while (k && !C[k]) k--; // 去除前导零
        string res;
        while (k >= 0) res += C[k--] + '0'; // 转为字符串
        return res;
    }
};
```

- 时间：O(n*m)
- 空间：O(n+m)