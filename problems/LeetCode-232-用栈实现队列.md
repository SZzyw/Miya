---
title: LeetCode 232：用栈实现队列
created: 2026-09-10
updated: 2026-09-10
type: problem
tags: [stack, queue]
tags-ch: [栈, 队列]
sources: [language/语法讲解 队列和栈]
difficulty: C
source_url: https://leetcode.cn/problems/implement-queue-using-stacks/description/
---

# LeetCode 232：用栈实现队列

## 题目来源

- 平台：LeetCode
- 题号：232
- 原题链接：[用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks/description/)

## 题面

请你仅使用两个栈实现先入先出队列。队列应当支持一般队列支持的所有操作（`push`、`pop`、`peek`、`empty`）：

实现 `MyQueue` 类：

- `void push(int x)`：将元素 `x` 推到队列的末尾；
- `int pop()`：从队列的开头移除并返回元素；
- `int peek()`：返回队列开头的元素；
- `boolean empty()`：如果队列为空，返回 `true`；否则返回 `false`。

说明：只能使用标准的栈操作，也就是只有 `push to top`、`peek/pop from top`、`size` 和 `is empty` 操作是合法的。

示例：

```text
输入：
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]

输出：
[null, null, null, 1, 1, false]
```

提示：

- `1 <= x <= 9`
- 最多调用 `100` 次 `push`、`pop`、`peek` 和 `empty`
- 假设所有操作都是有效的（例如，一个空的队列不会调用 `pop` 或者 `peek`）

进阶：能否实现每个操作均摊时间复杂度为 `O(1)` 的队列？换句话说，执行 `n` 个操作的总时间复杂度为 `O(n)`，即使其中一个操作可能花费较长时间。

## 涉及知识点

- 栈（`stack`）、队列（`queue`）：两种受限的线性结构。
- 用两个栈模拟队列，以及均摊复杂度分析。

## 难度评估

C（基础）：思路需要一点转换——把“反转顺序”这件事交给两个栈分工完成；代码本身不长，但要理解为什么每个元素只会被搬一次。

## 解法一：一个栈进、一个栈出

### 解题思路

栈只能在栈顶进出，队列要一端进、另一端出，所以用两个栈分工：`in` 专门负责入队，`out` 专门负责出队。

- `push(x)`：直接压进 `in`；
- 需要出队时，如果 `out` 是空的，就把 `in` 里的元素逐个弹出并压入 `out`。元素经过两次进出，顺序正好被反转一次，最早进入 `in` 的元素会跑到 `out` 的栈顶；
- 之后 `pop` 和 `peek` 都从 `out` 的栈顶取，正好符合先进先出；
- `empty()`：两个栈都空，队列才空。

关键点是**只在 `out` 为空时才搬运**：如果每次出队都搬运，会把已经排好的顺序再次打乱；而限制搬运时机之后，每个元素从 `in` 搬到 `out` 最多只发生一次。

### 复杂度分析

- 时间复杂度：`push` 是 `O(1)`。`pop`、`peek` 单次最坏是 `O(n)`（需要搬运），但每个元素最多只被搬运一次，所以连续执行 `n` 次操作的总代价是 `O(n)`，均摊到每次是 `O(1)`，满足题目的进阶要求。
- 额外空间复杂度：`O(n)`，两个栈合计存放全部元素；除此之外只使用常数个变量。

### 教练代码

```cpp
class MyQueue {
public:
    stack<int> in, out;

    MyQueue() {
    }

    void push(int x) {
        in.push(x);
    }

    int pop() {
        // 只在出栈为空时搬运，保证每个元素最多被搬一次。
        if (out.size() == 0) {
            while (in.size()) {
                out.push(in.top());
                in.pop();
            }
        }
        int value = out.top();
        out.pop();
        return value;
    }

    int peek() {
        // peek 也要先保证出栈里有元素，然后再看栈顶。
        if (out.size() == 0) {
            while (in.size()) {
                out.push(in.top());
                in.pop();
            }
        }
        return out.top();
    }

    bool empty() {
        // 两个栈都空，队列才是空的。
        if (in.size() + out.size() > 0)
            return false;
        return true;
    }
};
```

### 坑点

- `out` 里还有元素时不能搬运，否则会把已经反转好的顺序再打乱，出队顺序就错了。
- `peek` 必须和 `pop` 一样先检查并搬运，不能在 `out` 为空时直接取栈顶。
- 判断队列是否为空要同时看两个栈，只看 `in` 或只看 `out` 都会判错。
- 这份实现空间是 `O(n)`、均摊时间是 `O(1)`，与题目的进阶要求一致。

## 关联知识页

- [[语法讲解 队列和栈]]：栈与队列的实现，以及本题的完整说明。
- [[LeetCode-225-用队列实现栈]]：把两种结构反过来模拟，可以对比两者的思路差别。
- [[LeetCode-155-最小栈]]：同样是栈的封装，用辅助栈换取常数时间的查询。

^[language/语法讲解 队列和栈.md]
