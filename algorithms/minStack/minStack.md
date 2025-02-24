 

### 1、栈

也很单一，2个栈进出顺序

```cpp
class MinStack {
public:
    stack<int> stk; // 主栈，存储所有元素
    stack<int> f;   // 辅助栈，存储当前最小值

    MinStack() {
        // 构造函数，初始化栈
    }

    void push(int val) {
        stk.push(val); // 将元素压入主栈
        // 如果辅助栈为空，或者当前值小于等于辅助栈的栈顶元素，则压入辅助栈
        if (f.empty() || val <= f.top()) f.push(val);
    }

    void pop() {
        // 如果主栈的栈顶元素等于辅助栈的栈顶元素，则弹出辅助栈的栈顶元素
        if (stk.top() == f.top()) f.pop();
        stk.pop(); // 弹出主栈的栈顶元素
    }

    int top() {
        // 返回主栈的栈顶元素
        return stk.top();
    }

    int getMin() {
        // 返回辅助栈的栈顶元素，即当前最小值
        return f.top();
    }
};
```

