---
name: draft-goal
description: "Draft and refine Codex goal prompts through clarification before finalization."
---

# Draft Goal

## Overview

Use this skill to turn a raw user request into a strong goal contract before execution. Match the user's language unless they ask otherwise. This is a collaborative drafting workflow: do not treat the first response as the final goal unless the user explicitly asks for a final goal with no further questions.

## Workflow

1. Decide whether `/goal` is appropriate.
   Use a goal when the desired end state is clear but the path is uncertain, requires repeated attempts, or needs evidence before completion. For a one-shot edit or a simple command, tell the user a normal prompt is enough. If `/goal` is not appropriate, do not execute the user's underlying task, do not draft a `/goal`, and stop after giving a polished ordinary prompt the user can use instead.

2. Extract the six goal fields.
   Always organize the requirement into:
   - Result: what must be true when the work is done.
   - Validation surface: tests, benchmarks, reports, artifacts, command output, source material, or other evidence that proves completion.
   - Constraints: behavior, quality, compatibility, safety, or scope that must not regress.
   - Boundaries: files, tools, repositories, data, services, time, budget, or resources Codex may use.
   - Iteration strategy: how Codex should choose the next attempt after each result.
   - Blocked stop condition: when Codex should stop, what it should report, and what input would unlock progress.

3. Clarify before finalizing.
   Start by identifying the goal fields that are clear, uncertain, or missing. Ask up to three concise questions when the user's request leaves meaningful choices about outcome, validation, constraints, boundaries, iteration strategy, or blocked stop conditions. Prefer a short clarification round over making assumptions. If the user explicitly asks for a quick draft, produce a provisional draft and label all assumptions.

4. Draft the structured goal as provisional.
   After the first clarification pass, return the six fields as a reviewable draft. Label it "Draft" or the user's language equivalent. Do not call it final. Include a copyable `Draft /goal` line only when enough information is available to make the draft useful. Do not activate the goal unless the user explicitly asks to set it.

5. Confirm before final goal.
   Ask the user to confirm, revise, or answer the remaining open points. Only after the user confirms the draft or explicitly asks for the final version should you output "Final /goal". Before presenting the final `/goal`, check that it is measurable, evidence-driven, scoped, non-regressive, and has a clear blocked state. Replace vague phrases like "do the best possible job" with concrete evidence standards.

## Output Format

If `/goal` is not appropriate, use this shape and stop:

```text
Suitability: This does not need a `/goal` because <brief reason>.
Suggested ordinary prompt:
<a clearer, more specific version of the user's original request>
```

Do not run tools to perform the underlying task in this branch. Do not include `Draft /goal` or `Final /goal`.

Use this shape for the first response by default:

```text
Suitability: <whether this request is appropriate for a goal, and why>
Known fields:
- Result: <what is already clear>
- Validation surface: <what is already clear>
- Constraints: <what is already clear>
- Boundaries: <what is already clear>
- Iteration strategy: <what is already clear>
- Blocked stop condition: <what is already clear>
Open questions:
1. <question that materially affects the goal>
2. <optional question>
3. <optional question>
```

If the user has already answered the important questions or explicitly asks for a draft, use this shape:

```text
Suitability: <whether this request is appropriate for a goal, and why>
Draft:
Result: <the state that should be true when the work is complete>
Validation surface: <the evidence that proves completion>
Constraints: <what must not break or regress>
Boundaries: <the allowed scope, tools, inputs, and resources>
Iteration strategy: <how to choose the next step after each attempt>
Blocked stop condition: <when to stop, what to report, and what would unlock progress>
Assumptions: <labeled assumptions, or "None">
Draft /goal:
/goal <provisional goal text>
Please confirm or revise the draft before I produce the final `/goal`.
```

Only after confirmation, use this shape:

```text
Final /goal:
/goal <complete goal text>
```

If the user writes in another language, translate the labels naturally or keep them in the user's language.

## Goal Template

Use this template when composing the draft or final line:

```text
/goal <desired end state>, verified by <specific evidence>, while preserving <constraints>. Use <allowed inputs, tools, and boundaries>. Between iterations, <how Codex should choose the next best action>. If blocked or no defensible path remains, <what Codex should report and what would unlock progress>.
```

## Research Goals

For research, paper reproduction, audits, or ambiguous investigations, require an evidence ledger instead of a single success claim. The goal should ask Codex to:

- identify the main claims or target results,
- map each claim to available evidence,
- implement or reconstruct the feasible parts,
- label exact reproductions, approximations, proxy support, blocked claims, and remaining uncertainty,
- finish with an audit report that does not overstate the evidence.

Example:

```text
/goal Use the available paper materials and local resources to produce the strongest evidence-supported reproduction of <paper>. Attempt the main results, map each claim to available evidence, and validate any outputs that can be reconstructed locally. Finish with a report that separates reproduced mechanisms, approximate training results, blocked exact replays, and remaining uncertainty. Between iterations, choose the next step that most reduces uncertainty based on the current evidence. If original data, random seeds, training state, checkpoints, or other critical materials are unavailable and prevent exact reproduction, stop and report the attempted paths, available evidence, blockers, and missing materials needed to unlock progress.
```

## Quality Checks

Before presenting the final `/goal`, verify:

- The result is a state, not just an activity.
- The validation surface is concrete enough for Codex to audit.
- Constraints prevent important regressions.
- Boundaries stop the goal from expanding indefinitely.
- The iteration strategy explains how to continue after partial progress.
- The blocked stop condition allows honest failure instead of false completion.
