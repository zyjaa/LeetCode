### 1、一个队列实现栈

```
class MyStack {
public:
    queue<int> q;

    MyStack() {}
	
	//O(n)
    void push(int x) {
        int n = q.size();
        q.push(x);
        for (int i = 0; i < n; i++) {
            q.push(q.front());
            q.pop();
        }
    }

    int pop() {
        int t = q.front();
        q.pop();
        return t;
    }

    int top() {
        return q.front();
    }

    bool empty() {
        return q.empty();
    }
};
```

 n,n
