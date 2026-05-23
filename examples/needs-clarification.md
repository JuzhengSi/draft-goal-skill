# Needs Clarification Example

## User Request

```text
$draft-goal Make the app faster without breaking anything.
```

## Expected Skill Behavior

The request might be suitable for `/goal`, but it is too vague to draft safely. The skill should ask clarifying questions before producing a draft.

## Example First Response Shape

```text
Suitability: This may be appropriate for a `/goal` because performance work can require repeated measurement and iteration, but the success criteria are not defined yet.
Known fields:
- Result: The app should be faster.
- Validation surface: Missing.
- Constraints: Do not break existing behavior.
- Boundaries: Missing.
- Iteration strategy: Missing.
- Blocked stop condition: Missing.
Open questions:
1. Which performance metric should define success, such as p95 latency, build time, page load time, or memory usage?
2. Which command, benchmark, trace, or monitoring source should verify the improvement?
3. Which parts of the app may Codex modify, and which areas are out of scope?
```
