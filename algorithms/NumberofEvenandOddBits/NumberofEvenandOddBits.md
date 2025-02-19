[2595. 奇偶位数](https://leetcode.cn/problems/number-of-even-and-odd-bits/)

给你一个 **正** 整数 `n` 。

用 `even` 表示在 `n` 的二进制形式（下标从 **0** 开始）中值为 `1` 的偶数下标的个数。

用 `odd` 表示在 `n` 的二进制形式（下标从 **0** 开始）中值为 `1` 的奇数下标的个数。

返回整数数组 `answer` ，其中 `answer = [even, odd]` 。

 

**示例 1：**

```
输入：n = 17
输出：[2,0]
解释：17 的二进制形式是 10001 。 
下标 0 和 下标 4 对应的值为 1 。 
共有 2 个偶数下标，0 个奇数下标。
```

**示例 2：**

```
输入：n = 2
输出：[0,1]
解释：2 的二进制形式是 10 。 
下标 1 对应的值为 1 。 
共有 0 个偶数下标，1 个奇数下标。
```





### 法一：二进制

```cpp
class Solution {
public:
	vector<int> evenOddBit(int n) {
		int odd = 0, even = 0;
		int bit = 0;
        // 找到第一个为1的位置（开始枚举位的位置）
		for (int i = 31; i >= 0; i--) {
			if (n >> i & 1) {
				bit = i;
				break;
			}
		}

		for (int i = bit; i >= 0; i --) {
			if (n >> i & 1) {
				if (i % 2)
					odd++;
				else
					even++;
			}
		}

		vector<int> ans;
		ans.push_back(even);
		ans.push_back(odd);
		return ans;
	}
};
```

- 时间：O($$1$$)
- 空间：O($$1$$)



**位运算优化**

```cpp
int bit = __builtin_ctz(n);// 直接找到最低位1的位置
for (int i = bit; i < 32; i++) {
    if (n >> i & 1) {
        if (i % 2) odd++;
        else even++;
    }
}
```





**位掩码**

```cpp
class Solution {
public:
    vector<int> evenOddBit(int n) {
        const unsigned MASK = 0x55555555;
        return {popcount(n & MASK), popcount(n & (MASK >> 1))};
    }
};
```

- `MASK = 0x55555555`：
  二进制表示为 `01010101...0101`，用于提取偶数位（最低位为第0位）。
- `MASK >> 1`：
  二进制表示为 `00101010...1010`，用于提取奇数位。
- `popcount`：计算二进制数中1的个数