markdown
# Default Rules - Basic Test Case Writing Guidelines (fallback)

Used when `config/user-rules.mdc` has not yet been created after `/kandil.init`.

## Universal Structure
### Required Fields
- **ID**: unique identifier (format `TC-001`, incremental).
- **Title**: brief description of the check.
- **Preconditions**: initial system state (numbered list).
- **Steps**: numbered actions (imperative mood).
- **Expected Result**: verifiable outcomes (bulleted list `-`).
- **Priority**: `High` / `Medium` / `Low`.
- **Author**: full name from `/kandil.init` parameter.

### Basic Format (Markdown)
```
## Test Case: [Title]

**ID**: TC-001  
**Priority**: High  
**Author**: [Full Name]

### Preconditions
1. [Condition 1]
2. [Condition 2]

### Steps
1. [Step 1]
2. [Step 2]

### Expected Result
- [Result 1]
- [Result 2]
```

## Style
- Verbs in steps — imperative mood: "Click", "Enter", "Verify".
- Step numbering: `1.`, `2.`, `3.`.
- Expected results — bulleted list `-`.
- Preconditions — numbered list.

## ID Generation
- Default format: `TC-###` with increment.
- If `user-rules.mdc` exists, use its pattern.

## Metadata
- Priority: `High` / `Medium` / `Low`.
- Author: from `/kandil.init` parameter.
- Default status is not set (can be added in user-rules).

## Supported Formats (MVP)
- Text: `md`, `txt`.
- Requirement images: `png`, `jpg` (OCR, accuracy depends on quality).
- `docx/pdf` — not supported in MVP; prompt user to convert when attempted.

## When to Update
- These rules are fallback only. After `/kandil.init`, always use `user-rules.mdc`.

