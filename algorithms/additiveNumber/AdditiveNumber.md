```
class Solution {
public:
    // 字符串加法函数
    string add(string x, string y) {
        string result;
        int carry = 0;
        int i = x.size() - 1, j = y.size() - 1;
        while (i >= 0 || j >= 0 || carry) {
            int sum = carry;
            if (i >= 0) sum += x[i--] - '0';
            if (j >= 0) sum += y[j--] - '0';
            result.push_back('0' + (sum % 10));
            carry = sum / 10;
        }
        reverse(result.begin(), result.end());
        return result;
    }

    bool isAdditiveNumber(string num) {
        int n = num.size();
        // 枚举第一个数字的结束位置
        for (int i = 1; i <= n / 2; i++) {
            // 枚举第二个数字的结束位置
            for (int j = 1; j <= (n - i) / 2; j++) {
                // 检查是否有前导零
                if ((i > 1 && num == '0') || (j > 1 && num[i] == '0')) continue;
                string num1 = num.substr(0, i);
                string num2 = num.substr(i, j);
                int start = i + j;
                while (start < n) {
                    string sum = add(num1, num2);
                    if (num.substr(start, sum.size()) != sum) break;
                    start += sum.size();
                    num1 = num2;
                    num2 = sum;
                }
                if (start == n) return true;
            }
        }
        return false;
    }
};
```

