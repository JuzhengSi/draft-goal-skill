# draft-goal-skill

[![skills.sh](https://skills.sh/b/JuzhengSi/draft-goal-skill)](https://skills.sh/JuzhengSi/draft-goal-skill)

`draft-goal-skill` helps AI agents turn vague or high-level requests into reviewable, evidence-driven `/goal` contracts.

The skill is intentionally collaborative. It does not treat the first answer as final. It first decides whether `/goal` is appropriate, asks focused clarification questions when needed, drafts a provisional goal, and only produces a final `/goal` after confirmation.

## What It Does

- Decides whether a request is suitable for goal-driven autonomous work.
- Extracts the six fields of a strong goal:
  - result
  - validation surface
  - constraints
  - boundaries
  - iteration strategy
  - blocked stop condition
- Asks concise clarification questions before finalizing.
- Produces a draft `/goal` for review.
- Produces a final `/goal` only after the user confirms.
- Refuses to turn simple one-shot tasks into goals; instead, it suggests a clearer ordinary prompt.

## When To Use It

Use this skill when the task has a clear desired end state but an uncertain path, such as:

- debugging an intermittent test failure until it is fixed or clearly blocked
- migrating a complex dependency while preserving behavior
- improving benchmark results with repeated measurement
- reproducing or auditing a research result
- turning a vague project request into a scoped, testable contract

## When Not To Use It

Do not use `/goal` for simple, direct requests such as:

- changing one CSS rule
- running a single command
- explaining an error message
- editing one known file in a straightforward way

In these cases, the skill should not execute the request and should not draft a `/goal`. It should explain that a normal prompt is enough and provide a polished ordinary prompt.

## Installation

Install from GitHub with skills.sh:

```bash
npx skills add JuzhengSi/draft-goal-skill
```

You can also install from a local checkout:

```bash
npx skills add .
```

Or copy this folder into an agent skills directory:

```bash
cp -R skills/draft-goal .agents/skills/draft-goal
```

Adjust the destination path for your agent environment if it uses a different skills directory.

## Usage

Invoke the skill by name:

```text
$draft-goal I want the agent to keep working on this flaky checkout test until it is either fixed with evidence or clearly blocked.
```

For a suitable long-running task, the skill will usually start with known fields and open questions. After the important questions are answered, it returns a draft goal. After confirmation, it returns the final copyable `/goal`.

For a simple one-shot request, it returns a suggested ordinary prompt instead of a goal.

## Workflow

1. Suitability check: decide whether `/goal` is appropriate.
2. Clarification: ask up to three questions if important details are missing.
3. Draft: produce a reviewable goal contract with assumptions labeled.
4. Confirmation: wait for the user to confirm or revise.
5. Final: produce the final `/goal` only after confirmation.

## Examples

See the `examples/` directory:

- `suitable-goal.md`: a request that should become a `/goal`
- `not-suitable.md`: a simple task that should stay a normal prompt
- `needs-clarification.md`: a request that needs questions before drafting

## License

MIT
