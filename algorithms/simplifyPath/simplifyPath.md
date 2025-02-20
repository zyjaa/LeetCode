[71. 简化路径](https://leetcode.cn/problems/simplify-path)



### 1、模拟

```cpp
class Solution {
public:
    string simplifyPath(string path) {
        string res;
        if(path.back()!='/')path+='/';
        string name;
        for(auto x:path){
            if(x!='/')name+=x;
            else{
                if(name==".."){
                    //  a/b/../
                    while(res.size() && res.back()!='/')res.pop_back();
                    if(res.size())res.pop_back();
                }else if(name!="." && name!=""){
                    //  a/b//././
                    // a/b/c/
                    res=res+"/"+name;
                }
                name.clear();
            }
        }
        if(res.empty())res="/";
        return res;
    }
};
```

- 时间：O(n)，path长度
- 空间：O(n)，res