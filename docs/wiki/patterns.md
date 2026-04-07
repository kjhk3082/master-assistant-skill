# Patterns — Coding Best Practices

> Auto-accumulated by Master Assistant. Add patterns here when you discover reusable solutions.

## Pattern Template

```
## [Pattern Name]
**Context**: When to use this pattern
**Solution**: How to implement it
**Example**: Code snippet or command
**Avoid**: Common mistakes
```

---

## Example: Safe API Call Pattern

**Context**: When calling external APIs that may timeout or fail
**Solution**: Always wrap in try/catch with timeout, log errors to gotchas.md
**Example**:
```javascript
try {
  const response = await fetch(url, { signal: AbortSignal.timeout(3000) });
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return await response.json();
} catch (err) {
  // Log to gotchas.md: "API timeout — always set 3s timeout"
  throw err;
}
```
**Avoid**: Naked `fetch()` without timeout or error handling
