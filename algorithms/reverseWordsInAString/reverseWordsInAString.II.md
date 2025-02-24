https://blog.csdn.net/qq_29051413/article/details/108595337

### 1、模拟

```cpp
class Solution {
public:
    void reverseWords(vector<char>& s) {
        int n = s.size();
        int left = 0; // 单词的起始位置

        // 翻转每个单词
        for (int right = 0; right <= n; right++) {
            if (right == n || s[right] == ' ') { // 遇到空格或字符串结束
                reverseWord(s, left, right - 1); // 翻转单词
                left = right + 1; // 更新下一个单词的起始位置
            }
        }

        // 翻转整个数组
        reverseWord(s, 0, n - 1);
    }

private:
    // 翻转字符数组中指定范围的字符
    void reverseWord(vector<char>& s, int left, int right) {
        while (left < right) {
            swap(s[left], s[right]);
            left++;
            right--;
        }
    }
};
```

 n，1
