### 1、哈希表+双指针

```
class WordDistance {
private:
    unordered_map<string, vector<int>> wordToIndices; // 记录每个单词的下标列表

public:
    // 构造函数，初始化哈希表
    WordDistance(vector<string>& words) {
        for (int i = 0; i < words.size(); i++) {
            wordToIndices[words[i]].push_back(i);
        }
    }

    // 查询 word1 和 word2 的最短距离
    int shortest(string word1, string word2) {
        vector<int>& indices1 = wordToIndices[word1]; // 获取 word1 的下标列表
        vector<int>& indices2 = wordToIndices[word2]; // 获取 word2 的下标列表

        int minDistance = INT_MAX;
        int i = 0, j = 0;

        // 双指针法遍历两个列表
        while (i < indices1.size() && j < indices2.size()) {
            minDistance = min(minDistance, abs(indices1[i] - indices2[j]));
            if (indices1[i] < indices2[j]) {
                i++; // 移动较小的指针
            } else {
                j++;
            }
        }

        return minDistance;
    }
};
```

###  
