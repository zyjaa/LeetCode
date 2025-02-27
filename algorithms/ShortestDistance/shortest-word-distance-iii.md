```
int shortestWordDistance(vector<string>& words, string word1, string word2) {
    int index1 = -1, index2 = -1; // 初始化下标为 -1
    int minDistance = INT_MAX;   // 初始化最小距离为最大值

    for (int i = 0; i < words.size(); i++) {
        if (words[i] == word1) {
            if (word1 == word2) {
                // 如果 word1 和 word2 相同，更新 index2 为 index1，index1 为当前下标
                index2 = index1;
                index1 = i;
            } else {
                // 如果 word1 和 word2 不同，更新 index1
                index1 = i;
            }
        } else if (words[i] == word2) {
            // 如果 word1 和 word2 不同，更新 index2
            index2 = i;
        }

        // 如果两个下标都有效，计算距离
        if (index1 != -1 && index2 != -1) {
            minDistance = min(minDistance, abs(index1 - index2));
        }
    }

    return minDistance;
}
```

 
