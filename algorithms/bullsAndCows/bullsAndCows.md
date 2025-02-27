```
#include <string>
#include <unordered_map>

using namespace std;

class Solution {
public:
    string getHint(string secret, string guess) {
        unordered_map<char, int> hash;  // 用于统计 secret 中每个数字的频率
        int bulls = 0, cows = 0;        // Bulls 和 Cows 的数量

        // 统计 Bulls 并记录 secret 中每个数字的频率
        for (int i = 0; i < secret.size(); i++) {
            if (secret[i] == guess[i]) {
                bulls++;  // 数字和位置都正确，Bulls 加 1
            } else {
                hash[secret[i]]++;  // 记录 secret 中数字的频率
            }
        }

        // 统计 Cows
        for (int i = 0; i < guess.size(); i++) {
            if (secret[i] != guess[i] && hash[guess[i]] > 0) {
                cows++;           // 数字正确但位置不对，Cows 加 1
                hash[guess[i]]--; // 减少对应数字的频率
            }
        }

        // 返回提示字符串
        return to_string(bulls) + "A" + to_string(cows) + "B";
    }
};
```

