
#### 解题思路
根据随机快速排序的思路，每次选一个数，比这个小的放左边，相等放中间，大于放右边，再看第k个是在3个区间的哪个范围，继续递归下去

#### 时间复杂度和空间复杂度
时间复杂度O(n)，额外空间复杂度O(1)

#### 代码
```c++
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    array<int, 2> partition(vector<int> &arr, int l, int r, int x) {
        int first = l, last = r;
        for (int i = l; i <= last; i++) {
            if (arr[i] < x)
                swap(arr[i], arr[first++]);
            else if (arr[i] > x)
                swap(arr[i--], arr[last--]);
        }
        return {first, last};
    }

    int findKthLargest(vector<int> &nums, int k) {
        int l = 0, r = nums.size() - 1;
		srand(time(0));
        while (1) {
            int x = nums[rand() % (r - l + 1) + l];
            array<int, 2> mid = partition(nums, l, r, x);
            if (k <= r - mid[1])
                l = mid[1] + 1;
            else if (k <= r - mid[0] + 1)
                return x;
            else
                k -= (r - mid[0] + 1), r = mid[0] - 1; //注意顺序，必须先更新k再更新r
        }
    }
};
```

