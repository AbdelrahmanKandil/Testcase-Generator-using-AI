
# /kandil.clear

## Purpose
Reset to default settings. Deletes personal rules and optionally clears data.

## Syntax
```
/kandil.clear
```

## Algorithm
1. Warn about consequences and ask to choose an option:
   - Rules only (`user-rules.md`)
   - Rules + examples
   - Rules + requirements
   - Rules + output
   - Full cleanup (rules + examples + requirements + output)
   - Cancel
2. Delete selected items, keep empty folders with `.gitkeep`.
3. Report that fallback `config/default-rules.md` is now in use.

## Confirmation Template
```
⚠️ Cleanup:
- user-rules.md: delete
- examples: {yes/no}
- requirements: {yes/no}
- output: {yes/no}
Confirm your choice or cancel.
```

## Success Response Template
```
✅ Cleanup complete.
Deleted: {list}
Status: returned to default-rules.
For new style: add examples to test-case-examples/ and run /kandil.init
```

