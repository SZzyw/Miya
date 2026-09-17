[231. 2 的幂 - 力扣（LeetCode）](https://leetcode.cn/problems/power-of-two/description/)

2的幂说明只有二进制中仅仅只有1个1
如果有多个1，就说明这个数是由多个2的幂相加所组成的。


```c++
class Solution {
public:
    bool isPowerOfTwo(int n) {
        return n > 0 && n == ((unsigned int) n & -(unsigned int) n);
    }
};
```