```cpp 
class Solution {
public:
    string convertToTitle(int n) {
        string res;
        while(n){
            n--;
            res+=n%26+'A';
            n/=26;
        }
        reverse(res.begin(),res.end());
        return res;
    }
};
```

