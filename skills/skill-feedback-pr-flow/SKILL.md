---
name: skill-feedback-pr-flow
description: "Use when a user gives feedback, correction, rejection, or an improvement request about an agent skill, SKILL.md, or the agent's skills; routes the change through self-improve, compact skill editing, Syncwheel PR delivery, and an explicit install-now versus wait-for-merge decision."
metadata:
  author: Yehonal
  version: "1.0"
---

# Skill Feedback PR Flow

Use for durable feedback about skills. The goal is a source-backed PR that must merge before the
improvement is considered complete.

## Contract

- Use `self-improve` to turn feedback into a durable rule and target.
- For any `SKILL.md` edit, use `compact-skill-creator`; do not edit skill text directly.
- Use the owning source repo. Never edit Agentwheel cache, runtime-installed skills, or generated outputs as the source of truth.
- Use Syncwheel before branch, commit, push, PR, integration, cleanup, or handoff work.
- Produce a PR for the skill-source change. A local edit or runtime install alone is not complete.
- Treat the PR as review-only unless the user explicitly authorizes merge.

## Workflow

1. Capture the feedback as one durable rule. If the target skill/doc is unclear after inspection, ask one concise question; otherwise proceed.
2. Locate the owning source package or repo with Agentwheel config, repo files, and sibling skills. If only runtime/cache copies exist, stop and report the missing source path.
3. Run `syncwheel repo tracking status` in the source repo before branch work. If tracking is missing, initialize or set the policy only when the repo owner/user has authorized that delivery scope; otherwise stop before branch/PR work.
4. Create or select the Syncwheel stack/branch for the feedback. Keep unrelated dirty files out of the stack.
5. Draft the skill/doc change through `self-improve` and `compact-skill-creator`; preserve all feedback intent in the shortest clear text.
6. Validate the changed skill: YAML frontmatter parses, required references exist, and any touched scripts/tests pass or are explicitly unavailable.
7. Commit only the scoped files, record the stack commits in Syncwheel, validate/plan, then push and open the PR.
8. Report PR URL, changed files, validation, and install decision.

## Install Decision

Default: wait for the PR to merge, then install/update through Agentwheel from the merged source.

Pre-merge install is allowed only when the user explicitly approves it as a temporary hotfix. Record:

- PR URL and branch
- installed source commit
- why pre-merge install was needed
- validation run
- follow-up to reconcile after merge

## Completion

The improvement is complete only when every item is true:

- PR exists for the source change
- PR merge status is known
- if merged, Agentwheel install/update has been considered and either run or deliberately deferred
- if installed pre-merge, the temporary install is reconciled or tracked as follow-up
- unrelated local changes are reported, not hidden
