```
class Solution {
public:
    string removeDuplicateLetters(string s) {
        string stk; // 用于存储结果的栈
        unordered_map<char, bool> ins; // 记录字符是否已经在栈中
        unordered_map<char, int> last; // 记录每个字符最后一次出现的位置

        // 遍历字符串，记录每个字符最后一次出现的位置
        for (int i = 0; i < s.size(); i++) {
            last[s[i]] = i;
        }

        // 遍历字符串，构建结果
        for (int i = 0; i < s.size(); i++) {
            // 如果当前字符已经在栈中，跳过
            if (ins[s[i]]) {
                continue;
            }

            // 如果栈不为空，且栈顶字符比当前字符大，且栈顶字符在后面还会出现
            // 则弹出栈顶字符，保证字典序最小
            while (stk.size() && stk.back() > s[i] && last[stk.back()] > i) {
                ins[stk.back()] = false; // 标记栈顶字符为未在栈中
                stk.pop_back(); // 弹出栈顶字符
            }

            // 将当前字符加入栈中，并标记为已存在
            stk += s[i];
            ins[s[i]] = true;
        }

        return stk; // 返回结果
    }
};
```

