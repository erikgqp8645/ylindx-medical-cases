# Session Log — 2026-07-10 — 方剂拆解工作流 (SESSION LEARNING RECORD)

> This file is **not** for skill loading. It records the 2026-07-10 session that produced the「方剂拆解分析」Sub-Workflow + 3 个真实拆方实例 + GitHub push, for future sessions that need to reproduce or extend this work.

## What was produced

### 1. 三个真实拆方实例(同会话内连续请求)

用户连续 3 次贴出处方,要求「拆解」,全部走 Sub-Workflow 处理:

| # | 处方 | 核心方 | 病机 |
|---|---|---|---|
| 1 | 花椒3 黑顺片6 苦杏仁10 石菖蒲10 细辛3 冬花10 紫菀10 干姜10 桂枝10 麻黄6 茯苓30(11 味) | **理饮汤化裁 + 麻黄附子细辛汤** | 寒饮停肺 + 阳虚外感 |
| 2 | 柴胡10 玄参10 当归10 浙贝10 防风10 鸡内金10 槟榔15 石菖蒲20 僵蚕10 蝉蜕10 片姜黄6 苦杏仁10 紫菀20 枇杷叶10 厚朴10 枳实10 薏苡仁30 白豆蔻10(19 味) | **升降散 + 三仁汤核心 + 消瘰丸核心 + 达原饮变方** | 气郁 + 湿浊 + 痰结 |
| 3 | 柴胡15 黄芩10 法半夏10 党参10 甘草6 苍术15 桂枝10 泽泻30 猪苓10 茯苓30 麻黄6 薏苡仁60 苦杏仁10(14 味) | **柴苓汤 + 麻杏苡甘汤** | 少阳不利 + 湿浊内停 + 表寒外束 |

3 次都走完整 9 步流水线,每次结尾问「有具体主诉可以精修推论吗?」——Erik 全部绿灯确认通过,没纠错。

### 2. Sub-Workflow 整合到 SKILL.md

Erik 的明确偏好: **「把这个拆解方剂的流程或者工作流合并到医林独秀斋的这个skill里面,然后推送到github」**

→ **不要**单独建 `references/fang_jie_workflow.md`(我第一次错了,创建了独立文件)
→ 修正:把工作流合并进 SKILL.md 的「Sub-Workflow: 方剂拆解分析」节
→ 删除独立文件,避免双份维护

### 3. 4 个 references/ 文件新增(在本次会话前后)

| 文件 | 大小 | 主题 |
|---|---|---|
| `eye_red_eye_disease.md` | 14.8 KB | 眼红三分法(肝胆郁热/水毒侵犯/燥热瘀血) |
| `shingles_herpes_zoster.md` | 18.2 KB | 带状疱疹(瓜蒌红花汤+升麻鳖甲汤+真武汤三大支柱) |
| (独立) `fang_jie_workflow.md` | 9.5 KB | **已删除**——合并进 SKILL.md |

### 4. GitHub 推送

- repo: `https://github.com/erikgqp8645/ylindx-medical-cases`
- 分支: `master`(不是 main)
- commit: `4906628` — "Expand Sub-Workflow: 方剂拆解分析 (fang-jie)"
- diff: 1 file changed, 236 insertions(+), 2 deletions(-)
- 验证:upstream SKILL.md size = 62589 bytes(本地一致)

## Erik 的关键纠错(已编入 SKILL.md)

### 纠错 1:「独立文件 vs 合并到 SKILL.md」

**我错的地方**:第一次创建了 `references/fang_jie_workflow.md` 独立文件,准备推送。

**Erik 实际要的**:把工作流**合并到 SKILL.md 内部**,作为 Sub-Workflow 节。

**Lesson**:
- 方法论/工作流本身 → 合并进 SKILL.md
- 内容文件(如某方剂专题)→ 才放 `references/<topic>.md`

→ 已编码进 SKILL.md 「Sub-Workflow: 方剂拆解分析」节的开头(「保存形式选择」)+ 「Step 9」(decision point)+ 「黄金原则」第 6 条

### 纠错 2:Trigger 词与工作流未一一对应

**我错的地方**:原 Trigger 词表把「这个方子 / 方子构成 / 任意药物列表」指向 Reverse-Lookup Workflow,实际应该指向 Sub-Workflow: 方剂拆解分析。

**Erik 实际要的**:两个工作流必须分清,Trigger 词必须一一对应:
- 方剂输入 → **Sub-Workflow: 方剂拆解分析**(本节)
- 症状输入 → Reverse-Lookup

→ 已修复 Trigger Vocabulary 表,新增「拆解这个方子」「这个方是什么思路」触发词,明确指向 Sub-Workflow

→ 已编码进 SKILL.md 「黄金原则」第 7 条

## 推送记录

- `827d8be..4906628  master -> master` (2026-07-10)
- 仅推送 SKILL.md(1 file, 236 insertions)
- 没推 references/ 下的眼红/带疱专题文件(那些是上一轮工作,在更早的 commit 里)

## 未来会话的复现要点

如果未来要扩展示例库:
- 拆方输出应**保留 ASCII 框图**,不要把框图转成 mermaid(CLI 不可读)
- 逐药回溯表必须有「来源」+「剂量」+「角色」三列
- 结尾必须问「有具体主诉可以精修推论吗?」——这是 Erik 硬性偏好
- 引证带 line number 是 Skill-wide 规则,不只是拆方

## 重复模式(Erik 反复的工作流节奏)

Erik 在 yilin-mentor-lineage 任务里反复表现:
- 一次性给多个相关请求(本会话 3 个拆方 + 1 个推送要求)
- 偏好「合并整理」而不是「分散多文件」
- 对 prompt 改进要求不急,但对「工作流清晰度」「可重复性」很在意
- 「拆方/方子构成/方子思路」类请求,必须能稳定给出结构化报告,而不是模糊分析
