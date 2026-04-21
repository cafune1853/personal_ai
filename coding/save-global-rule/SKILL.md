---
name: save-global-rule
description: Use this skill when the user discovers a useful new coding or agent rule while working in any project and wants to capture it into the canonical rule file at ~/code/personal_ai/coding/AGENTS.md, review the exact change, then sync the approved version to ~/.codex/AGENTS.md and commit the personal_ai repo changes.
---

# Save Global Rule

Use this skill when the user wants to add or refine personal global agent rules and keep the canonical personal_ai copy plus the local Codex global copy in sync.

## Files

- Canonical rule source file: `~/code/personal_ai/coding/AGENTS.md`
- Global target file: `/Users/zhiwei.huang/.codex/AGENTS.md`
- Repo to commit: `~/code/personal_ai`

The source of truth is always `~/code/personal_ai/coding/AGENTS.md` unless the user explicitly says otherwise.

The project where the user is currently coding is only the discovery context. Do not edit that project's `AGENTS.md` as part of this skill unless the user explicitly asks for it.

If `~/code/personal_ai/coding/AGENTS.md` is missing, inaccessible, or the user asks to replace the source of truth with a different file, ask before editing anything.

## Required workflow

1. Understand the rule the user wants to capture, including any context from the project where they discovered it.
2. Update `~/code/personal_ai/coding/AGENTS.md` first.
3. Show the user exactly what changed.
4. Pause for review. The user may ask for more edits; if so, keep editing the canonical file and show the new change again.
5. Only after the user approves the canonical file, overwrite `~/.codex/AGENTS.md` with the approved contents.
6. Commit the `personal_ai` repo changes after the sync is complete.

Do not reorder these steps.

## Review gate

Before syncing to `~/.codex/AGENTS.md` or committing:

- summarize the change in plain language
- show the concrete diff or the exact added/removed lines
- wait for explicit user approval

If the user says the change is still not right, continue revising `~/code/personal_ai/coding/AGENTS.md` and repeat the review gate.

## Commit behavior

- Commit inside `~/code/personal_ai`
- Stage only files related to this rule-sync task unless the user asks otherwise
- If "submit" could mean pushing to remote, ask before pushing
- If the user only asked for commit, do not push or open a PR

## Guardrails

- Preserve unrelated existing edits
- Prefer small, style-consistent changes to `AGENTS.md`
- Do not silently rewrite the whole file when a local patch is enough
- If the requested rule conflicts with existing guidance, point out the conflict before editing
- If the user's instruction is too vague to encode reliably as a rule, ask a focused clarifying question before changing the file
- Treat examples from another repo as input context, not as the file to edit
- Keep the rule phrased as a reusable global preference rather than project-specific implementation detail unless the user explicitly wants project-specific wording

## Final response checklist

- Mention that `~/code/personal_ai/coding/AGENTS.md` changed
- Mention whether the global file was synced
- Mention whether a commit was created
- Include any waiting state clearly if approval is still needed
