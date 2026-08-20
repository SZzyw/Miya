# Wiki Schema

## Domain
ACM 竞赛教学(面向学生教学与教练备课),使用 C++ 作为教学语言。

## 标签体系(Tag Taxonomy)

两级标签,用途不同:

- **大类标签**(9 个):页面归档用,决定页面在 index.md 的分栏。每个知识页必须至少有一个大类标签。
- **精确标签**:题目(problem)页的 tags 必须使用精确知识点,可多选;知识页也可加精确标签。
- **双写中文(`tags-ch`)**:tags 用英文(检索引擎用),tags-ch 用同一组标签的中文名(人读用),两个字段内容一一对应。
- 精确标签见下方"精确标签列表"(`英文` + 中文名);找不到对应项时先考虑大类,若仍无法确定,***必须问教练***,不猜、不擅自造新标签。

### 大类标签

| 标签                       | 中文    | 覆盖内容                                                       |
| ------------------------ | ----- | ---------------------------------------------------------- |
| `greedy`                 | 贪心    | 贪心策略、反悔贪心                                                  |
| `data-structure`         | 数据结构  | 栈队列堆、链表、并查集、树状数组、线段树、平衡树、ST 表、莫队、二分/三分、二分答案、分治/整体二分、CDQ 分治 |
| `dp`                     | 动态规划  | 线性 DP、背包、区间 DP、树形 DP、状压 DP、数位 DP、记忆化搜索                     |
| `graph`                  | 图论    | 最短路、最小生成树、拓扑、强连通/Tarjan、二分图、网络流、LCA、树上问题                   |
| `number-theory`          | 数论    | 素数、GCD/LCM、欧拉函数、同余、逆元、组合数学、博弈                              |
| `string`                 | 字符串   | 字符串哈希、KMP、AC 自动机、Manacher、后缀数组、字典树                         |
| `computational-geometry` | 计算几何  | 向量、凸包、半平面交、旋转卡壳、极角排序                                       |
| `cpp`                    | C++语言 | 语法、STL                                                     |
| `misc`                   | 其他    | 模拟、高精度、位运算、对拍器                                             |

### 精确标签列表

| 大类                       | 精确标签                                                                                                                                                                                                                                                                                    |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `greedy`                 | `greedy-strategy` 贪心策略, `regret-greedy` 反悔贪心                                                                                                                                                                                                                                            |
| `data-structure`         | `stack` 栈, `queue` 队列, `heap` 堆, `linked-list` 链表, `dsu` 并查集, `fenwick` 树状数组, `segment-tree` 线段树, `balanced-tree` 平衡树, `sparse-table` ST 表, `mo-algorithm` 莫队, `binary-search` 二分/三分, `binary-search-answer` 二分答案, `divide-and-conquer` 分治, `parallel-binary-search` 整体二分, `cdq` CDQ 分治 |
| `dp`                     | `linear-dp` 线性 DP, `knapsack` 背包, `interval-dp` 区间 DP, `tree-dp` 树形 DP, `bitmask-dp` 状压 DP, `digit-dp` 数位 DP, `memoization` 记忆化搜索                                                                                                                                                       |
| `graph`                  | `shortest-path` 最短路, `mst` 最小生成树, `topological-sort` 拓扑排序, `tarjan` 强连通/Tarjan, `bipartite` 二分图, `network-flow` 网络流, `lca` LCA, `tree` 树上问题                                                                                                                                             |
| `number-theory`          | `prime` 素数, `gcd-lcm` GCD/LCM, `euler-phi` 欧拉函数, `congruence` 同余, `inverse` 逆元, `combinatorics` 组合数学, `game-theory` 博弈                                                                                                                                                                  |
| `string`                 | `string-hash` 字符串哈希, `kmp` KMP, `ac-automaton` AC 自动机, `manacher` Manacher, `suffix-array` 后缀数组, `trie` 字典树                                                                                                                                                                             |
| `computational-geometry` | `vector-geo` 向量, `convex-hull` 凸包, `half-plane` 半平面交, `rotating-calipers` 旋转卡壳, `polar-sort` 极角排序                                                                                                                                                                                       |
| `cpp`                    | `cpp-syntax` 语法, `stl` STL                                                                                                                                                                                                                                                              |
| `misc`                   | `simulation` 模拟, `bigint` 高精度, `bitwise` 位运算, `brute-checker` 对拍器                                                                                                                                                                                                                       |

- 新增大类/精确标签需先更新本表(由教练确认),不擅自扩张标签。
- ***标签归属不确定时,必须先问教练***,不猜、不擅自造新标签。

## Conventions

- 页面文件名用中文词组(如 `二分答案.md`)不使用空格。
- 每个 wiki 页面以 YAML frontmatter 开始。
- 使用 `[[wikilinks]]` 做页面互链(如前置知识点、关联题目)。
- 每次修改页面,更新 frontmatter 中的 `updated` 日期。
- 每个页面必须在 `index.md` 的对应栏目登记。
- 每次操作追加到 `log.md`(时间、对象、动作)。
- 来自外部素材的整理,在页面末尾用 `^[raw/xxx/源文件]` 注明来源。

## Frontmatter

```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: knowledge | problem | tool | student | comparison | query
tags: [精确标签]             # 英文,检索用;problem 页必须用精确标签,可多选
tags-ch: [中文标签名]        # 与 tags 一一对应的中文名,人读用
sources: [raw/...]
difficulty: S | A | B | C | D     # 仅 problem 类型必填
source_url: <题目链接>            # 仅 problem 类型必填
confidence: high | medium | low   # 可选
---
```

### raw/ Frontmatter
```yaml
---
source_url: https://example.com
ingested: YYYY-MM-DD
sha256: <sha256 of the body below frontmatter>
---
```

## Page Types

### knowledge — 知识点页
每个算法/知识点一页,教学向骨架:
1. 定义(这个算法什么时候用、解决什么问题)
2. 适用场景与前置知识
3. 核心思路(大白话,面向学生)
4. 标准模板(带逐段注释的代码)
5. 复杂度分析
6. 常见坑
7. 例题(按难度递进,`[[wikilinks]]` 指向 problems 页)
8. 联动(可与哪些知识点组合出联合题)

### problem — 题目页(出题池)
- 教练喂进来的每道题独立一页,全量收录:题面、题目链接、教练作答代码、涉及知识点、难度档位 S/A/B/C/D、作答情况与坑点。
- tags 必须用精确标签(可多个),不使用大类代替。
- 所有题目进入出题池;出题时按"课时数、年龄、已学知识点"匹配难度与知识点。

### tool — 工具页
对拍器、时间/空间估算、输入输出模板、调试技巧等实战工具,单独成页,不混入知识点页。

### student — 学员档案页(将来)
年龄、课时数、已学知识点、刷题记录、难度反馈。数据只能由教练提供,不虚构。

### comparison / query
对比页记录两个及以上对象的维度比较;查询页记录值得保留的检索结果。

## 页面阈值
- 知识页面超过约 200 行时拆分为子页面(如"线段树-进阶")。
- 类似的题目不合并,题目页天然独立。
- 页面内容完全过时时移入 `_archive/`(须教练确认)。

## 更新策略
内容冲突时以教练原意优先;矛盾信息确实存在时,标注两个来源与立场,不擅自取舍。

## 素材投递(raw/ 投递箱)

- `raw/notes/`、`raw/problems/`、`raw/assets/` 是教练的投递口,由教练放入原始素材文件(笔记、题目原文、附件)。
- 教练说"看看 raw/"时,扫描投递箱中的新文件,逐个整理:
  - 笔记 → `knowledge/`(知识点页)
  - 题目 → `problems/`(题目页,评估难度、打精确标签)
  - 附件 → 保留在 `raw/assets/`,被其他页面引用
- 只处理尚未整理过的新文件,整理过的跳过;不修改 raw/ 原文;整理完在回复中列清单给教练确认。

## 目录结构
```text
SCHEMA.md       # 本文件:结构约定与标签体系
index.md        # 主目录(按大类分栏)
log.md          # 追加式操作日志
raw/            # 素材投递箱(不可修改的原始素材)
  notes/        #   笔记原文投递口
  problems/     #   题目原文投递口(题面+链接+代码)
  assets/       #   图片/附件投递口
knowledge/      # 知识点页(算法档案)
problems/       # 出题池题目页
tools/          # 工具页
students/       # 学员档案(将来)
comparisons/    # 对比页
queries/        # 查询档案
```
