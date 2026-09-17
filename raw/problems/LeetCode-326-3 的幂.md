[326. 3 的幂 - 力扣（LeetCode）](https://leetcode.cn/problems/power-of-three/submissions/749395725/)
质因数分解的唯一性：任何一个大于 1 的整数 N，都可以唯一地写成若干个质数的乘积
刚好3是个质因数。
所以3的幂一定是只由3这个质因数所组成的
那就可以按数据范围去到3的最大的幂，然后看数能不能除尽

```c++
class Solution {
public:
    bool isPowerOfThree(int n) {
        return n > 0 && 1162261467 % n == 0;
    }
};
```