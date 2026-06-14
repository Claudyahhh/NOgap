---
name: nogap
description: NOgap — AI 求职成长助手（评估 / 简历 / 能力 / 面试准备 / 面试展示 / 面试复盘）
arguments: mode # Claude Code specific
user-invocable: true
argument-hint: "[brief | cv-tailor | gap-roadmap | interview-prep | interview-strategy | interview-review]"
license: MIT
---

# NOgap -- Router

## Mode Routing

Determine the mode from `$mode`:

| Input | Mode |
|-------|------|
| (empty / no args) | `discovery` -- Show command menu |
| JD text or URL (no sub-command) | **`brief`** |
| `brief` | `brief` |
| `report` | `brief` (alias, backward compat) |
| `cv-tailor` | `cv-tailor` |
| `gap-roadmap` | `gap-roadmap` |
| `interview-prep` | `interview-prep` |
| `interview-strategy` | `interview-strategy` |
| `interview-review` | `interview-review` |

**Auto-pipeline detection:** If `$mode` is not a known sub-command AND contains JD text (keywords: "职责""要求""岗位""responsibilities", "requirements", "qualifications", company name + role) or a URL to a JD, execute `brief` directly.

If `$mode` is not a sub-command AND doesn't look like a JD, show discovery.

---

## Discovery Mode (no arguments)

Show this menu:

```
NOgap — AI 求职成长助手

核心功能（六步求职成长闭环）：
  /nogap {JD}               → 岗位评估：粘贴 JD 自动产出 A+B 快速评估 + 评分 + 下一步推荐
  /nogap brief              → 同上（显式调用）
  /nogap cv-tailor          → 简历改写：定级分析 + 针对目标 JD 逐条改写 + 事实依据安全锁
  /nogap gap-roadmap        → 能力缺口：四象限优先级 + 含教程推荐的可执行行动路径
  /nogap interview-prep     → 面试备战：公司调研 + 个性化问题预测 + P0-P2 备考清单 + STAR 拆解
  /nogap interview-strategy → 面试展示：开场自我介绍 + 可共享屏幕的展示网页
  /nogap interview-review   → 面试复盘：五维度诊断 + 缺口回流 + 下次改进点

使用方式：直接粘贴 JD 文本或 URL，即可启动岗位快速评估。所有 mode 输出均以三位 JD 编号对齐存档。
```

---

## Context Loading by Mode

After determining the mode, load the necessary files before executing:

### Modes that require `_shared.md` + their mode file:
Read `modes/_shared.md` + `modes/{mode}.md`

Applies to: `brief`

### Standalone modes (only their mode file):
Read `modes/{mode}.md`

Applies to: `cv-tailor`, `gap-roadmap`, `interview-prep`, `interview-strategy`, `interview-review`

Execute the instructions from the loaded mode file.
