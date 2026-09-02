# Wiki Log

> Wiki 操作的追加式记录。
> 格式：`## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete

## [2026-08-16] create | Wiki initialized
- Domain: AI/ML 与大模型研究
- Structure created with SCHEMA.md, index.md, log.md
- Directories created: raw/articles, raw/papers, raw/transcripts, raw/assets, entities, concepts, comparisons, queries
## [2026-08-16] create | wiki structure rebuilt for ACM teaching
- SCHEMA.md rewritten (ACM 9-category taxonomy, S/A/B/C/D difficulty)
- Removed old template dirs: concepts, entities, raw/articles, raw/papers, raw/transcripts
- Created: knowledge/, problems/, tools/, students/, comparisons/, queries/, raw/problems/, raw/notes/, raw/assets/
## [2026-08-16] update | taxonomy: 二分/三分、分治归入 data-structure; greedy 精简为策略+反悔贪心; 页名允许中文
## [2026-08-16] update | taxonomy 两级化:题目页用精确标签;保险规则(归属不确定必须问教练)
## [2026-08-16] update | taxonomy 两级化:精确标签(problem 必用)+ 保险规则(归属不确定必须问教练)
## [2026-08-16] update | frontmatter 增加 tags-ch(中文标签,与 tags 英文标签一一对应)
## [2026-08-16] update | raw/ 投递箱机制:教练投放素材,米娅按指令扫描整理
## [2026-08-21] update | 新增代码注释规则(题目页专用):头部必注、决策点必注、边界坑点必注、禁止注释显而易见逻辑
## [2026-08-22] ingest | 整理 raw/notes/ 四份入门笔记
- 创建：knowledge/二进制与位运算.md
- 创建：knowledge/选择、冒泡、插入排序.md
- 创建：knowledge/二分搜索.md
- 创建：tools/对数器.md
- 更新：index.md（登记 4 页）
- ⚠️ 待确认：原笔记中的补码/负数示例、C++ 语法与类型名、二分峰值前提

## [2026-08-22] update | 二分搜索样例迁移
- 重写：knowledge/算法讲解006【入门】二分搜索.md（保留原始章节顺序，展开已有示例）
- 创建：problems/LeetCode-162-寻找峰值.md
- 更新：index.md（替换二分知识页链接，登记题目页）
- 更新：findRight 中点计算为 l + (r - l) / 2；其余教练代码逻辑保持不变
- raw 原文未修改

## [2026-08-22] update | 剩余入门笔记迁移
- 重写：knowledge/算法讲解003【入门】二进制和位运算.md
- 重写：knowledge/算法讲解004【入门】选择、冒泡、插入排序.md
- 重写：tools/算法讲解005【入门】对数器.md
- 创建：problems/洛谷-P1177-【模板】排序.md
- 更新：SCHEMA.md（新增 sorting / 排序精确标签）
- P1177 教练代码保留冒泡排序，并注明按题目规模超时是预期结果
- raw 原文未修改

## [2026-08-22] update | 整理规则增加语义与 Markdown 校验
- 更新：SCHEMA.md（要求主要章节内容、推导、数字例子和特殊情况与 raw 一致）
- 更新：SCHEMA.md、SOUL.md（增加 Markdown 源码检查和运算符转义规则）
- 更新：SCHEMA.md、SOUL.md（登记已确认的三个参考页面）
- raw 原文和知识页面未因本次规则更新而修改

## [2026-08-24] update | LeetCode-162-寻找峰值
- 重写：题目页解题思路，补充端点处理、二分方向、区间不变量和返回 `l` 的原因
- 新增：复杂度分析小节
- 调整：教练代码注释为适度详细，解释关键决策和边界前提，不改变代码逻辑
- raw 原文、SCHEMA.md、SOUL.md 未修改

## [2026-08-24] update | 同步代码注释与题目页写作规则
- 更新：SCHEMA.md，明确正文与代码注释的分工、题目页解题思路和复杂度分析要求
- 更新：Ubuntu `/root/.hermes/SOUL.md`，同步代码注释粒度及语言页、工具页适用范围
- 保持：代码逻辑、raw 原文、标签体系和工作区边界不变

## [2026-08-24] update | 重写算法讲解006【入门】二分搜索知识页
- 重写：knowledge/算法讲解006【入门】二分搜索.md，保留 raw 原文的五个主要章节和示例顺序
- 补充：各类二分的区间含义、方向判断、正确性依据和复杂度分析
- 调整：代码注释为适度详细，只解释局部实现、关键决策和边界原因
- ⚠️ 待教练确认：洛谷模板代码在 findLeft 返回 -1 时访问 arr[ans] 的越界风险
- raw 原文未修改

## [2026-08-24] update | 修正二分知识页例题归档
- 调整：knowledge/算法讲解006【入门】二分搜索.md，仅保留 P2249 例题简介和独立题目页双链
- 创建：problems/洛谷-P2249-【深基13.例1】查找.md，迁移题面、教练代码、复杂度和待确认问题
- 更新：index.md，登记 P2249 独立题目页
- raw 原文未修改

## [2026-08-25] update | 补充二分搜索复杂度分析
- 更新：knowledge/算法讲解006【入门】二分搜索.md，补充额外空间复杂度 O(1)
- 保持：例题链接后的特殊性说明不变

## [2026-08-25] update | 调整洛谷-P2249题目页
- 更新：problems/洛谷-P2249-【深基13.例1】查找.md，按教练说明移除无解分支的待确认风险
- 调整：将“坑点与待确认问题”改为“坑点”
- 保持：教练代码逻辑和题面内容不变

## [2026-08-27] update | 增加 Mermaid 图示规则
- 更新：SCHEMA.md，规定 Mermaid 按需使用、辅助正文且必须检查源文本
- 更新：Ubuntu `/root/.hermes/SOUL.md`，同步 Mermaid 使用与校验规则
- 保持：不强制页面使用 Mermaid，不以图示替代正文、推导、证明或代码

## [2026-09-01] ingest | 整理算法讲解007时间复杂度和空间复杂度
- 重写：tools/算法讲解007【入门】时间复杂度和空间复杂度.md，保留 raw 原文主要章节、数字例子、特殊情况和教练代码逻辑
- 更新：index.md（登记工具页，页面总数 8）
- raw 原文未修改；未扫描或修改 raw/notes/、raw/problems/、raw/assets/ 中的其他素材

## [2026-09-01] ingest | 整理算法讲解009单双链表
- 创建：knowledge/算法讲解009【入门】单双链表.md
- 创建：problems/洛谷-B3631-单向链表.md、problems/洛谷-B4324-【模板】双向链表.md
- 创建：problems/LeetCode-21-合并两个有序链表.md、problems/LeetCode-86-分隔链表.md
- 更新：index.md（登记 1 个知识页和 4 个题目页，页面总数 13）
- ⚠️ 待教练确认：B4324 教练代码中 `fin.resize` 后使用 `fin.push_back` 的编号映射风险
- raw 原文未修改

## [2026-09-01] update | 确认链表精确标签
- 更新：SCHEMA.md，确认 `linked-list / 链表` 为数据结构精确标签
- 更新：算法讲解009知识页和 4 个相关题目页，补充或替换为已确认标签
- raw 原文未修改

## [2026-09-01] update | 按教练反馈重排算法讲解009
- 更新：knowledge/算法讲解009【入门】单双链表.md，恢复 raw 原文的章节顺序和独立的两个“模板题”及“练习题”栏目
- 更新：4 个相关题目页，同步 raw 中最新的教练代码
- raw 原文未修改

## [2026-09-01] update | 按教练最新反馈同步算法讲解009
- 更新：knowledge/算法讲解009【入门】单双链表.md，按 raw 原有格式保留两个独立的“模板题”栏目，并保留新增的“时间复杂度”和“练习题”栏目
- 更新：4 个相关题目页，同步 raw 中最新代码
- raw 原文未修改

## [2026-09-01] update | 按 raw 框架调整算法讲解009
- 更新：knowledge/算法讲解009【入门】单双链表.md，使模板题紧跟对应的单链表插入、双链表插入内容之后，恢复 raw 的章节顺序和层级关系
- 调整：练习题统一放在时间复杂度之后；知识页只保留题目双链
- raw 原文未修改

## [2026-09-01] update | 重写算法讲解009单双链表知识页
- 重写：knowledge/算法讲解009【入门】单双链表.md，强化单链表/双链表的节点表示、连接变化、操作顺序、编号映射和边界约定
- 保留：raw 原文的主要章节、数字例子、模板题、练习题和教练代码逻辑；仅调整正文表达与代码注释
- 未修改：raw 原文及相关题目页
- ⚠️ 更正：此前记录的“B4324 教练代码中 `fin.resize` 后的编号映射风险”判断不准确。代码使用 `fin[y] = arr.size()` 直接按编号写入，没有 `push_back`；`resize` 本身不会造成映射错位。已在题目页改为说明默认值 0 与哨兵节点带来的有效性前提。

## [2026-09-01] ingest | 整理算法讲解020递归和 Master 公式
- 教练已修改 raw 原文，将补充式确认为 `T(n) = 2 * T(n/2) + O(nlogn)`，结论为 `O(n*log^2 n)`。
- 更新：knowledge/算法讲解020【必备】递归和master公式.md，移除该公式的待确认标记，同步确认后的公式和复杂度说明。
- raw 原文未由米娅修改。

## [2026-09-02] ingest | 整理算法讲解017二叉树及其三种序的递归实现
- 更新：SCHEMA.md，新增 `binary-tree / 二叉树` 精确标签，并将二叉树纳入图论大类覆盖范围
- 创建：knowledge/算法讲解017【入门】二叉树及其三种序的递归实现.md
- 创建：problems/洛谷-B3642-二叉树的遍历.md、problems/洛谷-P1030-【NOIP 2001 普及组】求先序排列.md、problems/洛谷-P1827-【USACO3.4】美国血统 American Heritage.md
- 更新：index.md（登记 1 个知识页和 3 个题目页，页面总数 18）
- 保留：raw 原文未修改；知识页只保留题目简介和独立题目页双链，题目页保留题面、解题思路、复杂度、教练代码、坑点和关联知识页
- 题面：根据教练提供的洛谷链接补齐 B3642、P1030、P1827 的必要题面信息
- raw 原文未修改

## [2026-09-02] update | 同步算法讲解017 raw 示例与日期
- 更新：knowledge/算法讲解017【入门】二叉树及其三种序的递归实现.md，补充 raw 新增的 7 个节点满二叉树节点关系和三种遍历结果
- 更新：knowledge/算法讲解017【入门】二叉树及其三种序的递归实现.md 的 `updated` 日期为 `2026-09-02`
- 核对：系统当前日期为 `2026-09-02`；本次日期记录与页面日期一致
- raw 原文未修改

## [2026-09-02] ingest | 整理算法讲解021归并排序
- 创建：knowledge/算法讲解021【必备】归并排序.md
- 更新：problems/洛谷-P1177-【模板】排序.md，补充归并排序解法并修正来源关联
- 更新：index.md（登记 1 个知识页；页面总数由 18 调整为 19）
- 保留：raw/notes/算法讲解021【必备】归并排序.md 未修改
- 重写：归并排序的递归划分、merge 合并过程、`6，4，2，3，9，4` 示例、步长为 `1，2，4，……` 的非递归思路及 P1177 模板题关联
- ⚠️ 待教练确认：完整教练代码的额外空间应计入 `help` 数组的 O(n)，raw 中“空间复杂度 O(log n)”是否仅指递归栈；原地归并排序的 O(n²) 是否特指某种具体实现
