 

```cpp
class Solution {
public:
    string reverseWords(string s) {
        int k = 0; // 记录新字符串的写入位置
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == ' ') continue; // 跳过空格

            // 提取一个单词
            int a = i, b = k;
            while (a < s.size() && s[a] != ' ') s[b++] = s[a++];

            // 反转单词
            reverse(s.begin() + k, s.begin() + b);

            // 添加一个空格
            s[b++] = ' ';

            // 更新索引
            i = a;
            k = b;
        }

        // 去除最后一个多余的空格
        if (k) k--;

        // 删除剩余字符
        s.erase(s.begin() + k, s.end());

        // 反转整个字符串
        reverse(s.begin(), s.end());

        return s;
    }
};
```

n,1
