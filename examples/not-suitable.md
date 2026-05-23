# Not Suitable Example

## User Request

```text
$draft-goal Change this code block so long lines wrap instead of showing a horizontal scrollbar.
```

## Expected Skill Behavior

The request is not suitable for `/goal` because it is a direct, one-shot UI styling change. The skill should not execute the request, should not produce a draft goal, and should instead suggest a clearer ordinary prompt.

## Example Output Shape

```text
Suitability: This does not need a `/goal` because it is a narrow one-shot CSS change with a clear implementation.
Suggested ordinary prompt:
Update the code block styles so long lines wrap within the container instead of showing a horizontal scrollbar. Set the relevant `pre`/`code` styles to avoid horizontal overflow, preserve readable whitespace, then verify the page has no horizontal scroll on desktop and mobile.
```
