### 1、栈

```cpp
class BrowserHistory {
public:
    vector<string> history;
    int cur=0;
    BrowserHistory(string homepage) {
        history.push_back(homepage);
    }
    
    //history.resize(cur)：O(cur)，因为需要调整 history 的大小。其他都是O(1)
    void visit(string url) {
        cur++;
        //这里是为了清除没用的前进，比如home->p1->p2
        //访问 home -> page1 -> page2。
		//点击“后退”回到 page1。
		//此时“前进”记录是 page2。
		//如果在 page1 访问一个新页面 page3，那么 page2 就不再是“前进”记录，因为浏览历史已经分叉。
        history.resize(cur);
        history.push_back(url);
    }
    
    string back(int steps) {
        cur=max(cur-steps,0);
        return history[cur];
    }
    
    string forward(int steps) {
        cur=min(cur+steps,(int)history.size()-1);
        return history[cur];
    }
};

/**
 * Your BrowserHistory object will be instantiated and called as such:
 * BrowserHistory* obj = new BrowserHistory(homepage);
 * obj->visit(url);
 * string param_2 = obj->back(steps);
 * string param_3 = obj->forward(steps);
 */
```
