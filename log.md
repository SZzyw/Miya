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
