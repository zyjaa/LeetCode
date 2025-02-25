```
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> S;
        for(auto x:nums){
            if(S.count(x))return true;
            S.insert(x);
        }
        return false;
    }
};
```

 
