### 1、归并排序

```
class Solution {
public:
    vector<int> countSmaller(vector<int>& nums) {
        vector<int> counts(nums.size(), 0); // 结果数组
        vector<pair<int, int>> indexedNums; // 存储元素及其原始索引
        for (int i = 0; i < nums.size(); i++) {
            indexedNums.push_back({nums[i], i});
        }
        mergeSort(indexedNums, 0, nums.size() - 1, counts);
        return counts;
    }

private:
    void mergeSort(vector<pair<int, int>>& indexedNums, int left, int right, vector<int>& counts) {
        if (left >= right) return;

        int mid = left + (right - left) / 2;
        mergeSort(indexedNums, left, mid, counts); // 递归排序左半部分
        mergeSort(indexedNums, mid + 1, right, counts); // 递归排序右半部分
        merge(indexedNums, left, mid, right, counts); // 合并左右两部分
    }

    void merge(vector<pair<int, int>>& indexedNums, int left, int mid, int right, vector<int>& counts) {
        vector<pair<int, int>> temp(right - left + 1); // 临时数组
        int i = left, j = mid + 1, k = 0; // 左右部分的指针

        // 统计右侧比当前元素小的个数
        while (i <= mid && j <= right) {
            if (indexedNums[i].first <= indexedNums[j].first) {
                counts[indexedNums[i].second] += j - (mid + 1); // 统计右侧较小元素个数
                temp[k++] = indexedNums[i++];
            } else {
                temp[k++] = indexedNums[j++];
            }
        }

        // 处理剩余元素
        while (i <= mid) {
            counts[indexedNums[i].second] += j - (mid + 1); // 统计右侧较小元素个数
            temp[k++] = indexedNums[i++];
        }
        while (j <= right) {
            temp[k++] = indexedNums[j++];
        }

        // 将临时数组复制回原数组
        for (int p = 0; p < temp.size(); p++) {
            indexedNums[left + p] = temp[p];
        }
    }
};
```

