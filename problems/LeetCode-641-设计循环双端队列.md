---
title: LeetCode 641：设计循环双端队列
created: 2026-09-10
updated: 2026-09-10
type: problem
tags: [deque]
tags-ch: [双端队列]
sources: [language/语法讲解 双端队列]
difficulty: C
source_url: https://leetcode.cn/problems/design-circular-deque/description/
---

# LeetCode 641：设计循环双端队列

## 题目来源

- 平台：LeetCode
- 题号：641
- 原题链接：[设计循环双端队列](https://leetcode.cn/problems/design-circular-deque/description/)

## 题面

设计实现双端队列。实现 `MyCircularDeque` 类：

- `MyCircularDeque(int k)`：构造函数，双端队列最大为 `k`。
- `boolean insertFront(int value)`：将一个元素添加到双端队列头部。如果操作成功返回 `true`，否则返回 `false`。
- `boolean insertLast(int value)`：将一个元素添加到双端队列尾部。如果操作成功返回 `true`，否则返回 `false`。
- `boolean deleteFront()`：从双端队列头部删除一个元素。如果操作成功返回 `true`，否则返回 `false`。
- `boolean deleteLast()`：从双端队列尾部删除一个元素。如果操作成功返回 `true`，否则返回 `false`。
- `int getFront()`：从双端队列头部获得一个元素。如果双端队列为空，返回 `-1`。
- `int getRear()`：获得双端队列的最后一个元素。如果双端队列为空，返回 `-1`。
- `boolean isEmpty()`：若双端队列为空，则返回 `true`，否则返回 `false`。
- `boolean isFull()`：若双端队列满了，则返回 `true`，否则返回 `false`。

示例：

```text
输入：
["MyCircularDeque", "insertLast", "insertLast", "insertFront", "insertFront", "getRear", "isFull", "deleteLast", "insertFront", "getFront"]
[[3], [1], [2], [3], [4], [], [], [], [4], []]

输出：
[null, true, true, true, false, 2, true, true, true, 4]
```

提示：

- `1 <= k <= 1000`
- `0 <= value <= 1000`
- `insertFront`、`insertLast`、`deleteFront`、`deleteLast`、`getFront`、`getRear`、`isEmpty`、`isFull` 的调用次数不大于 `2000` 次

## 涉及知识点

- 双端队列（`deque`）：两端都支持插入和删除的队列。
- 用定长数组加左右两个下标描述队列区间，并用取模实现循环下标。

## 难度评估

C（基础）：算法本身不复杂，难点在循环下标的边界处理和“空/满”的判定，要把两端的插入删除都用同一套下标规律表达出来。

## 解法一：数组加双下标，取模实现循环

### 解题思路

用定长数组 `deq` 存放数据，用 `l`、`r` 标出队列占据的下标区间 `[l, r]`：

- 初始状态 `l = 0`、`r = -1`，此时区间为空，元素个数 `r - l + 1 = 0`；
- 插入只移动对应的端点再写入数据：尾插先 `r++`、写到 `(r + n) % n`，头插先 `l--`、写到 `(l + n) % n`；
- 删除只移动端点，不搬动数据：头删 `l++`，尾删 `r--`；
- 读取队首、队尾元素同样要经过 `(下标 + n) % n`，因为端点可能已经绕过数组边界；
- 是否为空由 `size() == 0` 决定，是否已满由 `size() == n` 决定，其中 `n = k` 是容量上限；两种判断都不看某个位置上残留的值。

取模之前先给下标加 `n`：队列里最多同时有 `n` 个元素，头插时 `l` 最多减到 `-n`，所以 `l + n` 一定不小于 0，取模结果不会出现负数。构造函数虽然多开了 10 个位置，但读写范围完全由取模决定，多出来的位置只是余量。

### 复杂度分析

- 时间复杂度：`O(1)`。每个操作只做常数次下标运算和一次赋值，与队列中的元素个数无关。
- 额外空间复杂度：`O(k)`。需要一个能容纳队列元素的数组，除此之外只用 `l`、`r`、`n` 等常数个变量。

### 教练代码

```cpp
class MyCircularDeque {
public:
    vector<int> deq;
    int l, r, n;

    MyCircularDeque(int k) {
        // 多开 10 个位置留作余量；n 取容量上限 k，同时也是取模范围。
        deq.resize(k + 10);
        n = k;
        l = 0, r = -1;
    }

    // 队列中的元素个数就是区间 [l, r] 的长度。
    int size() {
        return r - l + 1;
    }

    bool insertFront(int value) {
        // 元素个数达到容量上限就不能再插入。
        if (this->size() == n)
            return false;
        // 头插：先把 l 左移一格，再按循环下标写入数据。
        l--;
        deq[(l + n) % n] = value;
        return true;
    }

    bool insertLast(int value) {
        if (this->size() == n)
            return false;
        // 尾插：先把 r 右移一格，再按循环下标写入数据。
        r++;
        deq[(r + n) % n] = value;
        return true;
    }

    bool deleteFront() {
        if (this->size() == 0)
            return false;
        // 删除只移动边界下标，原来的数据被排除在区间之外。
        l++;
        return true;
    }

    bool deleteLast() {
        if (this->size() == 0)
            return false;
        r--;
        return true;
    }

    int getFront() {
        if (this->size() == 0)
            return -1;
        return deq[(l + n) % n];
    }

    int getRear() {
        if (this->size() == 0)
            return -1;
        return deq[(r + n) % n];
    }

    bool isEmpty() {
        if (this->size() == 0)
            return true;
        return false;
    }

    bool isFull() {
        // 元素个数达到容量上限 n 才算满。
        if (this->size() == n)
            return true;
        return false;
    }
};
```

### 坑点

- 头插和尾插的区别只是先移动 `l` 还是先移动 `r`，写入时都必须取模，否则 `l = -1` 会写到数组外。
- 删除操作不清空数据，之后再插入会覆盖旧值；因此判断队列状态只能依据 `size()`。
- 取出队首、队尾元素前要先判空，题目要求空队列返回 `-1`。
- 判满用的是 `size() == n`，其中 `n = k` 是容量上限，不是数组长度。数组虽然开了 `k + 10` 个位置，但读写范围由取模决定，多出来的位置只是余量，不会让队列超出题目要求的 `k` 个元素。
- 判空和判满都只看 `size()`，不要去看某个位置上残留的值：删除只移动下标，旧数据仍然留在数组里。

## 关联知识页

- [[语法讲解 双端队列]]：循环数组、双下标区间和取模写法的完整说明。
- [[语法讲解 队列和栈]]：普通队列的数组实现，对比双端队列多开放了哪一端。

^[language/语法讲解 双端队列.md]
