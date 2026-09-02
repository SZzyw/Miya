---
title: LeetCode 21：合并两个有序链表
created: 2026-09-01
updated: 2026-09-01
type: problem
tags: [linked-list]
tags-ch: [链表]
sources: [raw/notes/算法讲解009【入门】单双链表.md]
difficulty: D
source_url: https://leetcode.cn/problems/merge-two-sorted-lists/
---

# LeetCode 21：合并两个有序链表

## 题目来源

原题链接：[LeetCode 21：合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

## 题面

将两个升序链表合并为一个新的升序链表并返回，使用给定节点拼接。

## 难度评估

D（入门/基础）：核心是维护链表节点之间的连接关系。

## 解题思路

使用节点的 `next` 或 `pre` 记录连接。插入时先保存原连接，再同时修改受影响的相邻节点；删除时让删除节点两侧直接相连。

## 复杂度分析

单次链表操作只修改常数个连接，时间复杂度为 $O(1)$；遍历链表为 $O(n)$，额外空间取决于保存节点的方式。

## 教练代码

```cpp
class Solution {
public:
    ListNode *mergeTwoLists(ListNode *list1, ListNode *list2) {
        // 任意一条链表为空时，另一条已经是合并结果的剩余部分。
        if (list1 == nullptr)
            return list2;
        if (list2 == nullptr)
            return list1;
        ListNode *head, *now;

        // 先选出较小的头节点作为结果头；相等时按教练代码选择 list2。
        if (list1->val < list2->val) {
            head = list1;
            list1 = list1->next;
        } else {
            head = list2;
            list2 = list2->next;
        }
        now = head;

        // 每次把当前较小的节点接到结果尾部，并推进对应链表。
        while (list1 != nullptr && list2 != nullptr) {
            if (list1->val < list2->val) {
                now->next = list1;
                list1 = list1->next;
            } else {
                now->next = list2;
                list2 = list2->next;
            }
            now = now->next;
        }

        // 一条链表耗尽后，直接接上另一条的剩余有序部分。
        if (list1 != nullptr)
            now->next = list1;
        else
            now->next = list2;
        return head;
    }
};

```

## 坑点

- 空链表必须先处理。
- 一条链表耗尽后要接上另一条的剩余部分。

## 关联知识页

[[算法讲解009【入门】单双链表]]

^[raw/notes/算法讲解009【入门】单双链表.md]
