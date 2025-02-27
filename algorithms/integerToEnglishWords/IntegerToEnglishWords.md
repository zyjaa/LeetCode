```
#include <string>
#include <map>
#include <sstream>

using namespace std;

// 定义常量
const int billion = 1000000000;  // 十亿
const int million = 1000000;     // 百万
const int thousand = 1000;       // 千
const int hundred = 100;          // 百

class Solution {
public:
    string numberToWords(int num) {
        // 特殊情况：如果 num 为 0，直接返回 "Zero"
        if (num == 0) {
            return "Zero";
        }

        // 定义数字到英文单词的映射，按数字从大到小排序
        static const map<int, string, greater<int>> m {
            {1, "One"}, {2, "Two"}, {3, "Three"}, {4, "Four"}, {5, "Five"},
            {6, "Six"}, {7, "Seven"}, {8, "Eight"}, {9, "Nine"}, {10, "Ten"},
            {11, "Eleven"}, {12, "Twelve"}, {13, "Thirteen"}, {14, "Fourteen"},
            {15, "Fifteen"}, {16, "Sixteen"}, {17, "Seventeen"}, {18, "Eighteen"},
            {19, "Nineteen"}, {20, "Twenty"}, {30, "Thirty"}, {40, "Forty"},
            {50, "Fifty"}, {60, "Sixty"}, {70, "Seventy"}, {80, "Eighty"},
            {90, "Ninety"}
        };

        // 使用 ostringstream 构建结果字符串
        ostringstream oss;

        // 处理十亿位
        if (num >= billion) {
            oss << numberToWords(num / billion) << " Billion";  // 递归处理十亿位
            num %= billion;  // 取余数
            if (num > 0) oss << ' ';  // 如果余数大于 0，添加空格
        }

        // 处理百万位
        if (num >= million) {
            oss << numberToWords(num / million) << " Million";  // 递归处理百万位
            num %= million;  // 取余数
            if (num > 0) oss << ' ';  // 如果余数大于 0，添加空格
        }

        // 处理千位
        if (num >= thousand) {
            oss << numberToWords(num / thousand) << " Thousand";  // 递归处理千位
            num %= thousand;  // 取余数
            if (num > 0) oss << ' ';  // 如果余数大于 0，添加空格
        }

        // 处理百位
        if (num >= hundred) {
            oss << numberToWords(num / hundred) << " Hundred";  // 递归处理百位
            num %= hundred;  // 取余数
            if (num > 0) oss << ' ';  // 如果余数大于 0，添加空格
        }

        // 处理小于 100 的数字
        for (const auto& [k, v] : m) {
            if (num >= k) {
                oss << v;  // 添加对应的英文单词
                num -= k;  // 减去已处理的部分
                if (num > 0) oss << ' ';  // 如果剩余部分大于 0，添加空格
            }
        }

        // 返回结果字符串
        return oss.str();
    }
};
```

