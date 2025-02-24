###  1、栈

```cpp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> stk;
        for(auto& x:tokens){
            if(x=="+" || x=="-" || x=="*" || x=="/"){
                int a=stk.top();stk.pop();
                int b=stk.top();stk.pop();
                if(x=="+")b+=a;
                if(x=="-")b-=a;
                if(x=="*")b*=a;
                if(x=="/")b/=a;
                stk.push(b);
            }else stk.push(stoi(x));
        }
        return stk.top();
    }
};
```

n,n

逆波兰是后序遍历
