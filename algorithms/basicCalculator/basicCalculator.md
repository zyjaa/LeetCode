```
class Solution {
public:
    // 计算操作符栈顶的表达式
    void eval(stack<int>& num, stack<char>& op) {
        auto b = num.top(); num.pop(); // 弹出第二个操作数
        auto a = num.top(); num.pop(); // 弹出第一个操作数
        auto c = op.top(); op.pop();  // 弹出操作符
        int r;
        if (c == '+') r = a + b; // 加法
        else r = a - b;          // 减法
        num.push(r);             // 将结果压入数字栈
    }

    int calculate(string rs) {
        string s;
        // 移除字符串中的空格
        for (auto c: rs)
            if (c != ' ')
                s += c;
        
        stack<int> num; // 数字栈
        stack<char> op; // 操作符栈

        for (int i = 0; i < s.size(); i++) {
            auto c = s[i];
            if (c == ' ') continue; // 忽略空格
            if (isdigit(c)) {       // 如果是数字
                int x = 0, j = i;
                // 解析完整的数字
                while (j < s.size() && isdigit(s[j])) x = x * 10 + (s[j++] - '0');
                i = j - 1; // 更新索引
                num.push(x); // 将数字压入栈
            } else if (c == '(') { // 如果是左括号
                op.push(c);
            } else if (c == ')') { // 如果是右括号
                // 计算括号内的表达式
                while (op.top() != '(') eval(num, op);
                op.pop(); // 弹出左括号
            } else { // 如果是操作符（+ 或 -）
                // 处理可能的符号（如 -1 或 +(1)）
                if (!i || s[i - 1] == '(' || s[i - 1] == '+' || s[i - 1] == '-')
                    num.push(0);
                // 计算栈顶的操作符
                while (op.size() && op.top() != '(') eval(num, op);
                op.push(c); // 将当前操作符压入栈
            }
        }

        // 计算剩余的操作符栈中的表达式
        while (op.size()) eval(num, op);

        // 返回最终结果
        return num.top();
    }
};
```

