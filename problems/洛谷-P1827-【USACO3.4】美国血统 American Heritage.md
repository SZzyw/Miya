---
title: 洛谷 P1827【USACO3.4】美国血统 American Heritage
created: 2026-09-02
updated: 2026-09-02
type: problem
tags:
  - binary-tree
tags-ch:
  - 二叉树
sources:
  - knowledge/算法讲解017【入门】二叉树及其三种序的递归实现.md
difficulty: D
source_url: https://www.luogu.com.cn/problem/P1827
---

# 洛谷 P1827【USACO3.4】美国血统 American Heritage

## 题目来源

- 平台：洛谷
- 题号：P1827
- 原题链接：[P1827【USACO3.4】美国血统 American Heritage](https://www.luogu.com.cn/problem/P1827)

## 题面

给出一棵二叉树的中序与前序排列，求出这棵树的后序排列。每头奶牛的姓名被表示为一个唯一的大写字母，树的节点数不超过 `26`。

### 输入格式

- 第一行输入一个字符串，表示这棵树的中序遍历；
- 第二行输入一个字符串，表示同一棵树的前序遍历。

### 输出格式

输出一行字符串，表示这棵树的后序遍历。

## 难度评估

D（入门）：题目只需要利用前序序列确定根、利用中序序列划分左右子树，再按照后序顺序输出。

## 解题思路

这道题同样不需要真正建立树节点，可以递归处理当前子树对应的中序和前序字符串。

对于当前子树：

1. 前序遍历顺序是“根、左、右”，所以前序序列的第一个字符一定是当前子树的根；
2. 在中序序列中找到根。根左边是左子树，根右边是右子树；
3. 如果根在中序序列中的下标为 `k`，那么左子树有 `k` 个节点。前序序列去掉根之后，前 `k` 个字符属于左子树，剩余字符属于右子树；
4. 先递归左子树，再递归右子树，最后输出根，得到后序遍历。

当当前中序序列长度为 `0` 时，当前子树为空，递归结束。

### 代码对应关系

- `pre[0]`：当前前序序列的第一个字符，即当前根；
- `in.find(pre[0])`：在中序序列中定位根，确定左右子树的大小；
- `posFind`：递归划分并保存每个节点的左右孩子；
- `posOrder`：按照“左、右、根”输出后序序列。

## 复杂度分析

设节点数为 `n`。按照教练代码使用字符串查找、删除和截取的实现方式，最坏时间复杂度为 `O(n^2)`，额外空间复杂度为 `O(n^2)`（包括递归过程中产生的字符串副本）；节点数组本身只占用 `O(n)` 空间。题目节点数不超过 `26`，该复杂度可以满足要求。

## 教练代码

```cpp
#include <bits/stdc++.h>
using namespace std;
using PII = array<int, 2>;
vector<PII> tree(30);

int posFind(string in, string pre) {
    int n = in.size();
    if (n == 0)
        return -1;

    // 前序第一个字符是当前子树的根，在中序中找到它来划分左右子树。
    int num = pre[0] - 'A';
    int k = in.find(pre[0]);
    pre.erase(pre.begin());

    // 左子树占前序剩余部分的前 k 个字符，右子树占其余字符。
    tree[num][0] = posFind(in.substr(0, k), pre.substr(0, k));
    tree[num][1] = posFind(in.substr(k + 1), pre.substr(k));
    return num;
}

void posOrder(int head) {
    // -1 表示空子树；没有节点时直接结束当前递归。
    if (head == -1)
        return;

    // 先处理左右子树，最后输出当前根节点，形成后序遍历。
    posOrder(tree[head][0]);
    posOrder(tree[head][1]);
    cout << char(head + 'A');
}

void solve() {
    string in, pre;
    cin >> in >> pre;
    posOrder(posFind(in, pre));
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

    int T = 1;
    // cin>>T;
    while (T--)
        solve();
    return 0;
}
```

## 坑点

- 前序序列的第一个字符是当前子树的根；不要与 P1030 中“后序序列的最后一个字符是根”混淆。
- 中序序列中根左侧的长度决定前序序列中左子树部分的长度。
- `substr` 的第二个参数表示截取长度，不是终点下标。
- 代码用 `-1` 表示空子树，输出函数必须以 `head == -1` 作为终止条件。
- 节点使用不同的大写字母表示，因此可以用 `字符 - 'A'` 作为数组下标。

## 关联知识页

[[算法讲解017【入门】二叉树及其三种序的递归实现]]

^[raw/notes/算法讲解017【入门】二叉树及其三种序的递归实现.md]
