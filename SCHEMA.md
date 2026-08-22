# Wiki Schema

## Domain

ACM 竞赛教学与教练备课，使用 C++ 作为教学语言。

本知识库同时保存三类教学材料：

- ACM 算法知识页：放在 knowledge/，按算法大类归档。
- C++ 语言笔记：放在 language/，单独在 index.md 的“语言笔记”栏目登记。
- 实战工具页：放在 tools/。

## 原始笔记优先

raw/notes/ 中的笔记是教练的教学素材。整理后的页面不是原文拼接，而是以原始笔记的主题、主要章节和顺序为骨架，重写成更通俗、连贯、适合备课和教学的正式稿。

整理时遵循以下原则：

- 保留 raw 笔记的文件名，包含“算法讲解”或“语言讲解”编号、难度等信息。
- 保留原始笔记的主要章节和讲解顺序；可以在章节内部重排段落、补足逻辑和润色表达。
- 每个主要章节需要表达的内容、推导、数字例子和特殊情况必须与 raw 原文一致。可以重写说法，但不能把关键推导概括掉、改成另一种意思或用普通结论替代原文的特殊说明。
- 不强制所有笔记套用同一套章节模板。根据每份笔记已有的内容，自行决定解释、示例、代码和补充的位置。
- 可以补充必要的解释、复杂度、常见坑、过程说明和页面链接，使原意更清楚。
- 教练提供了简略示例时，可以把示例展开为完整的输入、过程和结论；没有提供的示例不主动编造。
- 例题只整理教练在笔记或投递箱中明确提供的题目，不主动搜索其他题目扩充页面。
- 发现表达不清、错别字或逻辑跳跃可以直接重写；发现疑似技术错误、算法错误或边界问题时，标记“⚠️ 待教练确认”并询问教练。
- 原始笔记只读，整理产物写入对应目录。任何整理都不得修改、移动或删除 raw 原文。
- 不因页面长度自动拆分页面。是否拆分由教练另行决定。

### 已确认参考页面

整理新页面时可以参考以下已经由教练确认过的页面，学习它们的结构、表达密度、题目独立成页方式和 Markdown 写法：

- `knowledge/算法讲解006【入门】二分搜索.md`
- `problems/LeetCode-162-寻找峰值.md`
- `tools/算法讲解005【入门】对数器.md`

这些页面只作为结构和格式参考，不作为新的事实、例题或代码来源；raw 原文仍然是内容和教练原意的唯一来源。

## 标签体系

### 标签用途

- 大类标签：算法知识页的归档标签，决定页面在 index.md 的算法栏目中所处的分栏。
- 精确标签：页面涉及的具体知识点。题目页必须使用精确标签，知识页可同时使用大类和精确标签。
- tags 使用英文，tags-ch 使用对应中文；两者必须一一对应。
- C++ 语言页使用 topic 表示主题，不使用算法标签，也不使用 language 字段。
- 工具页不强制使用算法标签。

### 算法大类

| 标签                     | 中文   | 覆盖内容                                                         |
| ---------------------- | ---- | ------------------------------------------------------------ |
| greedy                 | 贪心   | 贪心策略、反悔贪心                                                    |
| data-structure         | 数据结构 | 栈、队列、堆、链表、并查集、树状数组、线段树、平衡树、ST 表、莫队、二分、二分答案、分治、整体二分、CDQ 分治、排序 |
| dp                     | 动态规划 | 线性 DP、背包、区间 DP、树形 DP、状压 DP、数位 DP、记忆化搜索                       |
| graph                  | 图论   | 最短路、最小生成树、拓扑、强连通/Tarjan、二分图、网络流、LCA、树上问题                     |
| number-theory          | 数论   | 素数、GCD/LCM、欧拉函数、同余、逆元、组合数学、博弈                                |
| string                 | 字符串  | 字符串哈希、KMP、AC 自动机、Manacher、后缀数组、字典树                           |
| computational-geometry | 计算几何 | 向量、凸包、半平面交、旋转卡壳、极角排序                                         |
| misc                   | 其他   | 模拟、高精度、位运算                                                   |

C++ 语法、函数、类、STL 等内容不属于上述算法大类，使用 language/ 和 type: language 管理。

### 精确标签

| 大类 | 精确标签 |
| --- | --- |
| greedy | greedy-strategy 贪心策略，regret-greedy 反悔贪心 |
| data-structure | stack 栈，queue 队列，heap 堆，linked-list 链表，dsu 并查集，fenwick 树状数组，segment-tree 线段树，balanced-tree 平衡树，sparse-table ST 表，mo-algorithm 莫队，binary-search 二分搜索，binary-search-answer 二分答案，divide-and-conquer 分治，parallel-binary-search 整体二分，cdq CDQ 分治，sorting 排序 |
| dp | linear-dp 线性 DP，knapsack 背包，interval-dp 区间 DP，tree-dp 树形 DP，bitmask-dp 状压 DP，digit-dp 数位 DP，memoization 记忆化搜索 |
| graph | shortest-path 最短路，mst 最小生成树，topological-sort 拓扑排序，tarjan 强连通/Tarjan，bipartite 二分图，network-flow 网络流，lca LCA，tree 树上问题 |
| number-theory | prime 素数，gcd-lcm GCD/LCM，euler-phi 欧拉函数，congruence 同余，inverse 逆元，combinatorics 组合数学，game-theory 博弈 |
| string | string-hash 字符串哈希，kmp KMP，ac-automaton AC 自动机，manacher Manacher，suffix-array 后缀数组，trie 字典树 |
| computational-geometry | vector-geo 向量，convex-hull 凸包，half-plane 半平面交，rotating-calipers 旋转卡壳，polar-sort 极角排序 |
| misc | simulation 模拟，bigint 高精度，bitwise 位运算 |

标签处理规则：

- 教练在 raw 笔记中用中文填写大类和精确知识点，例如“数据结构：二分搜索”。
- 米娅负责把中文映射为表中的英文标签，并生成对应的 tags-ch。
- 如果已有标签只有近似含义，必须先询问教练采用、删除还是保留哪个标签。
- 教练确认新增或替换标签后，先更新本表；迁移现有页面时同步替换旧标签；raw 原文保持不变。
- 英文标签由米娅根据教练确认的中文标准名补充，保持稳定、简洁、可检索。
- 不在教练确认前擅自把新精确标签写入正式页面。

## Raw 笔记分类写法

教练在 raw/notes/ 文件开头写分类信息，格式如下：

    数据结构：二分搜索

一份笔记涉及多个知识点时可以写多行：

    数据结构：二分搜索、二分答案

涉及多个大类时分别写行。C++ 语言笔记使用：

    C++：函数
    C++：类
    C++：STL

工具笔记使用：

    工具

分类信息用于决定页面类型和目录；精确标签仍按上面的标签确认规则处理。

## 文件与链接约定

- 从 raw 整理出的知识页和语言页，文件名与 raw 原文件名完全一致。
- 页面文件名不使用空格。
- 题目页文件名使用“平台-题号-题名”，例如 LeetCode-162-寻找峰值.md、洛谷-P4779-单源最短路.md。
- 使用 Obsidian 双链语法 `[[页面名]]` 做页面互链，例如 `[[二分搜索]]`。
- 每个页面必须在 index.md 的对应栏目登记。
- 每次修改 wiki 页面时更新 frontmatter 中的 updated 日期。
- 每次 wiki 内容操作追加到 log.md，记录日期、对象和动作。
- 来自 raw 的整理页在页面末尾用 ^[raw/notes/源文件] 标注来源。
- 检查 Markdown 源文本，而不只检查渲染后的显示效果：标题层级、YAML frontmatter、代码围栏、行内代码、数学公式和 Obsidian 双链都必须保持有效。
- 正文中可能被 Markdown 解析导致错误，要使用反斜杠转义。例如右移运算符的源码写成 `\>\>`。

## Frontmatter

### knowledge — 算法知识页

    ---
    title: Page Title
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    type: knowledge
    tags: [大类英文标签，精确英文标签]
    tags-ch: [大类中文标签，精确中文标签]
    sources: [raw/notes/源文件]
    confidence: high | medium | low
    ---

算法知识页的 tags 至少包含一个大类标签；精确标签按内容填写。

### language — C++ 语言笔记

    ---
    title: Page Title
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    type: language
    topic: function
    sources: [raw/notes/源文件]
    ---

语言页使用 topic 表示函数、类、STL 等主题，不填写 language 字段，也不填写 cpp-syntax、stl 等算法标签。

### problem — 题目页

    ---
    title: Platform ID Title
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    type: problem
    tags: [精确英文标签]
    tags-ch: [精确中文标签]
    sources: [raw/problems/源文件或raw/notes/源文件]
    difficulty: S | A | B | C | D
    source_url: <题目链接>
    confidence: high | medium | low
    ---

题目页的 tags 只能使用精确标签，不用大类标签。难度由米娅先评估；精确标签无法确定时先询问教练。

### tool — 工具页

    ---
    title: Page Title
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    type: tool
    sources: [raw/notes/源文件]
    ---

### student、comparison、query

    ---
    title: Page Title
    created: YYYY-MM-DD
    updated: YYYY-MM-DD
    type: student | comparison | query
    ---

学员数据只能由教练提供，不能虚构。

## 页面整理规则

### knowledge — 算法知识页

知识页采用“按 raw 笔记自适应”的教学结构：

- 保留原始笔记的主要小节和顺序。
- 核对每个主要小节的内容、推导、数字例子和特殊情况与 raw 是否一致；允许改写表达，不允许改变原意或丢失关键例外。
- 对含义不清的表达进行通俗化重写，补足必要的逻辑连接。
- 教练给出简略示例时，展开其中的过程、区间变化和结果；不主动添加新的示例。
- 保留并整理教练代码；只能修改注释、缩进和排版，不能改变代码逻辑。
- 代码存在疑似问题时，标记并向教练确认；确认前不写入未经确认的修正版。
- 可在原有框架内补充复杂度、常见坑、例题关联和知识点联动，但不强制每个小节具备同样的内容。
- 例题部分只列出教练提供的题目，并链接到 problems/ 中的独立题目页。
- 完成后复查 Markdown 源码，尤其是影响解析的符号，同时检查代码块和公式的边界。

### language — C++ 语言笔记

语言页也按 raw 笔记自适应整理：保留主要框架，由米娅重写表达、补足逻辑和展开教练给出的示例。代码处理规则与知识页相同。

### problem — 题目页

每道教练提供的题目独立成页，记录：

- 平台、题号、题名和来源链接；
- 题面；
- 涉及的精确知识点；
- S/A/B/C/D 难度及评估依据；
- 解题思路；
- 教练代码、作答情况和坑点；
- 关联的知识页。

只通过已提供的题目链接获取或补齐题面，不用网络搜索主动扩充题库。没有教练代码时标记“教练代码待补充”，不自行生成替代代码；代码有疑点时先标记并询问。

题目代码注释只标注算法范式、关键决策和边界原因，不注释循环递增、STL 调用、变量定义和 return 等显而易见的语句。代码逻辑仍以教练代码为准。

### tool — 工具页

对拍器、时间/空间估算、输入输出模板、调试技巧等工具单独成页。保留 raw 笔记的框架，由米娅重写和补充必要说明，不混入算法知识页。

## 素材投递箱

- raw/notes/：算法、C++ 语言和工具笔记原文。
- raw/problems/：教练提供的题目链接或题目材料。
- raw/assets/：图片和附件。

教练说“看看 raw/”或类似指令时：

1. 只扫描三个 raw 投递箱中的新文件。
2. 根据 raw 文件开头的分类信息决定页面类型和目录。
3. 逐个整理，跳过已经整理过的文件。
4. 不修改 raw 原文。
5. 整理完成后在回复中列出处理清单和需要教练确认的问题。

题目投递时只处理教练提供的题目；首选搜索或浏览已给出的链接来补齐题面，失败时说明缺失，不凭空编造题面或代码。

## 目录结构

    SCHEMA.md       # 本文件：结构、标签和整理规则
    index.md        # 主目录：算法、语言、题目和工具分栏
    log.md          # 追加式操作日志
    raw/            # 教练原始素材，只读
      notes/        #   算法、C++ 语言和工具笔记
      problems/     #   题目链接或题目材料
      assets/       #   图片/附件
    knowledge/      # ACM 算法知识页
    language/       # C++ 语言笔记
    problems/       # 出题池题目页
    tools/          # 实战工具页
    students/       # 学员档案（将来）
    comparisons/    # 对比页
    queries/        # 查询档案

## 更新与归档

- 内容冲突时以教练原意为优先；技术疑点标记并询问，不擅自取舍。
- 页面内容完全过时时移入 _archive/ 前必须得到教练确认。
- 出题池瘦身、删除或批量归档前必须得到教练确认。
