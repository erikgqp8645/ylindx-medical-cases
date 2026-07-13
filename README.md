# 医林独啸斋 · 经方医案知识库

> **5 分钟目录摘要卡** · 456 篇医案 · 23 个专题文件 · 5 个跨视角分类

A source-grounded TCM course pack from the WeChat public account 医林独啸斋 (tsp南极), packaged for the [lineage-skill](https://github.com/JuneYaooo/lineage-skill) course Skill framework. Used as the `yilin-mentor-lineage` Skill inside Hermes Agent.

---

## 项目简介

**医林独啸斋** 是 tsp南极(一位中医经方实战家)在微信公众号运营的中医课程。本仓库将 456 篇 markdown 医案 + 课程全文转化为 **可检索、可推理、可学习** 的结构化知识库,作为 **Hermes Agent** 的 `yilin-mentor-lineage` Skill 使用,辅助学习中医经方、温病、辨证论治,以及临床实战。

**核心特色:寒温一统,不拘门派。** 课程里既讲伤寒经方(桂枝汤、麻黄汤、真武汤、潜阳丹),也讲温病时方(银翘散、三仁汤、升降散、安宫牛黄);既覆盖外感热病,又延伸至内伤杂病(郁热、瘀血、湿热、阴火);既有经典方证体系,也有赵绍琴、胡天雄、曾荣修、李兴云等名家的临证经验。

---

## 数据规模

| 维度 | 数量 |
|---|---|
| 医案总数 | **456 篇** markdown |
| 课程全文语料 | ~9.5 MB(`references/full_transcript.md`) |
| 结构化课程包 | ~9.9 MB(`references/course_package.json`) |
| 课程摘要 | ~60 KB(`references/course_digest.md`) |
| 专题知识库 | **23 个 .md 专题文件**(总 ~280 KB) |
| 触发词条 | 30+ 短语(中英文混合,见 SKILL.md Trigger Vocabulary) |
| 主题覆盖 | 外感热病、内伤杂病、皮肤疮疡、肿瘤、儿科、妇科、五官、疼痛 |

---

## 仓库结构

```
yilin-mentor-lineage/
├── README.md                                # 本文件(5 分钟目录摘要卡)
├── SKILL.md                                 # Skill 定义(给 AI 助手读,33 KB)
├── lineage_manifest.json                    # 课程包元信息
├── agents/                                  # Skill 角色定义
├── references/                              # 核心知识库(23 个专题)
│   ├── full_transcript.md                   #   - 课程全文 ~9.5 MB
│   ├── course_package.json                  #   - 结构化数据 ~9.9 MB
│   ├── course_digest.md                     #   - 课程摘要
│   ├── lesson_index.json                    #   - 课程索引
│   ├── concept_glossary.md                  #   - 概念词典
│   ├── stagnant_heat_yure.md                # ⭐ 郁热专题(赵绍琴理法)
│   ├── sheng_jiang_san_variants.md          # ⭐ 升降散 29 种变法
│   ├── sanren_tang_formula.md               # ⭐ 三仁汤专题
│   ├── damp_heat_three_formulas.md          # ⭐ 湿热三方对比
│   ├── cold_damp_vs_damp_heat.md            # ⭐ 寒湿 vs 湿热 鉴别
│   ├── gardenia_fermented_soybean_formula.md  # ⭐ 栀子豉汤专题
│   ├── blood_stasis_formulas.md             # ⭐ 瘀血专题(10 方剂、69 篇)
│   ├── broad_typhoid_nine_grid.md           # 🆕 广义伤寒·视角 3·寒温一统九宫格
│   ├── broad_typhoid_five_categories.md     # 🆕 广义伤寒·视角 1·《难经》五分类
│   ├── broad_typhoid_six_channels.md        # 🆕 广义伤寒·视角 2·六经传变轴
│   ├── broad_typhoid_overview.md            # 🆕 广义伤寒·全景索引(三视角交叉)
│   ├── broad_typhoid_reading_guide.md        # 🆕 六经分卷阅读指南(429 篇)
│   └── conversion_workflow.md               # 转换工作流(开发者参考)
└── scripts/                                 # 数据处理脚本
```

---

## 专题知识库索引(23 个)

### ⭐ 病机与方剂专题(老专题,2026-06 立项)

| 专题 | 文件 | 覆盖 | 核心内容 |
|---|---|---|---|
| **郁热 / 火郁** | `references/stagnant_heat_yure.md` | 146 篇 | 赵绍琴理法、宣透郁热、透热转气 |
| **升降散变法** | `references/sheng_jiang_san_variants.md` | 29 种 | 姜黄/大黄/僵蚕 替换、合方升级、决策树 |
| **三仁汤** | `references/sanren_tang_formula.md` | 231 处 | 分消湿热、宣上畅中渗下、三禁 |
| **湿热三方对比** | `references/damp_heat_three_formulas.md` | — | 三仁 vs 甘露消毒 vs 藿朴夏苓 |
| **寒湿 vs 湿热** | `references/cold_damp_vs_damp_heat.md` | — | 5 步速判、3 大陷阱、病机转化 |
| **栀子豉汤** | `references/gardenia_fermented_soybean_formula.md` | 18 篇 | 表里双解体系 |
| **瘀血专题** | `references/blood_stasis_formulas.md` | 69 篇 | 10 方剂系统、桃核承气系列 |

### 🆕 广义伤寒分类五文件(2026-07 立项,五视角)

| 视角 | 文件 | 角色 | 内容 |
|---|---|---|---|
| **视角 3**(先做) | `references/broad_typhoid_nine_grid.md` | 临床综合 | 表/半/里 × 寒/热/湿 = 9 格 + 9 类跨格专题 |
| **视角 1** | `references/broad_typhoid_five_categories.md` | 经典理论 | 《难经》五分类(中风/伤寒/湿温/热病/温病)+ 卫气营血对接 |
| **视角 2** | `references/broad_typhoid_six_channels.md` | 传变轴 | 太阳→阳明→少阳→太阴→少阴→厥阴,7 类传变路径 |
| **全景索引** | `references/broad_typhoid_overview.md` | 跨视角交叉 | 15 个跨视角锚点医案 + 临床三步实战模板 |
| **阅读指南** | `references/broad_typhoid_reading_guide.md` | 实战路径 | 429 篇医案按六经分卷+附卷,三档阅读路线 |

每个专题文件都包含:
- 病机/方证图示(ASCII 框图)
- 关键金句(直接引证 + 行号定位)
- 速查表(舌/脉/症状)
- 临床决策流程图
- 医案/案例索引(带 ★ 优先级)
- 一句话核心心法

---

## 快速开始

### 作为 Hermes Agent Skill 使用

```bash
git clone https://github.com/erikgqp8645/ylindx-medical-cases.git \
  ~/.hermes/skills/yilin-mentor-lineage
```

之后,在对话中使用以下触发词,Skill 会自动加载对应文件并提供带原文出处的精准回答:

- 「三仁汤」 → 加载 `sanren_tang_formula.md`
- 「郁热」 / 「升降散」 → 加载 `stagnant_heat_yure.md` + `sheng_jiang_san_variants.md`
- 「广义伤寒」 / 「九宫格」 → 加载 `broad_typhoid_nine_grid.md`
- 「六经辨证」 → 加载 `broad_typhoid_six_channels.md`
- 「按六经阅读」 → 加载 `broad_typhoid_reading_guide.md`
- 「这个方子」 / 任意药物列表 → 运行 Reverse-Lookup Workflow

### 命令行检索

```bash
# 搜索关键词在课程全文中的位置
rg -n "升降散" references/full_transcript.md

# 跨专题关联
rg -n "三仁汤.*湿温|湿温.*三仁汤" references/

# 查看某个专题的全部内容
less references/sheng_jiang_san_variants.md
```

---

## 按六经体系阅读(推荐路径)

如果你想系统地读这份课程,**最推荐的方式是按六经分卷阅读**——把 429 篇医案按《伤寒论》六经架构组织:

```
卷一·太阳病(126 篇) → 卷二·阳明病(25 篇) → 卷三·少阳病(166 篇)
       ↓
卷四·太阴病(14 篇) → 卷五·少阴病(82 篇) → 卷六·厥阴病(17 篇)
       ↓
附卷一·合病并病(55 篇) / 附卷二·直中三阴(16 篇) / 附卷三·坏病救逆(87 篇)
```

详细分卷指南见 `references/broad_typhoid_reading_guide.md`。

---

## 数据生成

本仓库基于 [lineage-skill](https://github.com/JuneYaooo/lineage-skill) 课程包构建工具生成,所有数据均来自 tsp南极 的微信公众号文章:

```bash
git clone https://github.com/JuneYaooo/lineage-skill
cd lineage-skill
python scripts/build_course_skill.py \
  --source-dir /path/to/医林独啸斋/markdown \
  --output-dir /path/to/yilin-mentor-lineage
```

详细的转换工作流见 `references/conversion_workflow.md`。

---

## 内容来源

- **作者**: tsp南极(微信公众号「医林独啸斋」主理人)
- **来源**: 微信公众号 医林独啸斋(https://mp.weixin.qq.com/mp/homepage?__biz=MzkzNTM0Mzk3OA==)
- **原始语料**: 456 篇 markdown 医案
- **本地化时间**: 2026 年 7 月
- **维护者**: [erikgqp8645](https://github.com/erikgqp8645)

---

## 引用与版权

本仓库仅供 **学习、研究、教学** 使用,所有内容著作权归原作者 tsp南极 所有。

引用本仓库请注明:

```
数据来源:微信公众号 医林独啸斋(tsp南极)
GitHub: https://github.com/erikgqp8645/ylindx-medical-cases
```

---

## 免责声明

⚠️ **本仓库内容仅供学习者参考,非专业人士请勿自行使用。所有应用决策应由专业人员面诊/审慎评估后做出。**

本文档中的所有方法、剂量、案例分析均来自原作者的学术整理,仅供参考,不应被视为标准建议。

---

## 相关项目

- [Hermes Agent](https://hermes-agent.nousresearch.com/docs) - 通用 AI Agent 框架
- [lineage-skill](https://github.com/JuneYaooo/lineage-skill) - 课程包构建工具

---

## 贡献

本仓库为 **只读镜像**。如需:
- 修正错误 → 提交 Issue
- 增加专题 → 在 Hermes 端 `references/` 中新建,作者本人会定期同步
- 改进 Skill → 修改 `SKILL.md`,提交 PR

## 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

> **一句话核心心法**:
> 「寒温一统,辨证论治,见病知源。」

---

## README 写作要点(给未来的 agent 留的笔记)

基于 2026-07-13 README 与目录摘要卡合并经验:

1. **顺序固定**: 项目简介 → 数据规模 → 仓库结构 → 专题索引 → 快速开始 → 数据生成 → 内容来源 → 引用版权 → 免责声明 → 相关项目 → 贡献 → 许可证 → 一句话核心心法
2. **双语并排**: 中文段落用 `**粗体**` 强调,英文段落 1-2 句即可
3. **数据规模表必须有**: Erik 用具体数字(456 篇、9.5MB 等)判断项目完整性
4. **专题索引要列全部**: 不再用省略号,新增的也全部列
5. **「⭐」/「🆕」标记**: ⭐ = 核心专题,🆕 = 新增专题,视觉上区分基础数据
6. **触发词清单不可省**: 体现 Skill 的「快速加载」能力
7. **免责声明不可省**: 涉及医案的都要写
8. **结尾一句话心法**: 用「」包起来,这是 Erik 偏好的收束风格
9. **不要用 emoji 作为标题前缀**: 标题保持纯文本,emoji 只在表格或强调用
10. **README 可承载目录摘要卡**: 当 Erik 要求「5 分钟摘要」时,直接做成完整 README,而不是另起文件,保持仓库结构简洁