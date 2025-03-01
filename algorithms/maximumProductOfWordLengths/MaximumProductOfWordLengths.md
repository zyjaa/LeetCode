### 1、模拟

```cpp
class Solution {
public:
    int maxProduct(vector<string>& words) {
        int n=words.size();
        vector<int> state;
        for(auto word:words){
            int s=0;
            for(auto x:word)
                s|=1<<(x-'a');
            state.push_back(s);//用位运算表示
        }

		int res = 0;
        for (int i = 0; i < words.size(); i ++ )
            for (int j = i + 1; j < words.size(); j ++ )
                if ((state[i] & state[j]) == 0)//位数中没有相等的
                    res = max(res, (int)(words[i].size() * words[j].size()));
        return res;
    }
};
```

