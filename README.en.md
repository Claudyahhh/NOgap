# NOgap

[中文](README.md) | [English](README.en.md)

> An AI career-growth companion for young people with no full-time work experience, designed first for the Chinese-language job market.

NOgap is a local AI career-growth system that can run with [OpenAI Codex](https://developers.openai.com/codex) or [Claude Code](https://claude.ai/code). It helps users close the gap between where they are and the work they want. It is not a mass-application tool. It creates a continuous loop of role evaluation, focused action, interview preparation, and learning from real outcomes.

The current version is designed around mainland China's job descriptions, resume conventions, early-career stages, and interview context. A separate version for English-speaking countries is planned.

## The Problem

For people without full-time work experience, the challenge is rarely just resume wording. They often need to determine:

- whether a role is genuinely worth pursuing
- whether a mismatch is a communication problem or a real skill gap
- what to learn first and what “good enough” looks like
- how to prepare for interviews without starting from zero each time
- how to turn rejection and weak answers into reusable learning

NOgap connects those decisions into one workflow:

```text
Role evaluation
      ↓
Resume tailoring + skill development
      ↓
Interview preparation + live presentation
      ↓
Interview review
      ↓
New gaps feed the next action plan
```

## Six Core Modes

| Mode | Purpose | Main output |
|------|---------|-------------|
| `brief` | Decide whether a role deserves time and attention | Role overview, CV match, initial gaps, score |
| `cv-tailor` | Tailor the resume to a specific JD | Level analysis, candidate profile, rewritten experience, evidence |
| `gap-roadmap` | Identify and close real capability gaps | Priority matrix, concrete actions, selected learning resources |
| `interview-prep` | Prepare for an upcoming interview | Company research, predicted questions, preparation plan, STAR stories |
| `interview-strategy` | Structure the live interview presentation | Confirm key experiences, personal theme color, sections, detail level, visual style, and duration before generating a spoken introduction and clean HTML presentation |
| `interview-review` | Learn from an actual interview | Five-part review, newly exposed gaps, next actions |

Each Mode writes a standalone Markdown document. Outputs for the same job share a three-digit ID beginning with `000`.

## Product Preview

The following `interview-strategy` page is a fictional demo. The person, company, experience, metrics, and projects are invented and contain no real user information.

### Desktop

![NOgap Interview Strategy desktop demo](docs/assets/interview-strategy-demo-desktop.jpg)

### Mobile

<img src="docs/assets/interview-strategy-demo-mobile.jpg" alt="NOgap Interview Strategy mobile demo" width="360">

[Open the demo HTML](docs/demo/interview-strategy-demo.html)

## Quick Start

### Requirements

- [OpenAI Codex](https://developers.openai.com/codex) (desktop app or CLI) or [Claude Code](https://claude.ai/code)
- An OpenAI account for Codex, or an Anthropic account / API credentials for Claude Code
- Git
- Node.js 18 or later

### Install

```bash
git clone https://github.com/Claudyahhh/NOgap.git
cd NOgap
```

### Use with Codex

Open the cloned `NOgap` folder in the Codex desktop app, or start Codex CLI from the repository:

```bash
codex
```

Then ask:

```text
Use NOgap and show all available features.
```

You can also paste a job description directly. Codex reads the repository's `AGENTS.md` and NOgap skill, completes setup, and routes the JD to `brief`.

### Use with Claude Code

Start Claude Code from the repository:

```bash
claude
```

Then run:

```text
/nogap
```

You can also paste a job description directly. NOgap will route it to `brief`.

After completing first-time setup, run:

```bash
node doctor.mjs
```

to verify the personal files and system directories.

## First-Time Setup

NOgap checks for three personal files:

| File | Purpose |
|------|---------|
| `cv.md` | The only source of truth for resume facts |
| `config/profile.yml` | Target roles, career stage, location, and basic preferences |
| `modes/_profile.md` | Strengths, narrative strategy, constraints, and writing style |

If any file is missing, the system guides the user through creating it in conversation. Users can paste an existing resume or describe their experience and ask NOgap to draft one.

Once setup is complete, paste a target JD to begin.

## Common Modes

In Codex, use natural-language requests:

```text
Evaluate the following job description.
Run cv-tailor for #000.
Run gap-roadmap for #000.
Run interview-prep for #000.
Run interview-strategy for #000.
Use this interview transcript to run interview-review for #000.
```

In Claude Code, you can also use the corresponding commands:

```text
/nogap
/nogap brief
/nogap cv-tailor #000
/nogap gap-roadmap #000
/nogap interview-prep #000
/nogap interview-strategy #000
/nogap interview-review #000
```

`#000` identifies one JD across the entire workflow. Both interfaces use that ID to load the correct context.

`interview-strategy` uses a two-step flow. It first confirms the past experiences the user wants to emphasize, personal theme color, page theme color, sections, level of detail, visual style, and expected presentation duration, and asks for any project files or links that may be shown during the interview. The generated HTML is a presentation-ready page with no color picker, upload prompt, editing prompt, or generation UI.

If the user provides a personal theme color, NOgap records it in `modes/_profile.md` and uses it by default for future interview pages. The page is intentionally more detailed than a generic personal website: it highlights the situation, action, result, metrics, and JD relevance behind key resume experiences so interviewers can understand the strongest evidence quickly.

Public links become project actions. Approved local files are copied into `output/assets/{###}/` and referenced with relative paths, so the page never exposes the original path on the user's computer.

## How Information Flows

```text
JDlist/000-*.md
  Stores the original JD, role profile, initial gaps, and score
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
                 └── feeds the next gap-roadmap
```

### Dependency Rules

- Missing hard dependency: stop and tell the user which Mode to run first
- Missing soft dependency: continue in a reduced-quality mode and explain what context is absent
- Completed Mode: recommend the most useful next step

This keeps every Mode independently callable without pretending that missing upstream analysis has no cost.

## Design Principles

### Evidence Before Polish

`cv.md` is the only source of truth. NOgap may reframe real experience, but it must not invent metrics, projects, responsibilities, or partners. Important rewrites should remain traceable to actual evidence.

### Separate Wording Gaps from Skill Gaps

- Wording gap: relevant experience exists but is poorly expressed; handled by `cv-tailor`
- Skill gap: the user genuinely lacks the capability or experience; handled by `gap-roadmap`

### Quality Over Volume

NOgap never submits applications for the user and does not encourage indiscriminate applying. Its purpose is to help users invest effort in opportunities that are more relevant and more real.

### Learning Must Feed Back

New weaknesses exposed during interviews are stored in `data/gap-backlog.md` and become input for future learning plans and interview preparation.

## Output Directories

```text
JDlist/               Original JDs and shared context
brief/                Fast role evaluations
cv-tailor/            Tailored resume reports
gap-roadmap/          Skill-gap analysis and action plans
interview-prep/       Pre-interview preparation
interview-strategy/   Live presentation strategy
interview-review/     Post-interview reviews
output/               Generated HTML pages
data/                 Application tracking and gap feedback
```

Personal outputs are ignored by Git by default.

## Data and Privacy

- Resumes, JDs, reports, and personal configuration remain in the local workspace
- Codex or Claude Code sends required context to its model service during analysis; review the data and privacy policy of the product you use
- Do not commit real resumes, contact details, interview transcripts, or confidential company information to a public repository
- A private repository is recommended for an actively used personal NOgap workspace

## Current Scope

The current scoring logic, output language, resume conventions, and interview advice are built primarily for the Chinese-language job market.

English JDs can be parsed, but that does not mean the system has fully adapted to the hiring systems, culture, and communication norms of English-speaking countries. A dedicated international version is planned instead of a simple translation of the Chinese version.

## Acknowledgements and License

NOgap's early architecture was inspired by [career-ops](https://github.com/santifer/career-ops), created by [@santifer](https://github.com/santifer). NOgap redesigns the target audience, workflow, Mode boundaries, information flow, and output structure.

This project is licensed under the MIT License. The original copyright notice and the copyright notice for NOgap modifications are retained in [LICENSE](LICENSE).
