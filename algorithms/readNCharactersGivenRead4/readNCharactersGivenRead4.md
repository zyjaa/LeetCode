 

题目：https://blog.csdn.net/qq_29051413/article/details/108709170

给定一个 `read4` API，每次调用可以从文件中读取最多 4 个字符。设计一个算法，通过调用 `read4`，实现一个 `read` 函数，该函数可以读取文件中任意数量的字符。

```cpp
class Solution {
public:
    int read(char *buf, int n) {
        int total = 0; // 实际读取的字符数
        char buf4;  // 临时缓冲区
        while (total < n) {
            int count = read4(buf4); // 调用 read4 读取字符
            if (count == 0) break;   // 如果 read4 返回 0，说明文件结束
            // 将 buf4 中的字符复制到 buf 中
            for (int i = 0; i < count && total < n; i++) {
                buf[total++] = buf4[i];
            }
        }
        return total; // 返回实际读取的字符数
    }
};
```

