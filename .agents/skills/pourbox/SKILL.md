---
name: pourbox
description: Pourbox is a public, safety-first Outlook web mail cleanup workflow for auditing, filtering, and batch-deleting mailbox clutter through the in-app browser. Use when a user asks to delete old email, clean Focused or Other inbox categories, remove Sent mail, preserve flagged/official/offer messages, reduce mailbox storage, or define repeatable Outlook retention rules.
---

# Pourbox

Use the in-app Browser skill. Read its confirmation guidance before interacting with Outlook.

## Start with boundary questions

If the user has not already answered a boundary, ask it before filtering. Prefer one compact questionnaire. Use the question UI when available; otherwise show numbered options and accept answers such as `1B 2A 3D 4B 5A`.

1. **Age boundary**
   - A. Older than one calendar month
   - B. Older than a rolling number of days
   - C. Before an exact date
   - D. No age boundary for selected categories

2. **Folders**
   - A. Inbox only
   - B. Inbox and Sent Items
   - C. Inbox, Sent Items, and Archive
   - D. Custom folders

3. **Messages to keep**
   - A. Current flagged/favorite messages
   - B. Flagged messages and confirmed offers
   - C. Flagged messages, confirmed offers, and official role accounts
   - D. Nothing
   - E. Custom rules

4. **Other inbox category**
   - A. Apply the same age and keep rules
   - B. Delete everything in Other
   - C. Skip Other

5. **Deleted Items**
   - A. Move there and keep recoverable
   - B. Empty permanently after a separate confirmation

Ask a follow-up only when the selected option needs a value, such as the exact date, day count, custom folders, or custom keep rules.

## Offer presets

When the user asks for a recommendation, offer:

- **Cautious:** `1A 2B 3C 4A 5A`
- **Balanced:** `1A 2B 3B 4A 5A`
- **Aggressive:** `1A 2B 3D 4B 5A`

Never choose Aggressive without explicit user selection.

## Normalize the request

Before acting, convert the answers into an execution contract:

```text
Cutoff: YYYY-MM-DD and earlier / earlier than YYYY-MM-DD
Folders: ...
Keep: ...
Other: ...
Deleted Items: recoverable / permanent
```

For relative dates, state the absolute date and whether it is inclusive. "Older than one calendar month" normally keeps messages on the same day of the previous month and deletes the day before and earlier.

## Audit

1. Inspect the active account, folder, Focused/Other category, search state, and selection.
2. Test each filter separately.
3. Set Outlook advanced search scope to `Current folder`.
4. Use the end-date picker instead of relying only on textual date operators.
5. Sample visible results and verify rendered dates, senders, and categories.
6. Report ambiguity before deletion. Preserve uncertain messages unless the user selected "keep nothing."

## Preserve without mutating user data

- Never use flags as temporary retention markers.
- Treat current flags as user data.
- Prefer deletion queries that exclude retained messages.
- If Outlook cannot express a safe exclusion, delete narrower reviewed groups.
- If a prior run added temporary flags, disclose that their provenance cannot be recovered and default to retaining all current flags.

Read [references/classification.md](references/classification.md) when preserving offers or official accounts.

## Delete

Process independent scopes in this order:

1. Other category, if selected.
2. Focused category.
3. Sent Items.
4. Archive or custom folders.

For each scope:

1. Apply category, folder, and date filters.
2. Select all matching results.
3. Stop at Outlook's final deletion dialog.
4. State the scope and authoritative dialog count.
5. Obtain action-time confirmation unless the user just confirmed that exact scope.
6. Confirm deletion.
7. Wait for the success notice.
8. Repeat while matching results remain.

Outlook may delete search results in batches of 75 conversations. Do not declare completion after one batch.

## Verify

- Confirm every requested scope says no results remain.
- Confirm Deleted Items was not emptied unless separately authorized.
- Report counts by scope and total.
- Explain that cloud deletion may not immediately reduce local disk use because Outlook cache compaction can lag.

## Safety rules

- Deletion syncs across Outlook clients.
- "Delete all Other" overrides keep rules within Other. Call this out explicitly.
- Never permanently empty Deleted Items under the same confirmation used for ordinary deletion.
- After a failed locator or navigation, take a fresh DOM snapshot before acting.
- Use the final Outlook dialog, not visible row count, as the authoritative batch count.

