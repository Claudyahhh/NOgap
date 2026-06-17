# NOgap

[中文](README.md) | [English](README.en.md)

> 面向中文求职语境下零正职工作经验的年轻人，帮助和陪伴他们消除与理想工作之间的 gap。

NOgap 是一个运行在本地、可由 [OpenAI Codex](https://developers.openai.com/codex) 或 [Claude Code](https://claude.ai/code) 驱动的 AI 求职成长系统。它不是批量投递工具，而是一套围绕真实岗位持续评估、行动和复盘的求职成长闭环。

当前版本优先适配中国大陆的招聘信息、简历表达、求职阶段和面试语境。面向英语国家的独立版本在后续规划中。

## 它解决什么问题

对零正职经验的年轻人来说，困难通常不只是“不会写简历”，而是：

- 不知道一个岗位是否真的适合自己
- 分不清表达问题和真实能力缺口
- 不知道该先补什么、补到什么程度
- 面试准备分散，失败后也没有形成积累

NOgap 把这些问题连接成一个完整流程：

```text
岗位评估
   ↓
简历定制 + 能力补齐
   ↓
面试准备 + 现场展示
   ↓
面试复盘
   ↓
新缺口回流到下一轮行动
```

## 六个核心 Mode

| Mode | 作用 | 主要输出 |
|------|------|----------|
| `brief` | 判断岗位是否值得投入 | 岗位概览、简历匹配度、初步 gap、评分 |
| `cv-tailor` | 针对 JD 重写简历 | 定级分析、人才画像、逐条改写、事实依据 |
| `gap-roadmap` | 识别并补齐真实能力缺口 | 四象限优先级、具体行动、优质教程 |
| `interview-prep` | 准备即将到来的面试 | 公司调研、问题预测、备考清单、STAR 拆解 |
| `interview-strategy` | 组织面试现场的自我展示 | 先确认重点经历、个人主题色、板块、颗粒度、视觉风格和时长，再生成口播自我介绍与纯净 HTML 页面 |
| `interview-review` | 从真实面试中学习 | 五维复盘、新缺口、下一次改进动作 |

每个 Mode 都会生成独立 Markdown 文档。同一 JD 的所有输出共享一个三位数字编号，从 `000` 开始。

## 产品展示

下面是 `interview-strategy` 生成的虚构示例。人物、公司、经历、数字和项目均为演示数据，不包含真实用户隐私。

### 桌面端

![NOgap Interview Strategy 桌面端示例](docs/assets/interview-strategy-demo-desktop.jpg)

### 手机端

<img src="docs/assets/interview-strategy-demo-mobile.jpg" alt="NOgap Interview Strategy 手机端示例" width="360">

[打开示例 HTML](docs/demo/interview-strategy-demo.html)

## 快速开始

### 环境要求

- [OpenAI Codex](https://developers.openai.com/codex)（桌面端或 CLI）或 [Claude Code](https://claude.ai/code)
- OpenAI 账号（使用 Codex）或 Anthropic 账号 / API 凭据（使用 Claude Code）
- Git
- Node.js 18 或更高版本

### 安装

```bash
git clone https://github.com/Claudyahhh/NOgap.git
cd NOgap
```

### 使用 Codex

你可以在 Codex 桌面端打开克隆后的 `NOgap` 文件夹，也可以在仓库目录启动 Codex CLI：

```bash
codex
```

然后直接输入：

```text
使用 NOgap，显示所有功能。
```

也可以直接粘贴一份 JD。Codex 会读取仓库中的 `AGENTS.md` 和 NOgap skill，完成初始化并进入 `brief`。

### 使用 Claude Code

在仓库目录启动：

```bash
claude
```

然后输入：

```text
/nogap
```

也可以直接粘贴一份 JD，系统会自动进入 `brief`。

完成首次初始化后，可以运行：

```bash
node doctor.mjs
```

检查个人文件和系统目录是否完整。

## 第一次使用

NOgap 会检查三个个人文件：

| 文件 | 用途 |
|------|------|
| `cv.md` | 唯一简历事实源 |
| `config/profile.yml` | 目标岗位、求职阶段、地点等基础偏好 |
| `modes/_profile.md` | 个人优势、叙事策略、拒绝条件和写作风格 |

如果文件缺失，系统会通过对话引导你创建。你可以直接粘贴现有简历，也可以让系统根据你的经历起草。

初始化完成后，直接粘贴目标 JD 即可开始。

## 常用 Mode

在 Codex 中可以直接使用自然语言：

```text
评估下面这份 JD。
对 #000 运行 cv-tailor。
对 #000 运行 gap-roadmap。
对 #000 运行 interview-prep。
对 #000 运行 interview-strategy。
使用这份面试文字稿对 #000 运行 interview-review。
```

在 Claude Code 中也可以使用对应命令：

```text
/nogap
/nogap brief
/nogap cv-tailor #000
/nogap gap-roadmap #000
/nogap interview-prep #000
/nogap interview-strategy #000
/nogap interview-review #000
```

`#000` 指向该 JD 的统一编号。两种使用方式都会通过编号读取同一岗位的上下文。

运行 `interview-strategy` 后，系统不会立即生成网页，而会先推荐并确认本轮想重点讲的经历、个人主题色、网页主题色、保留板块、内容颗粒度、视觉风格和预计讲解时长，并提醒你上传本轮面试可能展示的项目文件或链接。确认后生成的 HTML 是面试成品页，不包含配色按钮、上传提示、编辑提示或生成说明。

如果你提供个人主题色，NOgap 会把它写入 `modes/_profile.md`，之后生成面试展示网页时默认优先采用。网页内容会比普通个人主页更详细，会围绕简历中的核心经历补充场景、行动、结果和与 JD 的关系，帮助面试官快速抓住重点。

项目链接会被整理为可直接打开的展示入口。本地 PDF、图片、HTML 或其他项目文件会复制到该 JD 的 `output/assets/{###}/` 资源目录，网页通过相对路径引用，不会暴露原始电脑路径。

## 信息如何流动

```text
JDlist/000-*.md
  保存 JD 原文、岗位画像、初步 gap 和评分
          │
          ▼
brief/000-*.md
          │
          ├──────────────┐
          ▼              ▼
cv-tailor/          gap-roadmap/
          │              │
          └──────┬───────┘
                 ▼
         interview-prep/
                 ▼
       interview-strategy/
                 ▼
        interview-review/
                 ▼
       data/gap-backlog.md
                 │
                 └── 回流到下一次 gap-roadmap
```

### 依赖机制

- 强依赖缺失：停止执行，并提示先运行哪个 Mode
- 弱依赖缺失：允许降级执行，同时说明缺少的上下文
- 每个 Mode 完成后：提示最合理的下一步

这让单独使用某个 Mode 成为可能，也避免用户在缺少关键上游分析时得到看似完整、实际失真的结果。

## 核心原则

### 真实性

`cv.md` 是唯一事实源。简历改写可以调整角度和语言，但不能编造数字、项目、职责或合作方。每条关键改写都应能追溯到真实经历。

### 区分表达 gap 与能力 gap

- 表达 gap：有相关经历，但没有写清楚，由 `cv-tailor` 处理
- 能力 gap：确实不会或没有做过，由 `gap-roadmap` 处理

### 质量优先

NOgap 不代替用户提交申请，也不鼓励无差别投递。系统的目标是帮助用户把时间投入更匹配、更真实的机会。

### 复盘回流

面试中暴露的新问题会进入 `data/gap-backlog.md`，成为后续学习路径和面试准备的新输入。

## 输出目录

```text
JDlist/               JD 原文与共享上下文
brief/                岗位快速评估
cv-tailor/            简历定制
gap-roadmap/          能力缺口与行动路径
interview-prep/       面试前准备
interview-strategy/   面试现场展示策略
interview-review/     面试后复盘
output/               HTML 展示页面
data/                 投递记录与缺口回流
```

这些个人输出默认不会被 Git 提交。

## 数据与隐私

- 简历、JD、报告和个人配置保存在本地
- Codex 或 Claude Code 分析时会将必要内容发送给各自的模型服务，请阅读所使用产品的数据与隐私政策
- 不要将包含真实简历、联系方式、面试记录或公司内部信息的文件提交到公开仓库
- 建议使用私有仓库保存个人使用中的 NOgap 工作区

## 当前范围

当前版本的评分逻辑、输出语言、简历表达和面试建议以中文求职语境为核心。英文 JD 可以被解析，但这不等同于已完成英语国家招聘制度、文化和表达习惯的适配。

未来计划提供面向英语国家的独立版本，而不是在中文版本中简单翻译界面。

## 致谢与许可

NOgap 的早期架构设计借鉴了 [@santifer](https://github.com/santifer) 的开源项目 [career-ops](https://github.com/santifer/career-ops)。NOgap 在目标用户、工作流、Mode 设计、信息传递和输出结构上进行了重新设计。

本项目采用 MIT License。原项目版权声明和 NOgap 修改版权声明均保留在 [LICENSE](LICENSE) 中。
