# 📋 COMPLEXITY SCORING SYSTEM

## Complexity Score Calculation

```python
def calculate_complexity(task):
    score = 0
    
    # File scope
    if task.files_involved > 5: score += 3
    elif task.files_involved > 2: score += 2
    elif task.files_involved > 0: score += 1
    
    # Code changes
    if task.loc_changed > 500: score += 3
    elif task.loc_changed > 100: score += 2
    elif task.loc_changed > 20: score += 1
    
    # Domain complexity
    if task.involves_security: score += 2
    if task.involves_database: score += 1
    if task.involves_concurrency: score += 2
    if task.involves_architecture: score += 2
    
    # Debug complexity
    if task.failed_attempts > 2: score += 2
    if task.error_unclear: score += 1
    
    return score  # Max: 15

# Thresholds
ORACLE_THRESHOLD = 7
LIBRARIAN_THRESHOLD = 4  # for external code
SEARCH_THRESHOLD = 0     # always available
```

---

## Complexity Score → Subagent Mapping

| Score | Action | Subagent | Rationale |
|-------|--------|----------|-----------|
| 0-3 | Direct handling | Main Agent | Simple tasks |
| 4-6 | Consider subagent | Search + optional | Moderate complexity |
| 7-9 | Recommend Oracle | Oracle | High complexity |
| 10+ | Mandatory Oracle | Oracle (notify user) | Critical complexity |

---

## Scoring Breakdown

### File Scope Scoring
| Files Involved | Points |
|----------------|--------|
| 1 file | +1 |
| 2-5 files | +2 |
| >5 files | +3 |

### Code Changes Scoring
| Lines Changed | Points |
|---------------|--------|
| 1-20 LOC | +1 |
| 21-100 LOC | +2 |
| >500 LOC | +3 |

### Domain Complexity Scoring
| Domain | Points |
|--------|--------|
| Security | +2 |
| Database | +1 |
| Concurrency | +2 |
| Architecture | +2 |

### Debug Complexity Scoring
| Condition | Points |
|-----------|--------|
| Failed attempts > 2 | +2 |
| Error message unclear | +1 |

---

## Auto-Escalation Rules

```yaml
escalation:
  to_oracle:
    - score >= 7
    - domain == "security" AND score >= 5
    - failed_attempts >= 3
    
  to_librarian:
    - external_dependency == true AND score >= 4
    - github_reference == true
    
  notify_user:
    - score >= 10
    - message: "Task phức tạp, đang sử dụng Oracle để hỗ trợ"
```
