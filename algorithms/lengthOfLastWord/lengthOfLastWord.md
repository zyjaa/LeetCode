[58. 最后一个单词的长度](https://leetcode.cn/problems/length-of-last-word/)

**示例 1：**

```
输入：s = "Hello World"
输出：5
解释：最后一个单词是“World”，长度为 5。
```



### 1、模拟

```cpp
class Solution {
public:
    int lengthOfLastWord(string s) {
        int k=s.size()-1;
        while(s[k]==' ')k--;
        for(int i=k;i>=0;i--){
            int j=i-1;
            while(j>=0 && s[j]!=' ')j--;
            return i-j;
        }
        return 0;
    }
};
```

- 时间复杂度：O($$n$$)，其中*n*是*s*的长度。
- 空间复杂度：O($$1$$)。