# Primary Workflow

> Token-efficient workflow aligned with [Amp Manual](https://ampcode.com/manual)

## Principles
- **YAGNI** | **KISS** | **DRY**
- Keep tasks focused, one per thread
- Abandon cluttered threads, start fresh

---

## 1. Planning
- Break large tasks into sub-tasks
- Use **Oracle** for complex planning: "Use oracle to plan how to implement X"
- Research before coding: read relevant files, understand context

## 2. Implementation
- Write clean, maintainable code
- Update existing files directly (no "enhanced" copies)
- Run compile/build after changes
- Use **Task subagents** for parallel independent work

## 3. Testing
- Run tests before push
- Fix failing tests (no mocks/cheats to pass)
- Use subagent for extensive test output

## 4. Review
- Use **Oracle** for code review: "Ask oracle to review the code"
- Follow coding standards in `@doc/code-standards.md`

## 5. Debugging
- Use **Oracle** for complex bugs: "Use oracle to debug this"
- Use **Librarian** for external library issues
- Check git diff, logs, error messages

---

## Tool Usage

| Task | Tool |
|------|------|
| Complex reasoning | `oracle` |
| External code research | `librarian` |
| Parallel work | `Task subagent` |
| Database queries | `psql` via bash |
| GitHub operations | `gh` via bash |