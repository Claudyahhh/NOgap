# NOgap — AI 求职成长助手

> 基于 [career-ops](https://github.com/santifer/career-ops) 改造的个人 AI 求职工具。
> 面向零正职工作经验的年轻人，帮助和陪伴他们消除与理想工作之间的 gap。

---

## 这是什么

NOgap 是一个跑在本地、由 Claude Code 驱动的 AI 求职成长系统。它面向零正职工作经验的年轻人，通过持续评估、行动和复盘，帮助和陪伴他们消除与理想工作之间的 gap。你把 JD 粘贴进来，它会陪你完成六件事：

1. **评估这个岗位** — 匹配度分析 + 评分，给出"值不值得投"的判断
2. **改写你的简历** — 针对这个 JD 逐条定制，每条改写有原文溯源
3. **分析能力缺口** — 告诉你真正缺什么、怎么补，直接找到最好的教程
4. **准备面试** — 公司实时调研 + 针对你的个性化问题预测 + STAR 故事拆解
5. **生成展示材料** — 100 字口播自我介绍 + 可共享屏幕的 HTML 展示网页
6. **复盘每次面试** — 五维度诊断，发现的新缺口自动回流进下次分析

每一步的输出都存成文件，按 JD 编号对齐，可以随时回头查。

**这不是批量投递工具。** 评分低于 3.5/5，系统会明确建议不投。精准投 5 家，比无差别投 50 家更值得。

---

## 先决条件

| 工具 | 用途 | 获取 |
|------|------|------|
| **Claude Code** | 系统运行的宿主环境 | [claude.ai/code](https://claude.ai/code) |
| **Anthropic 账号** | Claude Code 需要（Pro / Max 订阅或 API key） | [anthropic.com](https://anthropic.com) |
| **Git** | 克隆仓库 | 系统自带或 [git-scm.com](https://git-scm.com) |
| **Node.js ≥ 18** | 系统更新检查脚本 | [nodejs.org](https://nodejs.org) |

> Claude Code 目前支持 macOS / Linux / Windows（WSL）。

---

## 安装

```bash
# 1. 克隆仓库到本地
git clone https://github.com/Claudyahhh/NOgap.git
cd NOgap

# 2. 安装依赖（仅系统更新检查脚本需要）
npm install

# 3. 在 Claude Code 中打开这个目录
claude
```

Claude Code 启动后会自动识别 `.agents/skills/nogap/SKILL.md`，`/nogap` 命令随即可用。

---

## 初始化（第一次使用）

**你不需要手动配置任何文件。** 第一次启动后，直接在 Claude Code 里说任何话，系统会自动检测缺失的文件并引导你完成初始化。整个过程是对话式的：

---

### 第一步：录入简历

系统检测到 `cv.md` 不存在时，会问你：

```
还没有你的简历。你可以：
1. 直接粘贴简历（Word / PDF 复制出来的文字都行），我来转成 Markdown
2. 告诉我你的经历，我来帮你起草

选哪种？
```

**两种方式都可以。** 最终 `cv.md` 是你在整个系统里唯一的简历事实源——所有改写都基于这里的内容，任何时候都可以更新它。

> `cv.md` 的格式没有严格要求，按经历时间线组织即可。系统会实时读取，不做缓存。

---

### 第二步：填写基本偏好

系统会把 `config/profile.example.yml` 复制成 `config/profile.yml`，然后问你几个问题：

```
需要几个信息来个性化系统：
- 你的姓名和邮箱
- 目标岗位类型（如：AI 产品经理实习、AI 战略实习）
- 求职阶段（实习 / 校招 / 社招）
- 偏好城市
```

填完后 `config/profile.yml` 会写入你提供的信息。这个文件控制评估时的权重和优先级。你随时可以改它，比如求职阶段从实习升级到校招、换目标城市等。

---

### 第三步：系统了解你

基础文件就绪后，系统会主动问几个问题来提升后续所有输出的质量：

```
产出质量取决于我对你了解的深度，能告诉我：
- 你最突出的优势是什么？别人没有但你有的？
- 什么样的工作让你有能量？什么让你觉得没意思？
- 有没有硬性拒绝条件？（如不考虑非北上广、不去外企等）
- 最拿得出手的一段经历是什么？
```

你的回答会被写入 `modes/_profile.md`（你的个人策略文件）。这个文件越丰富，评估和改写就越个性化。

---

### 完成

```
已就绪。直接粘贴 JD 开始评估，或用 /nogap 查看所有命令。
```

---

## 日常使用

### 最简单的方式

在 Claude Code 里，**直接粘贴一段 JD 文本**，系统自动识别并启动评估。

### 显式调用

```
/nogap              → 查看所有命令和当前状态
/nogap brief        → 粘贴 JD，开始岗位评估
/nogap cv-tailor    → 针对 JD 改写简历
/nogap gap-roadmap  → 分析能力缺口
/nogap interview-prep     → 面试前备战
/nogap interview-strategy → 面试现场展示方案
/nogap interview-review   → 面试后复盘
```

### 指定 JD 编号

每个 JD 首次进入系统时会分配三位数编号（从 `000` 开始）。对同一个 JD 运行后续 mode 时，用编号告诉系统哪个 JD：

```
/nogap cv-tailor #000
/nogap gap-roadmap #000
/nogap interview-prep #000
```

---

## 六个 Mode 详解

### `brief` — 岗位快速评估

粘贴 JD 后，输出两个模块：

- **A 模块 — 岗位概览：** 岗位类型（archetype）、职级、远程政策、一句话概括
- **B 模块 — 与简历的匹配度：** JD 每条要求 → 映射到你简历里的具体内容；差距逐条分析（是硬门槛还是加分项？有没有替代经历？具体怎么应对？）

评分 1-5 分。低于 3.5 明确建议不投。

评估完成后，结论（archetype、人才画像、gap 列表、评分）会写入 `JDlist/{###}.md`，供后续所有 mode 直接读取，不重复分析 JD。

---

### `cv-tailor` — 简历定制改写

针对目标 JD，从职业规划师视角改写你的全部经历，分四个部分：

- **定级分析：** 你和 JD 要求的职级差距在哪？如何用"成长型"叙事切入？
- **JD 人才画像：** 这个岗位真正想要什么样的人，差异化机会窗口在哪
- **经历分类：** 每段经历标注"直接相关 / 间接相关 / 背景性重要"
- **逐条改写：** 全部经历改写，每条附原文出处（事实依据安全锁）

**改写边界：** 可以换角度、植入 JD 关键词、建立可迁移联系；不能编造数字、项目、合作方。面试官追问"能详细说说吗"，你必须能完整回答。

---

### `gap-roadmap` — 能力缺口四象限

诚实指出简历改写遮盖不住的真实能力缺口，并给出可执行的补齐方案。

**四象限：**

| | 补齐成本：低 | 补齐成本：高 |
|--|------------|------------|
| **影响度：高** | 🔥 立刻做（投递前完成） | 📅 规划长线（启动但不急） |
| **影响度：低** | 🆓 顺手做 | ❌ 暂时忽略 |

每条 🔥 和 📅 行动附带 **WebSearch 实时找到的最佳教程**（B 站播放量、GitHub stars、权威频道），直接给链接，不让你自己找。

---

### `interview-prep` — 面试前备战

面试前运行，生成四个模块：

1. **公司调研速读卡：** WebSearch 实时搜索公司现状、所在业务线、面试风格、近期负面信号（5-8 条，每条标来源）
2. **问题预测（四板块）：** 行业底层认知、行业趋势发展、个人技能边界、项目实操决策——每道题说明"面试官为什么问这题""答好了证明什么"
3. **P0-P2 备考清单：** 面试前必须完成的具体行动，带步骤和预估耗时
4. **STAR 拆解：** 从你的经历中筛出最贴切的 5 段，完整拆解背景 / 任务 / 行动 / 结果 / 复盘

---

### `interview-strategy` — 面试现场展示

面试当天用的两样东西：

- **100 字口播自我介绍：** 口语化，可以直接背，踩中 JD 最看重的 2-3 个点，所有内容溯源到 cv.md
- **可共享屏幕的 HTML 展示网页：** 单文件，浏览器直接打开，关键数字加粗高亮，展示顺序跟自我介绍对齐，让你顺着往下讲

---

### `interview-review` — 面试后复盘

粘贴面试文字稿（录音转写），五个维度逐条诊断：

1. **回答结构** — 有没有清晰的叙述框架（STAR / 金字塔等）
2. **内容质量与真实性** — 核对面试中说的数字和经历是否与 cv.md 一致
3. **岗位匹配度** — JD 核心要求哪些被提到了，哪些被遗漏了
4. **暴露的能力缺口** — 停顿、答非所问、主动承认不会的地方
5. **沟通表达** — 冗长、跑题、口头禅等具体问题

**每条诊断必须引用原文**，不写没有依据的空话。

新发现的缺口自动写入 `data/gap-backlog.md`，下次跑 `gap-roadmap` 时会提示是否并入分析。

---

## Mode 之间的数据流

```
用户粘贴 JD
     ↓
  JDlist/{###}.md  ← 编号在这里分配，JD 原文存档，brief 运行后写入分析结论
     ↓
  brief/{###}.md   ← A+B 评估、评分、gap 初步识别

     ↓                          ↓
cv-tailor/{###}.md         gap-roadmap/{###}.md
（读 JDlist 人才画像）      （读 brief gap 列表）
     ↓                          ↓
            interview-prep/{###}.md
            （读 brief + gap-roadmap，两者合并）
                   ↓
     interview-strategy/{###}.md
     （读 JDlist 人才画像 + cv-tailor 改写经历）
                   ↓
     interview-review/{###}.md
     （读 brief 差距分析 + interview-prep 备考计划）
                   ↓
          data/gap-backlog.md
          （新发现的缺口，下次 gap-roadmap 时并入）
```

**依赖关系说明：**

每个 mode 启动时会检查上游文件是否存在：
- **强依赖缺失** → 系统停下，告诉你先去跑哪个 mode
- **弱依赖缺失** → 继续运行，标注"降级模式"，提示补做

建议顺序（可跳步，但会有提示）：

```
brief → cv-tailor / gap-roadmap → interview-prep → interview-strategy → interview-review
```

---

## 文件结构

```
nogap/
├── cv.md                          # 你的简历（唯一事实源）
├── config/
│   ├── profile.yml                # 你的偏好配置（从 profile.example.yml 复制）
│   └── profile.example.yml        # 配置模板
├── modes/
│   ├── _profile.md                # 你的个人定位策略（从 _profile.template.md 复制）
│   ├── _profile.template.md       # 策略模板
│   ├── _shared.md                 # 系统规则（不要修改）
│   ├── brief.md                   # brief mode 指令
│   ├── cv-tailor.md               # cv-tailor mode 指令
│   ├── gap-roadmap.md             # gap-roadmap mode 指令
│   ├── interview-prep.md          # interview-prep mode 指令
│   ├── interview-strategy.md      # interview-strategy mode 指令
│   └── interview-review.md        # interview-review mode 指令
├── JDlist/                        # JD 原文存档 + 系统分析结论
├── brief/                         # 岗位快速评估报告
├── cv-tailor/                     # 简历定制改写报告
├── gap-roadmap/                   # 能力缺口分析报告
├── interview-prep/                # 面试备战报告
├── interview-strategy/            # 展示方案说明
├── interview-review/              # 面试复盘报告
├── output/                        # 生成的 HTML 展示网页
├── data/
│   ├── applications.md            # 投递记录追踪表
│   └── gap-backlog.md             # 面试复盘回流的新缺口
└── .agents/skills/nogap/
    └── SKILL.md                   # Claude Code skill 入口（勿修改）
```

---

## 个性化定制

### 用对话直接改

NOgap 设计为可以被 AI 直接修改。在 Claude Code 里说：

- "把我的目标岗位改成 AI 产品运营" → 系统更新 `config/profile.yml`
- "我不考虑北京以外的城市" → 写入 `config/profile.yml`
- "这个评分给高了，我在这块经历其实很薄弱" → 系统调整策略并记录到 `modes/_profile.md`
- "我刚加了一段实习经历" → 系统读取更新后的 `cv.md` 重新评估

每次交互后系统会变得更了解你。

### 手动编辑

| 文件 | 修改内容 |
|------|---------|
| `cv.md` | 添加新经历、更新数字、补充细节 |
| `config/profile.yml` | 目标岗位、城市偏好、薪资期望 |
| `modes/_profile.md` | 个人叙事策略、差异化标签、写作风格 |

**永远不要修改 `modes/_shared.md` 和其他 `modes/*.md` 文件**——这些是系统层文件，会随版本更新覆盖。你的所有个性化内容应该在 `modes/_profile.md` 和 `config/profile.yml` 里。

---

## 数据安全

- 所有数据**只存在你本地**，不上传任何服务器
- Claude Code 会把 JD 文本和你的简历发送给 Anthropic 的 API 进行分析，适用 [Anthropic 隐私政策](https://www.anthropic.com/legal/privacy)
- **建议把这个仓库设为私有（private）**，不要把包含真实简历和 JD 的版本 push 到公开仓库

---

## 常见问题

**Q：我没有 Claude Pro，可以用 API key 吗？**
可以。Claude Code 支持直接配置 Anthropic API key（`ANTHROPIC_API_KEY` 环境变量）。按量计费，每次评估大约消耗 $0.02-0.05。

**Q：可以评估英文 JD 吗？**
可以。系统默认用简体中文输出，英文 JD 会被正常解析。如果你想让输出也是英文，在 `modes/_profile.md` 里说明即可。

**Q：`/nogap` 命令不生效？**
确认 Claude Code 是在 `nogap/` 目录下启动的（`claude` 命令在项目根目录运行），技能文件路径为 `.agents/skills/nogap/SKILL.md`。

**Q：我已经面过一些公司了，历史记录怎么导入？**
直接在 `data/applications.md` 里手动加行记录公司名、岗位、状态即可。历史 JD 无需导入，系统从当前开始编号。

**Q：系统更新了我已有的文件吗？**
不会。`cv.md`、`config/profile.yml`、`modes/_profile.md` 是用户层文件，永远不会被自动更新覆盖。`/nogap update` 只更新系统层的 mode 文件。

---

## 伦理原则

- 系统**永远不会**替你提交申请，每一步操作都需要你确认
- 所有简历改写有事实依据安全锁：每条改写溯源到 `cv.md` 原文，禁止编造
- 评分低于 3.5/5 明确建议不投递
- 公司调研和缺口分析使用 WebSearch 实时数据，明确标注来源；搜不到的如实说，不编造

---

## 项目来源

本项目基于 [@santifer](https://github.com/santifer) 的 [career-ops](https://github.com/santifer/career-ops) 开源项目改造，在此致谢原作者。原项目 MIT License。
