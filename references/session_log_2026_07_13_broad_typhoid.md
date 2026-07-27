# Session Log — 2026-07-13+07-17 — 广义伤寒分类系列 + tcm-proofreading 整合 (SESSION LEARNING RECORD)

> This file is **not** for skill loading. It records the 2026-07-13 and 2026-07-17 sessions that produced the broad_typhoid_* 5视角 series + strict 分层 reading guide + the tcm-proofreading v2.0/v2.1 GitHub repo consolidation, for debugging reproducibility of any future session that builds on this work.

## Sessions covered

- **2026-07-13 (上午)**: 广义伤寒分类系列 + 严格分层阅读指南 + 推送 ylindx-medical-cases
- **2026-07-17 (下午)**: zhangchi-tcm-mentor skill 安装 + 黄帝内经 037-045 校对(9 篇) + tcm-neijing-proofreading skill 固化 + tcm-proofreading 远端仓库合并整合 v2.0/v2.1

## 2026-07-17 工作的关键产出

### 1. zhangchi-tcm-mentor skill 安装 (https://github.com/erikgqp8645/zhangchi-tcm-mentor)
- 从 GitHub clone 到 `~/.hermes/skills/zhangchi-tcm-mentor/`
- 自包含 SKILL.md + references/(10.3 MB 课程数据,主要是 full_transcript.md)
- 触发词: 张驰中医课程、伤寒论/金匮要略/神农本草经/黄帝内经/伤寒明理论
- 配套「四维必录规则」(脉/舌/内经出处/原文要点)

### 2. deepseek-tcm-proofreading skill — 黄帝内经支持新增
- 原本 deepseek-tcm-proofreading 只支持伤寒论/神农本草经/金匮要略,没有黄帝内经
- 本次为黄帝内经 037-045 (9 篇讲稿) 增加了专门的 `references/prompt_neijing.txt`(6.5 KB)
- 增强了「5 条铁则 prompt」(无废话开场白、【原文】格式、字数铁则、错别字修复、自然分段)
- 新增 `scripts/proofread_neijing.py`(10.4 KB):curl 调用 API、max_tokens=384000、智能配置 fallback
- 9 篇实际校对:037-045,共 95,182 字符 → 88,801 字符,平均 -6.7%,耗时 1:36/篇

### 3. tcm-neijing-proofreading skill 固化 (新 skill)
- 把 `scripts/proofread_neijing.py` + `references/prompt_neijing.txt` 复制到独立的 `~/.hermes/skills/tcm-neijing-proofreading/`
- 加上 `config_template.json` + `README.md` + `case_2026_07_13.md`(实战日志)
- 由 hermes 在会话间隙自动生成 `references/batch_progress_monitoring.md` 和 `references/output_size_diagnosis.md`(工程经验沉淀)

### 4. tcm-proofreading 远端仓库合并整合 (https://github.com/erikgqp8645/tcm-proofreading)
- 远端原本是 2025-05 的 v1.0(只支持 1 门课程,prompts/ 被 gitignore)
- 本次合并本地+远端的内容,推 v2.0:
  - 4 门课程 prompt(伤寒论/黄帝内经/伤寒明理论/神农本草经)+ 各课程独立引用格式
  - 智能配置加载(config.json → config_template.json fallback + 占位符检测)
  - dry-run 默认 + --batch 实际执行
  - 范围批处理(--start N --end M)
  - 单文件处理(--single <file>)
  - 文件列举(--list)
  - macOS SSL 兼容(curl 调用,不依赖 Python requests)
  - .gitignore 改进(白名单 SKILL.md/case/batch/output_*.md)
- 17 files changed, 1079 insertions(+), 883 deletions(-)
- commit `bc5c482`
- 后续 v2.1 新增神农本草经(commit `1f806b7`):
  - 从 deepseek-tcm-proofreading 迁移 prompt_shennong.txt (4.7 KB) + case-shennong.md (2.5 KB)
  - 脚本 COURSE_PROMPTS 字典新增 'shennong': 'prompt_shennong.txt'
  - README + SKILL.md 全面更新为 4 门课程

### 5. README v2.0 → v2.1 升级
- 原始 README 5,146 字节
- v2.0 README 11,202 字节(2 倍信息密度):新增 v2.0 重大更新表、5 步快速开始、命令行完整参考、输出格式示例、工程设计亮点、版本历史
- v2.1 README 进一步增加神农本草经条目

## Erik 的关键偏好(从 7-17 工作观察到的)

### 透明度 > 优化

Erik 对「字数减少 -9.1%」的反应:**「你告诉我删掉的是什么内容」** + **「如果是无效的我还是能接受」**。

他不是要求 prompt 改进,而是要求**理解删除原因**。当被告知 037 文件 931 个单字行(`果`、`养`、`禾`)是语音识别 bug,他接受了 -9.1% 这个数字。

**Lesson**: 面对工程化结果的不满时,**先讲清楚做了什么(可透明化数据)**,而不是急着改进算法。这条信号已编入 deepseek-tcm-proofreading 的 `references/output_size_diagnosis.md`,并沉淀到 yilin-mentor-lineage 这里作为对所有同类任务的指导。

### 整合 vs 创建新文件

Erik 选择「**合并 + 整理 + 推送到远端覆盖**」,而不是「保留两个 skill」。

他明示:远端 erikgqp8645/tcm-proofreading 是「概念验证版」,本地 tcm-neijing-proofreading 是「生产实现版」,合并后保留本地版本作为基础 + 远端的 LICENSE/requirements.txt。**最终选择一个 GitHub repo 承载所有内容**,不分裂。

**Lesson**: 维护 GitHub repo 时,Erik 偏好**单仓库单 README** 的简洁结构,而不是多仓库分散。本次的成功模式:1 个 tcm-proofreading 仓库 + 1 个 SKILL.md 文件承载全部信息。这与之前 README 摘要卡的偏好一致 — 不要分裂到多文件。

### 实战经验自动沉淀 (hermes-agent 在后台做事)

本次会话中,hermes-agent 在后台自动创建了 3 份实战经验文档:
- `case_2026_07_13.md`(9 篇黄帝内经校对日志)
- `batch_progress_monitoring.md`(process.poll 的局限)
- `output_size_diagnosis.md`(字数减少诊断)

这些文档是 hermes-agent 在工作过程中自动生成的,**不在我的明确请求下**。Erik 的反应:接受并推送了它们。

**Lesson**: hermes 的「自动沉淀实战经验」机制是有效的,我应该信任它,不要尝试去「手动管理」这些文档,只负责触发性的任务(创建主 skill 文件、跑批量任务、推送)。

## 推送记录 (7-13 + 7-17 合并)

### ylindx-medical-cases (医林独啸斋广义伤寒系列)
- 提交 `de828db`: 广义伤寒分类四视角 + SKILL.md index
- 提交 `f9967ea`: 六经分卷阅读指南(162 KB) + README 重写为摘要卡
- 提交 `b1a0281`: Rewrite reading guide as strict layered version (核心+延伸)

### tcm-proofreading (中医讲稿校对通用工具)
- 提交 `bc5c482`: v2.0 整合三门课程(伤寒论/黄帝内经/伤寒明理论)+ 工程化升级
- 提交 `b84dcaa`: Update README to reflect v2.0 design
- 提交 `1f806b7`: v2.1 新增《神农本草经》支持

### zhangchi-tcm-mentor (课程问答 skill)
- 没有推送操作(本地安装即可)

## 未来会话需要后校验

- 黄帝内经 037-045 校对输出: `/Users/applemima1111/AiCoding/张弛老师讲稿/整理后/黄帝内经/`
- 重新跑批校对: `python3 scripts/tcm_proofreader.py --course neijing --start 16 --end 36 --batch`
  (35 讲未校对,可作为下一会话工作)
- 字数减少根因分析:**先讲清楚做了什么(可透明化数据)**,再问是否需要改进 prompt

## 重复提示(Erik 的反复要求)

Erik 在 7-17 会话末尾多次说「推送吧」、「1」、「2」、「3」,确认操作时坚持简短回应。

**Lesson**: Erik 的工作流节奏(**topic-bank 任务**):
- 用「继续/可以/开始/推送吧」做绿灯,不重新说明要求
- 每完成一步就停下等他确认,不要 preempt 后续步骤
- 「按 X 阅读」类请求需要:产出一份像分卷书目的结构化阅读指南,把每篇文章都映射到框架的对应位置(全量清单,不是精简版)