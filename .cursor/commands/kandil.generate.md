
# /kandil.generate

## Purpose
Generate test cases from requirements in the user's style.

## Syntax
```
/kandil.generate [path_to_requirements]
```
- Path relative to `feature-requirements/`. Examples: `login.md`, `ui/mock.png`.

## Supported Requirement Formats (MVP)
- Text: `md`, `txt`
- Images: `png`, `jpg` (OCR; accuracy depends on quality)
- `docx/pdf` — not supported in MVP (suggest conversion)

## Algorithm
1. Check for `config/user-rules.mdc`:
   - If exists — load and use only it.
   - If not — warn and use fallback `config/default-rules.md`.
2. Load requirements file from `feature-requirements/`. If file not found — show available files/subfolders.
3. Analyze requirements:
   - Text: functionality, roles, scenarios, constraints, data/validations.
   - Images: key UI elements, states, navigation.
4. Plan coverage: positive, negative, edge cases (if applicable).
5. Generate test cases strictly in rule format (tables/lists/headers, step style, terminology).
6. Save to `generated-test-cases/{YYYY-MM-DD}_{name}_test-cases.md`.
7. Output statistics and file path.

## Interactive Clarifications (with incomplete data)
Ask 2–3 questions, for example:
```
🤔 Clarifications:
1. Which user roles are critical?
2. Are there password/input field constraints?
3. Are negative scenarios needed (errors/validation)?
Respond or type "skip" to generate based on current data.
```

## Success Response Template
```
✅ Test cases created!
Total: {N} (positive {P}, negative {Nn}, edge {G})
File: generated-test-cases/{YYYY-MM-DD}_{name}_test-cases.md
Would you like to refine or add scenarios?
```

## Error Templates
- user-rules not found:
```
❌ Personal rules not found.
Use default-rules? (yes/no)
Or run: /kandil.init Full Name
```
- Requirements file not found:
```
❌ File not found: {path}
Available in feature-requirements/:
{list}
```
- Format not supported:
```
❌ Format not supported (docx/pdf).
Please convert to md/txt or png/jpg.
```

