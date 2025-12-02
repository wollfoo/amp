# 🔄 FALLBACK MECHANISMS

## Fallback Chain

```
Primary Subagent Failed/Timeout
    │
    ▼
┌─────────────────────────────────────────┐
│ Fallback Decision Tree                   │
├─────────────────────────────────────────┤
│                                          │
│ Oracle Failed?                           │
│ ├─► Retry with simpler context           │
│ ├─► Fallback to Librarian (if external)  │
│ └─► Fallback to Main Agent + Search      │
│                                          │
│ Librarian Failed?                        │
│ ├─► Retry with specific repo scope       │
│ ├─► Fallback to web_search + read_page   │
│ └─► Manual GitHub navigation suggestion  │
│                                          │
│ Search Failed?                           │
│ ├─► Expand search scope                  │
│ ├─► Use Grep with broader patterns       │
│ └─► Request user clarification           │
└─────────────────────────────────────────┘
```

---

## Timeout Handling

```yaml
timeouts:
  oracle:
    soft: 60s   # Warn user
    hard: 120s  # Abort + fallback
    
  librarian:
    soft: 30s
    hard: 60s
    
  search:
    soft: 10s
    hard: 20s

fallback_actions:
  on_timeout:
    - log_event: true
    - notify_user: "Subagent đang chậm, đang thử phương án khác"
    - execute_fallback: true
```

---

## Retry Strategy

```yaml
retry_config:
  oracle:
    max_retries: 2
    backoff: exponential
    initial_delay: 5s
    max_delay: 30s
    
  librarian:
    max_retries: 3
    backoff: linear
    delay: 5s
    
  search:
    max_retries: 2
    backoff: none
    delay: 2s
```

---

## Fallback Matrix

| Primary | Failure Type | Fallback 1 | Fallback 2 | Final |
|---------|--------------|------------|------------|-------|
| Oracle | Timeout | Retry (simpler) | Librarian | Main Agent |
| Oracle | Error | Librarian | Main + Search | User escalation |
| Librarian | Timeout | Retry (scoped) | web_search | Manual lookup |
| Librarian | Not Found | web_search | read_web_page | User clarification |
| Search | No Results | Grep (broader) | glob patterns | User clarification |

---

## Error Recovery

```yaml
error_recovery:
  rate_limit:
    action: "backoff_and_retry"
    delay: 60s
    
  network_error:
    action: "retry_with_timeout"
    max_attempts: 3
    
  invalid_response:
    action: "fallback_to_next"
    log: true
    
  context_overflow:
    action: "compact_and_retry"
    compression_ratio: 0.5
```
