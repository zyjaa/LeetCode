### 1、哈希表

```cpp
class Solution {
public:
    vector<string> findRepeatedDnaSequences(string s) {
        vector<string> res;
        unordered_map<string,int> hash;
        for(int i=0;i+9<s.size();i++)
            hash[s.substr(i,10)]++;
        for(auto [k,v]:hash)
            if(v>1)res.push_back(k);
        return res;
    }
};
```

