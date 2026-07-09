# 医林独啸斋 中医医案精华

> 456 例临床真实病案 · tsp 南极 · 经方思维的系统整理

A curated knowledge base of 456 real-world Traditional Chinese Medicine (TCM) clinical cases by tsp南极, packaged for the [lineage-skill](https://github.com/JuneYaooo/lineage-skill) course Skill framework.

---

## 项目简介

**医林独啸斋** 是中医师 tsp南极 创办的公众号,作者用 **经方思维** 系统整理了 456 例真实临床医案,涵盖内科、外科、妇科、儿科、皮肤科、骨科等各科疾病,以及经方、时方、汉唐古方在各病种中的应用。

本仓库将医林独啸斋全部 456 篇文章转化为 **可检索、可推理、可学习** 的结构化知识库,作为 **Hermes Agent** 的 `ylindx-medical-cases` Skill 使用,辅助学习、复习与临床辨证。

## 数据规模

| 维度 | 数量 |
|---|---|
| 医案总数 | **456 篇** |
| 涉及方剂 | 数百首(以经方为主) |
| 涉及病种 | 内科、外科、妇科、儿科、皮肤、骨科等 |
| 全文检索语料 | ~6.5 MB( `references/full_transcript.md` ) |
| 病例结构化数据 | ~1 MB( `references/course_package.json` ) |
| 课程摘要 | ~1 MB( `references/course_digest.md` ) |

## 仓库结构

```
ylindx-medical-cases/
├── README.md                                # 本文件
├── SKILL.md                                 # Skill 定义(给 AI 助手读)
├── lineage_manifest.json                    # 课程包元信息
├── agents/                                  # Skill 角色定义
├── references/                              # 核心知识库(全部为可检索数据)
│   ├── full_transcript.md                   #   - 456 篇文章全文
│   ├── course_digest.md                     #   - 课程摘要
│   ├── course_package.json                  #   - 结构化病例数据
│   ├── lesson_index.json                    #   - 课程索引
│   ├── concept_glossary.md                  #   - 概念词典
│   ├── quote_index.md                       #   - 经典引文索引
│   ├── evidence_map.json                    #   - 证据来源映射
│   ├── study_paths.md                       #   - 学习路径
│   ├── mentor_playbook.md                   #   - 导师话术
│   ├── mentor_sessions.md                   #   - 复盘记录
│   ├── learner_progress.json                #   - 学习进度
│   ├── playbooks.md                         #   - 玩法
│   ├── checklists.md                        #   - 检查清单
│   ├── templates.md                         #   - 模板
│   ├── case_index.json                      #   - 病例索引
│   │
│   ├── blood_stasis_formulas.md             # ⭐ 瘀血专题
│   ├── damp_heat_three_formulas.md          # ⭐ 湿热三方对比
│   ├── cold_damp_vs_damp_heat.md            # ⭐ 寒湿 vs 湿热 鉴别
│   ├── gardenia_fermented_soybean_formula.md# ⭐ 栀子豉汤专题
│   ├── sanren_tang_formula.md               # ⭐ 三仁汤专题
│   ├── stagnant_heat_yure.md                # ⭐ 郁热/升降散专题
│   └── conversion_workflow.md               # 转换工作流(开发者参考)
└── scripts/                                 # 数据处理脚本
```

## 专题知识库(Pre-built Topic Banks)

本仓库最重要的资产是 **6 个深度专题知识库**,每个都从 456 篇文章中提取、整理、对比、形成体系:

| 专题 | 文件 | 文章覆盖 | 核心内容 |
|---|---|---|---|
| **瘀血/淤血专题** | `references/blood_stasis_formulas.md` | 69 篇 | 10 首方剂、诊断指征、配伍规律、典型医案 |
| **郁热/火郁专题** | `references/stagnant_heat_yure.md` | 146 篇 | 赵绍琴理法,升降散+栀子豉汤+三仁汤架构 |
| **栀子豉汤专题** | `references/gardenia_fermented_soybean_formula.md` | 18 篇 | 「表里双解体系」重新定义 |
| **三仁汤专题** | `references/sanren_tang_formula.md` | 231 处 | 分消三焦湿热,8 大合方体系,三禁要旨 |
| **湿热三方对比** | `references/damp_heat_three_formulas.md` | — | 三仁汤 vs 甘露消毒丹 vs 藿朴夏苓汤 |
| **寒湿 vs 湿热** | `references/cold_damp_vs_damp_heat.md` | — | 临床鉴别,湿热假寒三大陷阱,5 步速判法 |

每个专题文件都包含:
- 病机图示(ASCII 框图)
- 关键金句(直接引证 + 行号定位)
- 舌象/脉象速查表
- 临床决策流程图
- 医案索引(带行号)
- 一句话核心心法

## 快速开始

### 作为 Hermes Agent Skill 使用

将本仓库作为 Skill 安装到 `~/.hermes/skills/ylindx-medical-cases/`,然后在对话中触发:

```bash
git clone https://github.com/erikgqp8645/ylindx-medical-cases.git \
  ~/.hermes/skills/ylindx-medical-cases
```

之后,你可以问:

- "医林独啸斋 三仁汤"
- "湿热病机专题"
- "寒湿和湿热怎么鉴别"
- "瘀血专题"
- "升降散治什么"
- "栀子豉汤到底是涌吐剂还是表里双解"

Hermes Agent 会自动加载对应的专题文件,提供带原文出处的精准回答。

### 作为命令行工具检索

`scripts/` 目录提供数据处理脚本,可直接对 `full_transcript.md` 做全文搜索:

```bash
# 搜索「三仁汤」所有出现位置
rg -n "三仁汤" references/full_transcript.md

# 搜索「升降散」合方
rg -n "升降散.*合方" references/full_transcript.md
```

## 数据生成

本仓库基于 [lineage-skill](https://github.com/JuneYaooo/lineage-skill) 课程包构建工具生成:

```bash
git clone https://github.com/JuneYaooo/lineage-skill
cd lineage-skill
python scripts/build_course_skill.py \
  --source-dir /path/to/医林独啸斋/markdown \
  --output-dir /path/to/ylindx-medical-cases
```

详细的转换工作流见 `references/conversion_workflow.md`。

## 内容来源

- **作者**: tsp南极(医林独啸斋创办人)
- **公众号**: 医林独啸斋
- **原始语料**: 456 篇公众号文章
- **本地化时间**: 2026 年 6 月
- **维护者**: [erikgqp8645](https://github.com/erikgqp8645)

## 引用与版权

本仓库仅供 **学习、研究、教学** 使用,所有医案著作权归原作者 tsp南极 所有。

引用本仓库请注明:

```
数据来源:医林独啸斋(tsp南极)中医医案精华
GitHub: https://github.com/erikgqp8645/ylindx-medical-cases
```

## 免责声明

⚠️ **本仓库内容仅供中医学习者参考,非专业医生请勿自行试药。所有医疗决策应由专业中医师面诊后做出。**

本文档中的所有方剂、剂量、医案分析均来自原作者 tsp南极 的临床经验与学术整理,仅供参考,不应被视为标准医疗建议。

## 相关项目

- [Hermes Agent](https://hermes-agent.nousresearch.com/docs) - 通用 AI Agent 框架
- [lineage-skill](https://github.com/JuneYaooo/lineage-skill) - 课程包构建工具
- [JuneYaooo/lineage-skill](https://github.com/JuneYaooo/lineage-skill) - 原始课程生成器

## 贡献

本仓库为 **只读镜像**。如需:
- 修正错误 → 提交 Issue
- 增加专题 → 在 Hermes 端 `references/` 中新建,作者本人会定期同步
- 改进 Skill → 修改 `SKILL.md`,提交 PR

## 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

> **一句话核心心法**:
> 「医林独啸斋 456 篇文章,以经方思维贯穿始终,核心治法可总结为六字——**分消走泄、三焦同治**。」

