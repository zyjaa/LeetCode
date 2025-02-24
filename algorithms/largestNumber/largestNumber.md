```cpp 
class Solution {
public:
    string largestNumber(vector<int>& nums) {
        sort(nums.begin(),nums.end(),[](int x,int y){
            string a=to_string(x),b=to_string(y);
            return a+b>b+a;
        });
        string res;
        for(auto x:nums)res+=to_string(x);
        int k=0;
        while(k+1<res.size() && res[k]=='0')k++;
        return res.substr(k);
    }
};
```

