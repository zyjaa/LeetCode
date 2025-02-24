```cpp 
class Solution {
public:
    string fractionToDecimal(int numerator, int denominator) {
        using ll = long long; // 使用 long long 防止溢出
        ll x = numerator, y = denominator;

        // 如果能够整除，直接返回结果
        if (x % y == 0) return to_string(x / y);

        string res; // 存储结果
        // 处理符号
        if ((x < 0) ^ (y < 0)) res += '-';
        x = abs(x), y = abs(y); // 取绝对值

        // 处理整数部分
        res += to_string(x / y) + '.';
        x %= y; // 取余数，用于计算小数部分

        // 哈希表记录余数对应的位置，用于检测循环
        unordered_map<ll, ll> hash;
        while (x) {
            // 如果余数已经出现过，说明进入循环
            if (hash.count(x)) {
                res = res.substr(0, hash[x]) + '(' + res.substr(hash[x]) + ')';
                break;
            }
            hash[x] = res.size(); // 记录当前余数的位置
            x *= 10; // 余数乘以 10，继续计算小数部分
            res += to_string(x / y); // 将商添加到结果中
            x %= y; // 更新余数
        }
        return res;
    }
};
```

- 时间：由于余数最多有 `denominator` 种可能的值，因此最多需要计算 `denominator` 次才能检测到循环。
  - 如果小数部分没有循环，时间复杂度为 **O(k)**，其中 `k` 是小数部分的长度。
  - 如果小数部分有循环，时间复杂度为 **O(k + c)**，其中 `k` 是非循环部分的长度，`c` 是循环部分的长度。
- 空间：哈希表 `hash` 最多存储 `denominator` 个键值对，因此空间复杂度为 **O(denominator)**。
