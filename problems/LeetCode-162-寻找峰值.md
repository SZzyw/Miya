---
title: LeetCode 162：寻找峰值
created: 2026-08-22
updated: 2026-08-22
type: problem
tags: [binary-search]
tags-ch: [二分搜索]
sources: [raw/notes/算法讲解006【入门】二分搜索.md]
difficulty: D
source_url: https://leetcode.cn/problems/find-peak-element/
confidence: medium
---

# LeetCode 162：寻找峰值

## 题目来源

- 平台：LeetCode
- 题号：162
- 原题链接：[寻找峰值](https://leetcode.cn/problems/find-peak-element/)

## 题面

给定一个下标从 0 开始的整数数组 nums，找到任意一个峰值并返回它的下标。

如果一个元素严格大于它相邻的元素，那么这个元素就是峰值。数组两端之外的元素视为负无穷，因此第一个和最后一个元素也可能成为峰值。题目保证相邻元素不相等，并要求使用 O(log n) 的算法。

## 知识点

- 精确标签：二分搜索
- 关联知识页：[[算法讲解006【入门】二分搜索]]

## 难度评估

D（入门）：题目不要求数组整体有序，重点是理解“沿着上坡方向一定能找到峰值”，并据此排除一半区间。

## 解题思路

先单独判断数组两端：

1. 如果数组只有一个元素，返回 0。
2. 如果第一个元素大于第二个元素，第一个元素就是峰值。
3. 如果最后一个元素大于倒数第二个元素，最后一个元素就是峰值。

如果两端都不是峰值，那么下标 1 到 n - 2 的范围内一定存在峰值。对这个范围进行二分：

- 如果 nums[m] 大于左右邻居，直接返回 m。
- 如果左邻居大于 nums[m]，向左继续查找。
- 否则向右继续查找。

## 教练代码

```cpp
class Solution {
public:
    // 峰值二分：O(log n) 时间，O(1) 额外空间
    int exist(vector<int> &arr) {
        int l = 1, r = arr.size() - 2;

        while (l <= r) {
            int m = l + (r - l) / 2;

            if (arr[m] > arr[m - 1] && arr[m] > arr[m + 1]) {
                return m;
            }

            if (arr[m - 1] > arr[m]) {
                // 左侧处于上坡方向，左侧一定能找到峰值
                r = m - 1;
            } else {
                // 右侧处于上坡方向，右侧一定能找到峰值
                l = m + 1;
            }
        }

        return l;
    }

    // 处理两端峰值后，在中间范围内使用二分查找
    int findPeakElement(vector<int>& nums) {
        int n = nums.size() - 1;

        if (nums.size() == 1 || nums[0] > nums[1]) {
            return 0;
        }

        if (nums[n] > nums[n - 1]) {
            return n;
        }

        return exist(nums);
    }
};
```

## 复杂度

时间复杂度为 O(log n)，额外空间复杂度为 O(1)。

## 代码中的关键点与坑

- 这份代码依赖题目的条件：相邻元素不相等，数组两端之外视为负无穷。
- exist 只处理内部区间；两端峰值由 findPeakElement 先判断。
- arr[m - 1] > arr[m] 时向左，其他情况向右，是因为只要沿着上坡方向走，就一定能遇到峰值。
- 题目允许返回任意一个峰值，因此找到一个就可以返回，不必寻找下标最小的峰值。

## 作答情况

raw 笔记提供了教练代码，未提供额外的提交记录或错误记录。

^[raw/notes/算法讲解006【入门】二分搜索.md]

