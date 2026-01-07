
# /kandil.init

## Purpose
Initialize personal rules based on user examples. Creates `config/user-rules.mdc`, describing the exact structure, style, and terminology.

## Syntax
```
/kandil.init [Author]
```
- `[Author]` — Full name format `Last First`; will be used as test case author.

## Supported Example Input Formats (MVP)
- Text: `md`, `txt`
- Images: `png`, `jpg` (OCR; accuracy depends on quality)
- `docx/pdf` — not supported in MVP (suggest conversion)

## Algorithm
1. Check for files in `test-case-examples/`. If folder is empty → return error and ask for 3–5 examples.
2. Read ALL supported files from `test-case-examples/`.
3. Analyze:
   - Test case structure: sections, order, tables/lists/headers.
   - Field formats: ID, Title, Preconditions, Steps, Expected Results, Metadata.
   - Style: imperative/infinitive, terminology, detail level, step numbering, result format.
   - Patterns: priorities, status, author, ID format, test data.
4. Generate `config/user-rules.mdc` with:
   - Metadata: author, creation date, number of examples.
   - Exact table/section structure (as in examples).
   - Writing style for steps/results/preconditions.
   - Patterns for IDs, priorities, statuses, terminology.
5. Output analysis summary to chat.

## Success Response Template
```
✅ Initialization complete!
Examples analyzed: {N}
Detected structure:
- Format: {tables/lists/...}
- Sections: {list}
- Step style: {imperative/infinitive/...}
- Author: {Full Name}

Personal rules created: config/user-rules.mdc
You can now use /kandil.generate
```

## Error Templates
- Examples not found:
```
❌ Examples not found.
Place 3–5 files in test-case-examples/ (md/txt/png/jpg).
Then run: /kandil.init Full Name
```
- Format not supported:
```
❌ File format not supported (docx/pdf).
Please convert to md/txt or png/jpg.
```

