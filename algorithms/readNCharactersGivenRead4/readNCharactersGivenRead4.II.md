 题目：给定一个 `read4` API，每次调用可以从文件中读取最多 4 个字符。设计一个算法，通过多次调用 `read4`，实现一个 `read` 函数，该函数可以读取文件中最多 `n` 个字符。

```cpp
class Solution {
private:
    char buf4; // 内部缓冲区
    int buf4Ptr = 0; // 缓冲区指针
    int buf4Count = 0; // 缓冲区中剩余的字符数

public:
    int read(char *buf, int n) {
        int total = 0; // 实际读取的字符数
        while (total < n) {
            // 如果缓冲区中没有字符，则调用 read4 读取新的字符
            if (buf4Ptr == 0) {
                buf4Count = read4(buf4);
            }
            // 如果 read4 返回 0，说明文件结束
            if (buf4Count == 0) break;
            // 将缓冲区中的字符复制到 buf 中
            while (total < n && buf4Ptr < buf4Count) {
                buf[total++] = buf4[buf4Ptr++];
            }
            // 如果缓冲区中的字符已经全部读取完毕，则重置指针
            if (buf4Ptr == buf4Count) buf4Ptr = 0;
        }
        return total; // 返回实际读取的字符数
    }
};
```

