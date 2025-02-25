 一一对应

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        unordered_map<char,char> st,ts;
        int n=s.size();
        for(int i=0;i<n;i++){
            char a=s[i],b=t[i];
            if(st.count(a) && st[a]!=b)return false;
            st[a]=b;
            if(ts.count(b) && ts[b]!=a)return false;
            ts[b]=a;
        }
        return true;
    }
};
```

