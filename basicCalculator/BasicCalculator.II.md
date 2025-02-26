```cpp
class Solution {
public:
    stack<int> num; // 数字栈
    stack<char> op; // 操作符栈

    // 计算操作符栈顶的表达式
    void eval() {
        int b = num.top(); num.pop(); // 弹出第二个操作数
        int a = num.top(); num.pop(); // 弹出第一个操作数
        char c = op.top(); op.pop();  // 弹出操作符
        int r;
        if (c == '+') r = a + b;      // 加法
        else if (c == '-') r = a - b; // 减法
        else if (c == '*') r = a * b; // 乘法
        else r = a / b;               // 除法
        num.push(r);                  // 将结果压入数字栈
    }

    int calculate(string s) {
        // 定义操作符的优先级
        unordered_map<char, int> pr;
        pr['+'] = pr['-'] = 1, pr['*'] = pr['/'] = 2;

        for (int i = 0; i < s.size(); i++) {
            char c = s[i];
            if (c == ' ') continue; // 忽略空格
            if (isdigit(c)) {       // 如果是数字
                int x = 0, j = i;
                // 解析完整的数字
                while (j < s.size() && isdigit(s[j])) x = x * 10 + (s[j++] - '0');
                num.push(x); // 将数字压入栈
                i = j - 1;   // 更新索引
            } else {         // 如果是操作符
                // 根据优先级计算栈顶的表达式
                while (op.size() && pr[op.top()] >= pr[c]) eval();
                op.push(c); // 将当前操作符压入栈
            }
        }

        // 计算剩余的操作符栈中的表达式
        while (op.size()) eval();

        // 返回最终结果
        return num.top();
    }
};
```

 
