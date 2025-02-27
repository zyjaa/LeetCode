```
class Solution {
public static int[] singleNumber(int[] nums) {
    int eor1 = 0;
    for (int num : nums) {
        // nums中有2种数a、b出现了奇数次，其他的数都出现了偶数次
        eor1 ^= num;
    }
    // eor1 : a ^ b
    // Brian Kernighan算法
    // 提取出二进制里最右侧的1
    int rightOne = eor1 & (-eor1);//这一位置是1，说明a,b这一位置一个为0，一个为1
    int eor2 = 0;
    for (int num : nums) {
        if ((num & rightOne) !=0) {//只要这一位置是0的全^，最终得到其中一个数字
            eor2 ^= num;
        }
    }
    return new int[] { eor2, eor1 ^ eor2 };
}
}
```





```
#include <vector>

using namespace std;

class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int eor1 = 0;
        for (int num : nums) {
            // eor1 : a ^ b
            eor1 ^= num;
        }

        // 提取出二进制里最右侧的1
        int rightOne = eor1 & (-eor1);//这一位置是1，说明a,b这一位置一个为0，一个为1

        int eor2 = 0;
        for (int num : nums) {
            if ((num & rightOne) != 0) {//只要这一位置是1的全^，最终得到其中一个数字
                // 只对这一位为1的数字进行异或
                eor2 ^= num;
            }
        }

        return {eor2, eor1 ^ eor2};
    }
};
```

