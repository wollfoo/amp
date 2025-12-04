# Development Rules

## Core Principles
**YAGNI** (You Aren't Gonna Need It) | **KISS** (Keep It Simple) | **DRY** (Don't Repeat Yourself)

---

## File Management
- **Naming**: kebab-case, descriptive names
- **Size**: Keep files <200 lines, split when larger
- **Updates**: Modify existing files directly, no "enhanced" copies

## Code Quality
- Follow standards in `@doc/code-standards.md`
- Use try-catch error handling
- Cover security standards
- Prioritize functionality + readability over strict linting

## Pre-commit/Push
- Run linting before commit
- Run tests before push (fix failures, don't mock)
- Keep commits focused, use conventional format
- **NEVER** commit secrets/credentials

---

## Tool Hints

| Need | Use |
|------|-----|
| Latest docs lookup | **Librarian** for external libs |
| GitHub operations | `gh` CLI |
| Database debugging | `psql` CLI |
| Complex analysis | **Oracle** |
| Image/multimodal | MCP tools if configured |