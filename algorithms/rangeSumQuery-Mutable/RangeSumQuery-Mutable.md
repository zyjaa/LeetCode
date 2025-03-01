### 1、树状数组

```
class BinaryIndexedTree {
public:
    BinaryIndexedTree(vector<int>& nums) {
        n = nums.size();
        c = vector<int>(n + 1, 0);
        for (int i = 1; i <= n; i++) {
            add(i, nums[i - 1]);
        }
    }

    // 在位置 index 增加 delta
    void add(int index, int delta) {
        for (; index <= n; index += index & -index) c[index] += delta;
    }

    // 计算前缀和，即前 index 个元素的和
    int prefixSum(int index) {
        int ans = 0;
        for (; index > 0; index -= index & -index) ans += c[index];
        return ans;
    }

private:
    int n;
    vector<int> c; // 树状数组
};

class NumArray {
public:
    NumArray(vector<int>& nums) : tree(BinaryIndexedTree(nums)) {
        this->nums = nums; // 存储原始数组
    }

    // 更新数组中指定位置的值
    void update(int index, int val) {
        int delta = val - nums[index];
        nums[index] = val; // 更新原始数组
        tree.add(index + 1, delta); // 更新树状数组
    }

    // 计算数组中指定区间的和
    int sumRange(int left, int right) {
        return tree.prefixSum(right + 1) - tree.prefixSum(left);
    }

private:
    BinaryIndexedTree tree;
    vector<int> nums; // 原始数组
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray* obj = new NumArray(nums);
 * obj->update(index,val);
 * int param_2 = obj->sumRange(left,right);
 */
```

