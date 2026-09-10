---
title: LeetCode 225：用队列实现栈
created: 2026-09-10
updated: 2026-09-10
type: problem
tags: [queue, stack]
tags-ch: [队列, 栈]
sources: [language/语法讲解 队列和栈]
difficulty: C
source_url: https://leetcode.cn/problems/implement-stack-using-queues/
---

# LeetCode 225：用队列实现栈

## 题目来源

- 平台：LeetCode
- 题号：225
- 原题链接：[用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues/)

## 题面

请你仅使用两个队列实现一个后入先出（LIFO）的栈，并支持普通栈的全部四种操作（`push`、`top`、`pop` 和 `empty`）。

实现 `MyStack` 类：

- `void push(int x)`：将元素 `x` 压入栈顶；
- `int pop()`：移除并返回栈顶元素；
- `int top()`：返回栈顶元素；
- `boolean empty()`：如果栈是空的，返回 `true`；否则返回 `false`。

注意：只能使用队列的标准操作，也就是 `push to back`、`peek/pop from front`、`size` 和 `is empty` 这些操作。

示例：

```text
输入：
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]

输出：
[null, null, null, 2, 2, false]
```

提示：

- `1 <= x <= 9`
- 最多调用 `100` 次 `push`、`pop`、`top` 和 `empty`
- 每次调用 `pop` 和 `top` 都保证栈不为空

进阶：能否仅用一个队列来实现栈。

## 涉及知识点

- 队列（`queue`）、栈（`stack`）：两种受限的线性结构。
- 用队列的“取出队首再放回队尾”模拟栈顶。

## 难度评估

C（基础）：要想到“把队首不断转到队尾，最后进队的元素就会转到队首”这一步；另外 `top` 需要把元素放回去，容易写漏。

## 解法一：一个队列旋转

### 解题思路

队列是先进先出，栈顶元素却是最后进队的那个，也就是在队尾。于是可以在取元素时做一次旋转：把队首取出再放到队尾，重复 `size - 1` 次之后，原来在队尾的元素就转到了队首，此时它就是栈顶。

- `push(x)`：直接入队，新元素成为队尾；
- `pop()`：把前 `size - 1` 个元素逐次转到队尾，然后队首就是栈顶元素，取出并弹出；
- `top()`：同样旋转，但取到队首的值之后要把它**放回去**：先把值推到队尾，再把原来队首的那一份弹出，队列顺序恢复原样，元素也没有被删除；
- `empty()`：直接看队列是否为空。

旋转次数必须是 `size - 1`：旋转 `size - 1` 次时最后进队的元素刚好来到队首；如果转满 `size` 次，队列会回到原样。

### 复杂度分析

- 时间复杂度：`push` 是 `O(1)`；`pop` 和 `top` 每次要旋转 `size - 1` 次，是 `O(n)`；`empty` 是 `O(1)`。
- 额外空间复杂度：`O(n)`，队列需要存放全部元素；旋转过程不需要额外数组，只用常数个变量。

### 教练代码

```cpp
class MyStack {
public:
    queue<int> que;

    MyStack() {
    }

    void push(int x) {
        que.push(x);
    }

    int pop() {
        // 把前 size - 1 个元素转到队尾，剩下的队首就是栈顶。
        int n = que.size() - 1;
        while (n--) {
            que.push(que.front());
            que.pop();
        }
        int value = que.front();
        que.pop();
        return value;
    }

    int top() {
        int n = que.size() - 1;
        while (n--) {
            que.push(que.front());
            que.pop();
        }
        int value = que.front();
        que.push(value); //记得放回去
        que.pop();
        return value;
    }

    bool empty() {
        if (que.size() > 0)
            return false;
        return true;
    }
};
```

### 坑点

- `top` 里 `que.push(value);` 之后必须再 `que.pop();`：先复制一份到队尾，再弹掉原来队首的那一份，队列顺序才恢复，元素也没有丢。少了这两步，要么元素被删除，要么队列顺序错乱。
- 旋转次数是 `size - 1` 而不是 `size`，用错会取到错误的元素（转满一圈会回到原状态）。
- `pop` 与 `top` 的旋转部分相同，区别只在取到值之后是否放回。
- 题目还留了一个进阶：只用一个队列实现栈。这份代码实际上就只用了一个队列，可以沿着这个方向思考。

## 关联知识页

- [[语法讲解 队列和栈]]：栈与队列的实现，以及本题的完整说明。
- [[LeetCode-232-用栈实现队列]]：把两种结构反过来模拟，可以对比两者的思路差别。
- [[洛谷-B3616-【模板】队列]]：队列的基础实现与操作。

^[language/语法讲解 队列和栈.md]
