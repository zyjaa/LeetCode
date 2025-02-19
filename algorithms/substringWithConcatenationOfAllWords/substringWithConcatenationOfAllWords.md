**30、串联所有单词的子串**：s中出现的都要包含，求这个范围（最早的下标和最晚的下标）

 

**示例 1：**

```
输入：s = "barfoothefoobarman", words = ["foo","bar"]
输出：[0,9]
解释：因为 words.length == 2 同时 words[i].length == 3，连接的子字符串的长度必须为 6。
子串 "barfoo" 开始位置是 0。它是 words 中以 ["bar","foo"] 顺序排列的连接。
子串 "foobar" 开始位置是 9。它是 words 中以 ["foo","bar"] 顺序排列的连接。
输出顺序无关紧要。返回 [9,0] 也是可以的。
```

**示例 2：**

```
输入：s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
输出：[]
解释：因为 words.length == 4 并且 words[i].length == 4，所以串联子串的长度必须为 16。
s 中没有子串长度为 16 并且等于 words 的任何顺序排列的连接。
所以我们返回一个空数组。
```

**示例 3：**

```
输入：s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
输出：[6,9,12]
解释：因为 words.length == 3 并且 words[i].length == 3，所以串联子串的长度必须为 9。
子串 "foobarthe" 开始位置是 6。它是 words 中以 ["foo","bar","the"] 顺序排列的连接。
子串 "barthefoo" 开始位置是 9。它是 words 中以 ["bar","the","foo"] 顺序排列的连接。
子串 "thefoobar" 开始位置是 12。它是 words 中以 ["the","foo","bar"] 顺序排列的连接。
```



### 法一：滑动窗口+哈希表

```cpp
class Solution {
public:
    vector<int> findSubstring(string s, vector<string>& words) {
        int n=s.size(),m=words.size(),k=words[0].size();
        vector<int> res;
        unordered_map<string,int> a;
        for(auto x:words)a[x]++;
        for(int i=0;i<k;i++){
            unordered_map<string,int> map;
            int cnt=0;
            for(int j=i;j+k-1<n;j+=k){
                auto word=s.substr(j,k);
                if(j-i+1>m*k){
                    auto front=s.substr(j-m*k,k);
                    map[front]--;
                    if(map[front]<a[front])cnt--;
                }
                map[word]++;
                if(map[word]<=a[word])cnt++;
                if(cnt==m)res.push_back(j-(m-1)*k);
            }
        }
        return res;
    }
};
```

- 时间：O($$n$$)
  - 外层循环：`O(k)`。
  - 内层循环：`O(n / k)`。
  - 每次循环的操作是常数时间。
- 空间：O($$m+n$$)