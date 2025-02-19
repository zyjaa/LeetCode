[68. 文本左右对齐](https://leetcode.cn/problems/text-justification/)







### 1、模拟

```cpp
class Solution {
public:
    vector<string> fullJustify(vector<string>& words, int maxWidth) {
        vector<string> res; // 存储结果
        for (int i = 0; i < words.size(); i++) {
            int j = i + 1; // 从 i + 1 开始找当前行的单词范围
            int len = words[i].size(); // 当前行的总长度（包括空格）
            while (j < words.size() && len + 1 + words[j].size() <= maxWidth) {
                len += 1 + words[j++].size(); // 更新当前行的总长度
            }

            string line; // 当前行的字符串
            if (j == i + 1 || j == words.size()) {
                // 情况1：当前行只有一个单词，或者当前行是最后一行，左对齐
                line += words[i];
                for (int k = i + 1; k < j; k++) {
                    line += ' ' + words[k];
                }
                while (line.size() < maxWidth) line += ' '; // 在末尾填充空格
            } else {
                // 情况2：均匀分配空格，使文本两端对齐
                int cnt = j - i - 1; // 当前行的空格数量
                int r = maxWidth - len + cnt; // 需要分配的总空格数量
                line += words[i]; // 先加入第一个单词
                int k = 0;
                while (k < r % cnt) { // 分配多余的空格
                    line += string(r / cnt + 1, ' ') + words[i + 1 + k];
                    k++;
                }
                while (k < cnt) { // 分配剩余的空格
                    line += string(r / cnt, ' ') + words[i + k + 1];
                    k++;
                }
            }

            res.push_back(line); // 将当前行加入结果
            i = j - 1; // 更新 i，继续处理下一行
        }
        return res;
    }
};
```

- **时间复杂度**：O(n × maxWidth)。
- **空间复杂度**：O(n × maxWidth)。