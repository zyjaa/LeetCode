### 1、模拟

每次都运算下

```

int shortestDistance(vector<string>& words, string word1, string word2) {
    int index1 = -1, index2 = -1; // 初始化下标为 -1
    int minDistance = INT_MAX;   // 初始化最小距离为最大值

    for (int i = 0; i < words.size(); i++) {
        if (words[i] == word1) {
            index1 = i; // 更新 word1 的下标
        } else if (words[i] == word2) {
            index2 = i; // 更新 word2 的下标
        }

        // 如果两个单词的下标都有效，计算距离
        if (index1 != -1 && index2 != -1) {
            minDistance = min(minDistance, abs(index1 - index2));
        }
    }

    return minDistance;
}
```

 
