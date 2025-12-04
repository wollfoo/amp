---
globs:
  - '**/*.js'
  - '**/*.ts'
  - '**/*.jsx'
  - '**/*.tsx'
---

# Code Standards

## File Structure
- **Naming**: kebab-case, descriptive names
- **Size**: Keep files <200 lines, split when larger
- **Organization**: Group by feature/module

## Naming Conventions

| Type | Style | Example |
|------|-------|---------|
| Variables/Functions | camelCase | `userName`, `getUserById` |
| Classes/Components | PascalCase | `UserService`, `AuthProvider` |
| Constants | UPPER_SNAKE | `MAX_RETRIES`, `API_URL` |
| Files | kebab-case | `user-service.js` |

## Code Style

### General
- 2 spaces indentation
- Single quotes for strings
- Semicolons required
- Max line length: 100 chars

### Comments
- JSDoc for public functions
- Explain WHY, not WHAT
- TODO format: `// TODO(name, date): description`

### Error Handling
```javascript
try {
  await operation();
} catch (error) {
  logger.error('Context message', { error: error.message });
  throw new AppError('User-friendly message', error);
}
```

## Security
- Validate ALL inputs
- Use parameterized queries
- Never log secrets/PII
- bcrypt rounds ≥12

## Testing
- Test file: `*.test.js` or `*.spec.js`
- Coverage target: >80%
- Test both success and error paths

## Commits
Format: `<type>(<scope>): <description>`

Types: `feat`, `fix`, `docs`, `refactor`, `test`, `chore`

---

**Full reference**: See original code-standards.md in version history if needed.
