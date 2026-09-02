---
title: LeetCode 86：分隔链表
created: 2026-09-01
updated: 2026-09-01
type: problem
tags: [linked-list]
tags-ch: [链表]
sources: [raw/notes/算法讲解009【入门】单双链表.md]
difficulty: C
source_url: https://leetcode.cn/problems/partition-list/description/
---

# LeetCode 86：分隔链表

## 题目来源

原题链接：[LeetCode 86：分隔链表](https://leetcode.cn/problems/partition-list/description/)

## 题面

给定链表和 x，使所有小于 x 的节点位于大于或等于 x 的节点之前，并保持两个分区内的相对顺序。

## 难度评估

C（入门/基础）：核心是维护链表节点之间的连接关系。

## 解题思路

使用节点的 `next` 或 `pre` 记录连接。插入时先保存原连接，再同时修改受影响的相邻节点；删除时让删除节点两侧直接相连。

## 复杂度分析

单次链表操作只修改常数个连接，时间复杂度为 $O(1)$；遍历链表为 $O(n)$，额外空间取决于保存节点的方式。

## 教练代码

```cpp
class Solution {
public:
    ListNode *partition(ListNode *head, int x) {
        ListNode *leftTail = nullptr, *leftHead = nullptr;
        ListNode *rightTail = nullptr, *rightHead = nullptr;
        ListNode *next = nullptr;
        while (head != nullptr) {
            // 先保存后继，再断开当前节点，避免分流后无法继续遍历原链表。
            next = head->next;
            head->next = nullptr;

            // 严格小于 x 的节点进入左链表，其余节点进入右链表。
            if (head->val < x) {
                if (leftHead == nullptr)
                    leftHead = head;
                else
                    leftTail->next = head;
                leftTail = head;
            } else {
                if (rightHead == nullptr)
                    rightHead = head;
                else
                    rightTail->next = head;
                rightTail = head;
            }
            head = next;
        }

        // 没有左链表时，结果就是右链表；否则把两个分区首尾相接。
        if (leftHead == nullptr)
            return rightHead;
        leftTail->next = rightHead;
        return leftHead;
    }
};
```

## 坑点

- 条件是严格小于 `x`。
- 分流前要保存原来的 `next`，避免断开节点后无法继续遍历。

## 关联知识页

[[算法讲解009【入门】单双链表]]

^[raw/notes/算法讲解009【入门】单双链表.md]
