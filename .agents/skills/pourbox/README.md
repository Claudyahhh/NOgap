# Pourbox

Pourbox is a safety-first Codex skill for cleaning Outlook mailboxes.

It helps you pour out email clutter without guessing what matters: first it asks the retention boundaries, then it audits Outlook search results, deletes in recoverable batches, and verifies that each cleanup scope is actually empty.

## Product Description

Pourbox is for people whose mailbox has become a storage closet: old applications, newsletters, sent drafts, automated notices, and years of half-useful threads. It turns vague cleanup wishes into explicit retention choices, then carries out the cleanup in Outlook with human confirmation at the risky moments.

The core promise is simple: ask before deleting, batch carefully, keep recovery possible.

## Installation

Place this folder in a Codex skills directory:

```text
~/.codex/skills/pourbox
```

Then invoke it by name:

```text
Use $pourbox to clean my Outlook mailbox.
```

## What It Does

- Cleans Outlook web mail through the in-app browser.
- Supports Inbox Focused, Inbox Other, Sent Items, Archive, and custom folders.
- Converts fuzzy requests like "older than one month" into exact date boundaries.
- Lets users choose what to keep: flagged messages, confirmed offers, official role accounts, custom rules, or nothing.
- Handles Outlook's 75-conversation batch deletion limit.
- Moves messages to Deleted Items by default instead of permanently deleting them.

## How To Use

Invoke the skill:

```text
Use $pourbox to clean my Outlook mailbox.
```

Pourbox will ask five boundary questions:

1. How old should deleted messages be?
2. Which folders should be cleaned?
3. Which messages should be kept?
4. What should happen to the Other inbox category?
5. Should Deleted Items remain recoverable?

You can answer with option codes:

```text
1A 2B 3C 4A 5A
```

## Presets

```text
Cautious:   1A 2B 3C 4A 5A
Balanced:  1A 2B 3B 4A 5A
Aggressive: 1A 2B 3D 4B 5A
```

Pourbox never chooses the aggressive mode unless the user explicitly selects it.

## Safety Rules

- Deletion syncs across Outlook clients.
- Messages go to Deleted Items unless permanent deletion is separately confirmed.
- Flags are treated as user data, not temporary markers.
- Official accounts are identified by role and purpose, not only by domain.
- `offer` messages are sampled and checked to avoid false positives.
- The final Outlook confirmation dialog is treated as the authoritative count.

## Skill Files

```text
pourbox/
├── SKILL.md
├── README.md
├── agents/openai.yaml
└── references/classification.md
```

## Tagline

Pourbox: pour out the clutter, keep what matters.
