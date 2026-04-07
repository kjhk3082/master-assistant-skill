# Gotchas — Lessons Learned the Hard Way

> Auto-accumulated by Master Assistant. Add gotchas here when you encounter bugs or surprises.

## Gotcha Template

```
## [Short Description]
**Symptom**: What went wrong
**Root Cause**: Why it happened
**Fix**: How to resolve it
**Prevention Rule**: Add to CLAUDE.md
```

---

## Example: DB Timestamp Timezone Mismatch

**Symptom**: Timestamps were off by 9 hours in production
**Root Cause**: Server stored UTC, frontend displayed without conversion
**Fix**: Always use `toISOString()` for storage, `toLocaleString()` for display
**Prevention Rule**: `CLAUDE.md` → "All DB timestamps MUST be stored in UTC (ISO 8601)"
