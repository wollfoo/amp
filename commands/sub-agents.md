---
description: Orchestrate AMP's 3 specialized subagents for complex tasks
argument-hint: <task-description>
allowed-tools: Read, Write, Edit, Grep, Glob, Bash
---

# AMP Subagent Orchestration

**Task**: `$ARGUMENTS`

---

## 3 Specialized Subagents

| Subagent | Model | Purpose |
|----------|-------|---------|
| 🔍 **Search** | Claude Haiku 4.5 | Fast, accurate codebase retrieval |
| 🧠 **Oracle** | GPT-5.1 | Complex reasoning & planning on code |
| 📚 **Librarian** | Claude Sonnet 4.5 | Large-scale retrieval & research on external code |

---

### 🔍 Search (Claude Haiku 4.5)
> Fast, accurate codebase retrieval

- **Performance**: 50% faster, ~3X cheaper
- **Invocation**: **Auto-spawn** — AMP tự động gọi khi cần tìm context
- **Tools**: Read-only (không edit files)

**Use cases**: Locate code, find files, answer "where is X?"

---

### 🧠 Oracle (GPT-5.1)
> Complex reasoning & planning on code

- **Invocation**: Auto hoặc explicit request
- **Trade-off**: Slower + expensive, dùng khi cần reasoning depth

**Use cases**:
- Planning (refactor, architecture)
- Debugging (complex bugs, log analysis)
- Code review (logic changes, commits)

**Prompts**:
```
"Use the oracle to review the last commit's changes"
"Ask the oracle whether there isn't a better solution"
"Use the oracle as much as possible, since it's smart"
"Use the oracle to analyze and design better architecture"
```

---

### 📚 Librarian (Claude Sonnet 4.5)
> Large-scale retrieval & research on external code

- **Scope**: All public GitHub + authorized private repos
- **Limit**: Default branch only
- **Output**: In-depth, detailed explanations
- **Requires**: [GitHub connection](https://ampcode.com/settings)

**Use cases**:
- Framework/library internals
- Multi-repo search
- Open-source examples
- Dependency debugging

**Prompts**:
```
"Use the Librarian to lookup how React's useEffect is implemented"
"Ask the Librarian to explain why we're getting this error from Zod"
"Use the Librarian to investigate [service] - any recent API changes?"
```

---

## Orchestration Flow

```
$ARGUMENTS
    │
    ▼
┌─────────────────────────────────────────────────┐
│              MAIN AGENT (Sonnet 4)              │
│                                                 │
│  ┌─────────┐  ┌─────────┐  ┌─────────────────┐ │
│  │ Search  │  │ Oracle  │  │    Librarian    │ │
│  │ (auto)  │  │ (reason)│  │ (external code) │ │
│  └─────────┘  └─────────┘  └─────────────────┘ │
└─────────────────────────────────────────────────┘
```

### Workflow

1. **Discovery**: Search → locate relevant code
2. **External Research**: Librarian → investigate dependencies/libraries
3. **Analysis**: Oracle → deep reasoning, plan approach
4. **Implementation**: Main agent executes with Search support
5. **Validation**: Oracle → review changes

---

## Quick Reference

| Need | Subagent | Prompt Pattern |
|------|----------|----------------|
| Find code | Search | *(auto)* |
| Debug complex bug | Oracle | "Use the oracle to..." |
| Review logic | Oracle | "Ask the oracle to review..." |
| Library internals | Librarian | "Ask the Librarian to lookup..." |
| Cross-repo research | Librarian | "Use the Librarian to investigate..." |

---

**Begin orchestration for**: `$ARGUMENTS`
