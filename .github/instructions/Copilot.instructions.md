---
applyTo: '**'
---
Provide project context and coding guidelines that AI should follow when generating code, answering questions, or reviewing changes.
# Kandil - Test Case Generation Instructions for GitHub Copilot

## Purpose
Generate test cases from requirements in the user's style.

---

## Syntax (Manual Prompt)
When asking Copilot to generate test cases, use:
```
Generate test cases from: [path_to_requirements]
```
- Path relative to `feature-requirements/`. Examples: `login.md`, `ui/mock.png`.

---

## Supported Requirement Formats
| Format | Support | Notes |
|--------|---------|-------|
| `.md`, `.txt` | ✅ Full | Text-based requirements |
| `.png`, `.jpg` | ✅ Limited | OCR; accuracy depends on quality |
| `.docx`, `.pdf` | ❌ No | Convert to md/txt first |

---

## Algorithm

### Step 1: Load Rules
1. Check for `config/user-rules.mdc`:
   - If exists → load and use only it
   - If not → warn and use fallback `config/default-rules.md`

### Step 2: Load Requirements
1. Load requirements file from `feature-requirements/`
2. If file not found → list available files/subfolders

### Step 3: Analyze Requirements
**For Text Files:**
- Identify functionality, user roles, scenarios
- Extract constraints, data validations
- Note acceptance criteria

**For Images:**
- Identify key UI elements
- Recognize states and navigation
- Extract visible text/labels

### Step 4: Plan Test Coverage
| Type | Description |
|------|-------------|
| Positive | Happy path scenarios that should work |
| Negative | Error handling, invalid inputs |
| Edge Cases | Boundary values, limits, special conditions |

### Step 5: Generate Test Cases
Use this table format:

| # | Title | Preconditions | Steps | Expected Result | Priority |
|---|-------|---------------|-------|-----------------|----------|
| 1 | [Action] [Object] | [Required state] | 1. [Verb] [action]<br>2. [Verb] [action] | [Expected outcome] | High/Medium/Low |

**Style Rules:**
- Use imperative verbs: Click, Enter, Verify, Check, Select, Navigate
- Keep titles concise and descriptive
- Steps should be numbered and atomic
- One expected result per test case

### Step 6: Save Output
Save to: `generated-test-cases/{YYYY-MM-DD}_{name}_test-cases.md`

Example: `generated-test-cases/2026-01-07_login_test-cases.md`

### Step 7: Output Statistics
Report total count and breakdown by type.

---

## Interactive Clarifications

When requirements are incomplete, ask 2-3 questions:

```
🤔 Clarifications:
1. Which user roles are critical?
2. Are there password/input field constraints?
3. Are negative scenarios needed (errors/validation)?

Respond or type "skip" to generate based on current data.
```

---

## Response Templates

### Success Response
```
✅ Test cases created!
Total: {N} (positive {P}, negative {Nn}, edge {E})
File: generated-test-cases/{YYYY-MM-DD}_{name}_test-cases.md

Would you like to refine or add scenarios?
```

### Error: Rules Not Found
```
❌ Personal rules not found.
Use default-rules? (yes/no)
Or create config/user-rules.mdc with your preferences.
```

### Error: Requirements File Not Found
```
❌ File not found: {path}
Available in feature-requirements/:
{list of files}
```

### Error: Format Not Supported
```
❌ Format not supported (docx/pdf).
Please convert to md/txt or png/jpg.
```

---

## Test Case Template

```markdown
# Test Cases: {Feature Name}

**Generated:** {YYYY-MM-DD}
**Source:** {requirements file}
**Author:** {name from user-rules or "Copilot"}

## Summary
- Total: {N}
- Positive: {P}
- Negative: {Nn}
- Edge Cases: {E}

## Test Cases

| # | Title | Preconditions | Steps | Expected Result | Priority |
|---|-------|---------------|-------|-----------------|----------|
| 1 | | | | | |
| 2 | | | | | |
```

---

## Example Usage

**User prompt:**
```
Generate test cases from: login.md
```

**Expected output:**
```markdown
# Test Cases: Login Feature

**Generated:** 2026-01-07
**Source:** feature-requirements/login.md
**Author:** Copilot

## Summary
- Total: 6
- Positive: 2
- Negative: 3
- Edge Cases: 1

## Test Cases

| # | Title | Preconditions | Steps | Expected Result | Priority |
|---|-------|---------------|-------|-----------------|----------|
| 1 | Login with valid credentials | User is registered | 1. Navigate to login page<br>2. Enter valid email<br>3. Enter valid password<br>4. Click Login button | User is redirected to dashboard | High |
| 2 | Login with invalid password | User is registered | 1. Navigate to login page<br>2. Enter valid email<br>3. Enter wrong password<br>4. Click Login button | Error message "Invalid credentials" displayed | High |
```

---

## Priority Guidelines

| Priority | When to Use |
|----------|-------------|
| High | Core functionality, security, data integrity |
| Medium | Important features, common user flows |
| Low | Edge cases, cosmetic issues, rare scenarios |