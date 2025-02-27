### 1、哈希表

```
class Solution {
public:
    bool isAnagram(string s, string t) {
        unordered_map<char,int> st,ts;
        for(auto x:s)st[x]++;
        for(auto x:t)ts[x]++;
        return st==ts;
    }
};
```

