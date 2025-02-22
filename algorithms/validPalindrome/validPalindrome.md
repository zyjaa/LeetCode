[125. 验证回文串](https://leetcode.cn/problems/valid-palindrome/) 



### 1、模拟

全部变小写，串一遍，i从前面，j从后面，两边扫一遍

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        for(int i=0,j=s.size()-1;i<j;i++,j--){
            while(i<j && !isalnum(tolower(s[i])))i++;
            while(i<j && !isalnum(tolower(s[j])))j--;
            if(i<j && tolower(s[i])!=tolower(s[j]))return false;
        }
        return true;
    }
};
```

- 时间：n
- 空间：1

