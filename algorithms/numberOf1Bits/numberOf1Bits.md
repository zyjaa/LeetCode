```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int res=0;
        for(;n;n-=n&-n)res++;
        return res;
    }
};
```

 
