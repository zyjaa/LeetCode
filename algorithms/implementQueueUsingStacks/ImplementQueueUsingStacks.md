```cpp
class MyQueue {
public:
    stack<int> a, b; // 两个栈 a 和 b
    MyQueue() {
        // 构造函数，初始化队列
    }
    
    void push(int x) {
        a.push(x); // 将元素 x 压入栈 a
    }
    
    int pop() {
        while(a.size() > 1) {
            b.push(a.top()); // 将栈 a 的顶部元素压入栈 b
            a.pop(); // 弹出栈 a 的顶部元素
        }
        int t = a.top(); // 获取栈 a 的最后一个元素
        a.pop(); // 弹出栈 a 的最后一个元素
        while(b.size()) {
            a.push(b.top()); // 将栈 b 的元素重新压回栈 a
            b.pop(); // 弹出栈 b 的顶部元素
        }
        return t; // 返回弹出的元素
    }
    
    int peek() {
        while(a.size() > 1) {
            b.push(a.top()); // 将栈 a 的顶部元素压入栈 b
            a.pop(); // 弹出栈 a 的顶部元素
        }
        int t = a.top(); // 获取栈 a 的最后一个元素
        while(b.size()) {
            a.push(b.top()); // 将栈 b 的元素重新压回栈 a
            b.pop(); // 弹出栈 b 的顶部元素
        }
        return t; // 返回栈 a 的最后一个元素
    }
    
    bool empty() {
        return a.empty(); // 判断栈 a 是否为空
    }
};
```

 
