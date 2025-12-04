# System Architecture

> Amp CLI with Oracle, Librarian, and Task subagents

## Core Components

```
User Request
    ↓
┌─────────────────┐
│   Amp CLI       │  Main agent (Claude Opus 4.5)
└────────┬────────┘
         ↓
    ┌────┴────┬─────────────┐
    ↓         ↓             ↓
┌───────┐ ┌─────────┐ ┌──────────┐
│Oracle │ │Librarian│ │  Task    │
│(GPT-5)│ │(GitHub) │ │(Subagent)│
└───────┘ └─────────┘ └──────────┘
```

## Tool Architecture

| Tool | Purpose | Activation |
|------|---------|------------|
| **Oracle** | Complex reasoning, debugging | Auto or explicit |
| **Librarian** | GitHub code search | Explicit request |
| **Task** | Parallel isolated work | Auto or "parallel" |
| **MCP** | External integrations | Config-based |

## File Organization

```
amp/
├── AGENTS.md              ← Entry point
├── rules/                 ← Behavioral rules
├── workflows/             ← Process workflows
└── docs/                  ← Reference docs
```

## Data Flow

```
User → Amp CLI → Parse Command → Execute Workflow
                       ↓
         ┌─────────────┴─────────────┐
         ↓                           ↓
   Simple task                Complex task
   (Main agent)               (Oracle/Subagent)
         ↓                           ↓
   Execute directly          Spawn tool/subagent
         ↓                           ↓
   Return result             Collect & summarize
```

## Integration Points

- **MCP Servers**: See `@docs/mcp-servers.md`
- **Subagents**: Via Task tool
- **External**: GitHub, CLI tools

---

**Note**: This is optimized for Amp CLI. Previous ClaudeKit architecture archived.
