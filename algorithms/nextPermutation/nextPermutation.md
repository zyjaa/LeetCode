**31题意**：下一个排列

`[1,2,3]`、`[1,3,2]`、`[3,1,2]`、`[2,3,1]` 。

必须[ 原地 ](https://baike.baidu.com/item/原地算法)修改，只允许使用额外常数空间。

**示例 1：**

```
输入：nums = [1,2,3]
输出：[1,3,2]
```

**示例 2：**

```
输入：nums = [3,2,1]
输出：[1,2,3]
```

**示例 3：**

```
输入：nums = [1,1,5]
输出：[1,5,1]
```



### 法一：模拟

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& a) {
        int k = a.size() - 1;
        // 寻找转折点
        while (k > 0 && a[k] <= a[k - 1]) k--;
        if (k <= 0) {
            // 如果找不到转折点，说明数组是降序排列，直接反转
            reverse(a.begin(), a.end());
        } else {
            int t = k;
            // 寻找第一个大于 a[k-1] 的元素
            while (t < a.size() && a[t] > a[k - 1]) t++;
            // 交换 a[k-1] 和 a[t-1]
            swap(a[t - 1], a[k - 1]);
            // 反转 k 到末尾的部分
            reverse(a.begin() + k, a.end());
        }
    }
};
```

- 时间：O($$n$$)
- 空间：O($$1$$)