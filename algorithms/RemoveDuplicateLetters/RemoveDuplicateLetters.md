### 1、DFS

```
#include <vector>
#include <string>
using namespace std;

class Solution {
public:
    vector<string> generateAbbreviations(string word) {
        vector<string> result; // 存储所有缩写的结果列表
        backtrack(word, 0, "", 0, result); // 调用递归回溯函数
        return result;
    }

private:
    void backtrack(const string& word, int index, string path, int count, vector<string>& result) {
        // index: 当前处理的字符位置
        // path: 当前生成的缩写部分
        // count: 当前未处理的数字长度（即连续被替换的字母数量）
        // result: 存储所有缩写的结果列表

        // 如果已经处理完所有字符
        if (index == word.length()) {
            // 如果还有未处理的数字，将其添加到 path 中
            if (count > 0) {
                path += to_string(count);
            }
            // 将当前生成的缩写添加到结果列表中
            result.push_back(path);
            return;
        }

        // 选择 1：用数字替换当前字符
        // 不将当前字符加入 path，而是增加 count
        backtrack(word, index + 1, path, count + 1, result);

        // 选择 2：保留当前字符
        if (count > 0) {
            // 如果 count > 0，表示之前有未处理的数字，将其加入 path
            // 然后将当前字符加入 path，并将 count 重置为 0
            backtrack(word, index + 1, path + to_string(count) + word[index], 0, result);
        } else {
            // 如果 count == 0，直接将当前字符加入 path
            backtrack(word, index + 1, path + word[index], 0, result);
        }
    }
};
```

1. **时间复杂度**：O(2^n)，其中 n*n* 是单词的长度。每个字符有两种选择（保留或用数字替换）。
2. **空间复杂度**：O(n)，递归栈的深度为 n*n*。
