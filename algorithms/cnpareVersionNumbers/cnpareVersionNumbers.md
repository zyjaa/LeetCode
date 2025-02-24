- 如果 `*version1* < *version2*` 返回 `-1`，
- 如果 `*version1* > *version2*` 返回 `1`，
- 除此之外返回 `0`。

```cpp
class Solution {
public:
    int compareVersion(string v1, string v2) {
        for (int i = 0, j = 0; i < v1.size() || j < v2.size();) {
            // 找到当前段的结束位置
            int a = i, b = j;
            while (a < v1.size() && v1[a] != '.') a++;
            while (b < v2.size() && v2[b] != '.') b++;

            // 将当前段转换为整数
            int x = (a == i) ? 0 : stoi(v1.substr(i, a - i));
            int y = (b == j) ? 0 : stoi(v2.substr(j, b - j));

            // 比较当前段的大小
            if (x > y) return 1;
            else if (x < y) return -1;

            // 移动到下一段
            i = a + 1;
            j = b + 1;
        }
        return 0; // 如果所有段都相等，返回 0
    }
};
```

- 时间：max(m,n)
- 空间：1

