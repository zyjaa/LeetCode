[2506. Count Pairs Of Similar Strings](https://leetcode.cn/problems/count-pairs-of-similar-strings/)

题意是是否由完全相同的字母组成，看有几对

**示例 1：**

```
输入：words = ["aba","aabb","abcd","bac","aabc"]
输出：2
解释：共有 2 对满足条件：
- i = 0 且 j = 1 ：words[0] 和 words[1] 只由字符 'a' 和 'b' 组成。 
- i = 3 且 j = 4 ：words[3] 和 words[4] 只由字符 'a'、'b' 和 'c' 。 
```



### 1、哈希表



```cpp
class Solution {
public:
    int similarPairs(vector<string>& words) {
        int ans=0;
        unordered_map<int,int> hash;
        for(auto s:words){
            int t=0;
            for(auto p:s){
                t|=1<<(p-'a');
            }
            //注意这个地方，要先加上之前的，比如现在是1之前是0个，那就组不成一对，如果之前有了1个，就组成1对，之前有2个，那当/前这个就能和之前的2个组成2对，之前有3个，当前这个就能和之前的组成3对
            ans+=hash[t];
            hash[t]++;
        }
        return ans;
    }
};
```

- 时间：n*m，n是words数量，m是单词平均长度
- 空间：n