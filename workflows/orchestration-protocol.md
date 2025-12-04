# Orchestration Protocol

> Ref: [Amp Manual](https://ampcode.com/manual#tools) | [GPT-5 Oracle](https://ampcode.com/news/gpt-5-oracle)

## Auto-Activation Directives

**IMPORTANT**: Proactively use Oracle/Librarian without waiting for user request when conditions match.

### Oracle (GPT-5) — AUTO when:
- [ ] Debugging fails after 2+ attempts
- [ ] Code review involves >3 files or >200 LOC
- [ ] Architecture/refactoring decision needed
- [ ] Security-sensitive code changes
- [ ] Performance optimization analysis
- [ ] Complex planning required

### Librarian — AUTO when:
- [ ] External library/framework error encountered
- [ ] GitHub URL or repo name mentioned
- [ ] "How does [library] work internally" pattern
- [ ] Version mismatch or deprecated API warning
- [ ] Cross-repository research needed

### Task Subagents — AUTO when:
- [ ] Independent parallel tasks identified
- [ ] Extensive output expected (tests, builds)
- [ ] Multi-step isolated operations

---

## Tool Reference

| Tool | Model | Best For |
|------|-------|----------|
| **Oracle** | GPT-5 | Planning, debugging, complex reasoning |
| **Librarian** | Subagent | GitHub code search, framework internals |
| **Task** | Subagent | Parallel isolated work |

---

## Usage Patterns

### Oracle
```
"Use oracle to [analyze/review/debug/plan] ..."
"Ask oracle whether there's a better solution"
"Work with oracle to refactor [code]"
```

### Librarian
```
"Ask librarian to investigate [library] source"
"Use librarian to search [repo] for [pattern]"
"Librarian lookup how [framework] handles [feature]"
```

---

## Decision Flow

```
Task Received
    ↓
Check auto-activation conditions above
    ↓
Match Oracle? → Use oracle tool
Match Librarian? → Use librarian subagent  
Match Task? → Spawn task subagent
None? → Handle directly
```

---

## Self-Activation Examples

**Bug debugging**:
> "Đã thử fix 2 lần không thành công → Sẽ consult Oracle để phân tích root cause"

**External library error**:
> "Gặp error từ Zod → Sẽ dùng Librarian để research source code"

**Complex refactoring**:
> "Refactor 5+ files → Sẽ nhờ Oracle lên plan chi tiết trước khi implement"

---

**Note**: Không chờ user request. Proactively activate khi match conditions.