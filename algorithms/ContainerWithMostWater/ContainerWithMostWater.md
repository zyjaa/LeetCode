题意：找最大的容水量



**示例 1：**

![img](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/07/25/question_11.jpg)

```
输入：[1,8,6,2,5,4,8,3,7]
输出：49 
解释：图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。
```

**示例 2：**

```
输入：height = [1,1]
输出：1
```

 

- `n == height.length`
- `2 <= n <= 105`
- `0 <= height[i] <= 104`



### 法一：双指针

双指针两端相向扫描，每次移动都判断是否超过原有答案



```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int l=0,r=height.size()-1;
        int res=0;
        while(l<r){
            if(height[l]<height[r]){
                res=max(res,height[l]*(r-l));
                l++;
            }
            else{
             res=max(res,height[r]*(r-l));
             r--;
            }
        }
        return res;
    }
};
```



- 时间复杂度：O(N)，2个指针扫一遍数组
- 空间复杂度：O(1)





