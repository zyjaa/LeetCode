```
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    vector<vector<int>> multiply(vector<vector<int>>& mat1, vector<vector<int>>& mat2) {
        // 将矩阵 mat1 转换为 CSR 格式
        auto to_csr = [](const vector<vector<int>>& matrix) -> tuple<vector<int>, vector<int>, vector<int>> {
            vector<int> values;       // 非零元素的值
            vector<int> col_indices;  // 非零元素的列索引
            vector<int> row_offsets = ; // 行偏移量

            for (const auto& row : matrix) {
                int non_zero_count = 0;
                for (int col_idx = 0; col_idx < row.size(); col_idx++) {
                    if (row[col_idx] != 0) {
                        values.push_back(row[col_idx]);
                        col_indices.push_back(col_idx);
                        non_zero_count++;
                    }
                }
                row_offsets.push_back(row_offsets.back() + non_zero_count);
            }
            return {values, col_indices, row_offsets};
        };

        // 将 mat1 和 mat2 转换为 CSR 格式
        auto [mat1_values, mat1_col_indices, mat1_row_offsets] = to_csr(mat1);
        auto [mat2_values, mat2_col_indices, mat2_row_offsets] = to_csr(mat2);

        // 初始化结果矩阵
        int m = mat1.size();  // mat1 的行数
        int n = mat2.size();  // mat2 的列数
        vector<vector<int>> result(m, vector<int>(n, 0));

        // 计算矩阵乘法
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                // 计算 mat1 的第 i 行和 mat2 的第 j 列的点积
                int sum_val = 0;
                // 遍历 mat1 的第 i 行的非零元素
                int row_start = mat1_row_offsets[i];
                int row_end = mat1_row_offsets[i + 1];
                for (int k = row_start; k < row_end; k++) {
                    // 获取 mat1 的非零元素的列索引
                    int col_mat1 = mat1_col_indices[k];
                    // 遍历 mat2 的第 col_mat1 行的非零元素
                    int row_start_mat2 = mat2_row_offsets[col_mat1];
                    int row_end_mat2 = mat2_row_offsets[col_mat1 + 1];
                    for (int l = row_start_mat2; l < row_end_mat2; l++) {
                        // 如果 mat2 的非零元素的列索引等于 j
                        if (mat2_col_indices[l] == j) {
                            sum_val += mat1_values[k] * mat2_values[l];
                        }
                    }
                }
                result[i][j] = sum_val;
            }
        }

        return result;
    }
};
```

