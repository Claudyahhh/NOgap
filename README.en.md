# NOgap

[中文](README.md) | [English](README.en.md)

> An AI career-growth companion for young people with no full-time work experience, designed first for the Chinese-language job market.

NOgap is a local AI career-growth system that can run with [OpenAI Codex](https://developers.openai.com/codex) or [Claude Code](https://claude.ai/code). It helps users close the gap between where they are and the work they want. It is not a mass-application tool. It creates a continuous loop of role evaluation, focused action, interview preparation, and learning from real outcomes.

The current version is designed around mainland China's job descriptions, resume conventions, early-career stages, and interview context. A separate version for English-speaking countries is planned.

## The Problem

NOgap grew out of the job-search experience shared by me and many young people around me. The difficulty is not only getting a resume seen or surviving the final interview. It is the often invisible **cognitive and capability gap** between a candidate and the role they care about most.

Most career products optimize discovery and application volume. For people with little or no full-time experience, the more important questions are:

- Do I actually understand what this role is trying to accomplish and what kind of person it needs?
- What exactly separates me from the role I want?
- Which gaps are communication problems, and which are real capability gaps?
- Which capability should I build first, and how can I turn it into visible evidence?
- How can each application, preparation cycle, and interview improve the next one?

Applying for a role is not only a submission task. It is a process of learning, training, and iteration.

NOgap therefore connects those decisions into one workflow:

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

## What Each Mode Produces

<details>
<summary><strong>1. brief: decide whether the role deserves deeper investment</strong></summary>

`brief` compares the JD with evidence from the candidate's real experience and produces:

1. **A | Role overview**: function, domain, level, location, team, core responsibilities, and the kind of person the role truly needs.
2. **B | Resume fit**: requirement-by-requirement mapping to evidence in `cv.md`, separating direct matches, transferable experience, and missing proof.
3. **Initial gaps**: hard gaps, bonus gaps, substitute evidence, and portfolio material to add.
4. **Score and recommendation**: a 1–5 fit score followed by the most useful next step.

The conclusions are written back to the numbered JD record so later modes can reuse the same analysis.

</details>

<details>
<summary><strong>2. cv-tailor: express existing value fully without crossing the truth boundary</strong></summary>

`cv-tailor` rebuilds the application narrative rather than merely replacing keywords:

1. **Candidate level**: level fit and the three to five strongest advantages.
2. **JD talent profile**: critical abilities, preferred experience patterns, recurring language, and differentiation opportunities.
3. **Experience classification**: directly relevant, indirectly transferable, or contextual support.
4. **Line-by-line rewrite**: original statement, revised statement, factual basis, and transferable value.
5. **Overall narrative**: resume storyline, central proof point, and priority of each experience.

Its boundary is explicit: **make the boldest competitive restatement supported by existing facts, but never invent a project, responsibility, metric, or result.** Every revision must trace back to `cv.md` and remain defensible in an interview.

</details>

<details>
<summary><strong>3. gap-roadmap: identify the capability with the highest return on effort</strong></summary>

`gap-roadmap` separates wording gaps from real capability gaps, then prioritizes them by **role impact × cost to close**. It produces:

1. **Existing assets**: current abilities, transferable experience, and reusable projects.
2. **A four-quadrant gap map**: fix now, schedule next, take the low-cost win, or deliberately defer.
3. **Three to five action paths**: timing, concrete steps, completion criteria, and an artifact that can become evidence.
4. **Current learning resources**: web-researched tutorials selected for authority, usefulness, and reputation.
5. **Substitutes for gaps that cannot be closed quickly**: an honest plan for handling them in a portfolio or interview.

Instead of saying “learn LLMs,” it may ask the user to understand how LLMs are trained, what structural errors those methods create, and how to demonstrate that understanding through a small experiment.

</details>

<details>
<summary><strong>4. interview-prep: understand the company and why the interview asks what it asks</strong></summary>

`interview-prep` avoids generic question banks. It generates:

1. **Gap reminder**: the most interview-relevant items from `gap-roadmap`.
2. **Company and market research**: current research on ecosystem position, product and business model, competitors, recent moves, and strategic direction, followed by an inference about why the company needs this role.
3. **Four personalized question boards**: industry fundamentals, industry trends, personal capability depth, and project execution or experience verification.
4. **Question analysis**: probability, difficulty, interviewer intent, and answer direction.
5. **P0–P2 preparation list**: five to eight actions ordered by urgency.
6. **STAR story breakdowns**: two to three core experiences structured as Situation, Task, Action, and Result.

The objective is not to memorize polished answers. It is to understand where the company is going and which judgments and evidence to bring into the conversation.

</details>

<details>
<summary><strong>5. interview-strategy: turn core experience into evidence that can be spoken and shown</strong></summary>

`interview-strategy` uses a two-stage workflow. Before generating a site, it confirms the experiences to emphasize, personal and interview theme colors, selected sections, detail level, visual style, speaking time, and project files or links.

It then produces:

1. **Spoken introduction**: a concise, role-specific opening of roughly 100 Chinese characters that establishes who the candidate is, why they fit, and what deserves follow-up.
2. **Clean interview presentation site**: a shareable standalone HTML page that supports the conversation without becoming a script full of paragraphs.

The page can present positioning, experience context/actions/results/JD relevance, projects and demos, metrics, methods, workflows, screenshots, and potential team contributions. The final page contains no generation controls. Important visuals receive large display areas, and local assets use relative paths for private, portable sharing.

</details>

<details>
<summary><strong>6. interview-review: make one interview improve the next one</strong></summary>

`interview-review` checks transcript quality, then reviews five dimensions:

1. **Answer structure**: clarity, focus, completeness, and evidence order.
2. **Content quality and truthfulness**: specific actions, judgments, outcomes, and verifiable detail.
3. **JD coverage**: whether the role's most important capabilities were demonstrated.
4. **Exposed capability gaps**: missing knowledge, experience, or judgment revealed by weak answers.
5. **Communication**: pace, redundancy, avoidance, follow-up handling, and interaction quality.

Every finding cites transcript evidence and includes a concrete next action. New gaps flow into `data/gap-backlog.md`; missing question types can be added to interview preparation. Resume facts surfaced in the interview generate recommendations only and **never trigger an automatic edit to `cv.md`**. The report ends with the three highest-priority improvements.

</details>

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

### Restraint Defines the Product Boundary

NOgap deliberately removed features outside its core journey and keeps only the six steps from **understanding a JD and preparing an application to reviewing an interview**. It is not trying to become a career platform that does everything at 60%. It aims to serve one important journey deeply: helping young candidates learn, practice, build evidence, and improve.

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
