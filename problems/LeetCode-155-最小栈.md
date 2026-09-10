---
title: LeetCode 155：最小栈
created: 2026-09-10
updated: 2026-09-10
type: problem
tags: [stack]
tags-ch: [栈]
sources: [language/语法讲解 队列和栈]
difficulty: C
source_url: https://leetcode.cn/problems/min-stack/
---

# LeetCode 155：最小栈

## 题目来源

- 平台：LeetCode
- 题号：155
- 原题链接：[最小栈](https://leetcode.cn/problems/min-stack/)

## 题面

设计一个支持 `push`、`pop`、`top` 操作，并能在常数时间内检索到最小元素的栈。

实现 `MinStack` 类：

- `MinStack()`：初始化堆栈对象；
- `void push(int value)`：将元素 `value` 推入堆栈；
- `void pop()`：删除堆栈顶部的元素；
- `int top()`：获取堆栈顶部的元素；
- `int getMin()`：获取堆栈中的最小元素。

示例：

```text
输入：
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

输出：
[null,null,null,null,-3,null,0,-2]
```

提示：

- `-2^31 <= val <= 2^31 - 1`
- `pop`、`top` 和 `getMin` 操作总是在非空栈上调用
- `push`、`pop`、`top` 和 `getMin` 最多被调用 `3 * 10^4` 次

## 涉及知识点

- 栈（`stack`）：后进先出的线性结构。
- 用辅助栈记录前缀最小值，把 `getMin` 降到常数时间。

## 难度评估

C（基础）：思路是“用空间换时间”，关键在于想清楚辅助栈里存的不是单个最小值，而是每一层对应的前缀最小值；代码短但容易在同步增删上出错。

## 解法一：主栈加辅助栈记录前缀最小值

### 解题思路

要在常数时间内取到最小值，就不能在 `getMin` 时扫描整个栈，而要随时把最小值准备好。做法是再开一个辅助栈 `mmin`：

- `sta` 是主栈，按正常顺序存放元素；
- `mmin` 与 `sta` 同步增长，`mmin` 的栈顶始终等于 `sta` 中所有元素的最小值。每次 `push(value)`，`mmin` 压入的是 `min(mmin.top(), value)`，也就是“加入这个元素之后的前缀最小值”。

这样 `getMin()` 只需要返回 `mmin.top()`；`pop()` 时两个栈一起弹出，`mmin` 的栈顶就又回到了上一层的答案。

构造函数里先给两个栈各压入一个 `INT_MAX` 作为哨兵：这样 `push` 中可以直接调用 `mmin.top()` 而不用先判断空栈，代码更简洁；哨兵比任何可能的元素都大，不会影响最小值的结果。

### 复杂度分析

- 时间复杂度：`push`、`pop`、`top`、`getMin` 都是 `O(1)`，每个操作只做常数次栈操作。
- 额外空间复杂度：`O(n)`。辅助栈与主栈等长，是这份实现为了常数时间查询付出的空间代价；每个元素会被调用最多 `3 * 10^4` 次，这个空间完全够用。

### 教练代码

```cpp
class MinStack {
public:
    stack<int> sta, mmin;

    MinStack() {
        // 先压入哨兵，避免在空栈上调用 top()。
        sta.push(INT_MAX);
        mmin.push(INT_MAX);
    }

    void push(int value) {
        sta.push(value);
        // 辅助栈记录加入当前元素之后的前缀最小值。
        mmin.push(min(mmin.top(), value));
    }

    void pop() {
        // 两个栈必须同步弹出，mmin 的栈顶才始终对应主栈的最小值。
        sta.pop();
        mmin.pop();
    }

    int top() {
        return sta.top();
    }

    int getMin() {
        return mmin.top();
    }
};
```

### 坑点

- 两个栈必须同步增删。如果只弹 `sta` 不弹 `mmin`，`getMin` 会返回已经不在栈里的旧元素。
- 构造函数压入的 `INT_MAX` 是哨兵，它不参与实际数据，但保证 `push` 里 `mmin.top()` 一定有值；`INT_MAX` 比题目范围内任何元素都大，所以不会影响最小值。
- `getMin` 返回的是辅助栈栈顶，不要写成主栈的某个位置，那样就退化成了 `O(n)` 的查找。
- 题目保证 `pop`、`top`、`getMin` 都在非空栈上调用，所以不需要额外处理空栈的情况。

## 关联知识页

- [[语法讲解 队列和栈]]：栈与队列的实现，以及本题的完整说明。
- [[LeetCode-232-用栈实现队列]]：同样是用额外的栈换取功能，可以对比“空间换时间”的两种用法。
- [[语法讲解 堆结构]]：如果需要随时取最小值又允许插入删除任意元素，堆才是合适的选择。

^[language/语法讲解 队列和栈.md]
