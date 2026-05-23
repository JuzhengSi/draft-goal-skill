# Suitable Goal Example

## User Request

```text
$draft-goal I want the agent to keep working on an intermittent checkout test failure until it either fixes the issue with evidence or can clearly explain what blocks progress.
```

## Expected Skill Behavior

The request is suitable for `/goal` because the desired end state is clear, the path is uncertain, and completion requires evidence.

The skill should identify or ask about:

- the failing test command
- the expected evidence for a real fix
- allowed files or services
- regressions that must not happen
- how the agent should iterate after each failure
- when the agent should stop as blocked

## Example Draft Shape

```text
Suitability: This is appropriate for a `/goal` because it requires repeated investigation and evidence-backed completion.
Draft:
Result: The intermittent checkout test is either fixed with a known cause or clearly classified as blocked.
Validation surface: Repeated passing test runs, relevant logs, and a short explanation of the root cause or blocker.
Constraints: Preserve existing checkout behavior and avoid weakening assertions.
Boundaries: Use the checkout service, related tests, fixtures, and local test commands.
Iteration strategy: After each run, use the latest failure evidence to choose the next smallest diagnostic or fix.
Blocked stop condition: Stop if the test cannot be reproduced or required external services/data are unavailable; report attempts, evidence, blockers, and needed inputs.
Assumptions: Exact test command and retry count should be confirmed.
Draft /goal:
/goal ...
Please confirm or revise the draft before I produce the final `/goal`.
```
