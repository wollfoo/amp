# 🤖 SUBAGENT ACTIVATION RULES

## 📊 Activation Priority Matrix

| Priority | Trigger Condition | Subagent | Confidence |
|----------|-------------------|----------|------------|
| P0 | Explicit "use oracle/librarian" | Specified | 100% |
| P1 | Complex debugging (>3 files) | Oracle | 95% |
| P2 | External library/repo research | Librarian | 90% |
| P3 | Architecture planning | Oracle | 85% |
| P4 | Code review (>100 LOC) | Oracle | 80% |
| P5 | Multi-repo search | Librarian | 85% |

---

## 🧠 ORACLE ACTIVATION RULES

### MANDATORY Triggers (Bắt buộc kích hoạt)

```yaml
triggers:
  explicit:
    - "use oracle"
    - "ask oracle"  
    - "oracle review"
    - "consult oracle"
    - "oracle analyze"
    - "oracle debug"
    - "oracle plan"
    
  implicit_high_confidence:  # Auto-trigger với confidence ≥ 85%
    - complexity_score >= 7
    - files_involved >= 3
    - bug_reproduction_failed: true
    - architecture_change: true
    - security_review_needed: true
    
  proactive:  # Trigger sau các action liên quan
    - after: "failed test 3+ times"
    - after: "circular dependency detected"
    - after: "performance regression found"
    - after: "security vulnerability scan"
```

### Oracle Examples

```markdown
<example id="oracle-debug">
Context: User gặp bug phức tạp, đã thử fix 2 lần không thành công
user: "Bug này fix hoài không được, không hiểu tại sao"
assistant: "Tôi sẽ consult Oracle để phân tích sâu root cause của bug này"
<commentary>
Bug phức tạp với failed attempts → Trigger Oracle cho deep analysis
</commentary>
</example>

<example id="oracle-review">
Context: PR lớn với nhiều thay đổi architecture
user: "Review PR này giúp tôi"
assistant: "PR này có nhiều thay đổi kiến trúc, tôi sẽ dùng Oracle để review kỹ"
<commentary>
Architecture changes → Oracle có expertise để review comprehensive
</commentary>
</example>

<example id="oracle-plan">
Context: User cần implement feature mới phức tạp
user: "Tôi cần implement real-time collaboration, nên thiết kế thế nào?"
assistant: "Đây là feature phức tạp, tôi sẽ nhờ Oracle lên plan chi tiết"
<commentary>
Complex feature planning → Oracle's reasoning depth is valuable
</commentary>
</example>
```

---

## 📚 LIBRARIAN ACTIVATION RULES

### MANDATORY Triggers

```yaml
triggers:
  explicit:
    - "use librarian"
    - "ask librarian"
    - "librarian lookup"
    - "librarian search"
    
  implicit_high_confidence:  # Auto-trigger với confidence ≥ 80%
    - external_repo_reference: true
    - github_url_mentioned: true
    - library_documentation_needed: true
    - "how does [library] work internally"
    - "implementation of [framework feature]"
    
  proactive:
    - after: "import error from external package"
    - after: "version mismatch detected"
    - after: "deprecated API warning"
```

### Librarian Examples

```markdown
<example id="librarian-lookup">
Context: User cần hiểu internal implementation của library
user: "React useEffect hoạt động như thế nào internally?"
assistant: "Tôi sẽ dùng Librarian để lookup implementation trong React source code"
<commentary>
External library internals → Librarian có access GitHub repos
</commentary>
</example>

<example id="librarian-research">
Context: User gặp error từ third-party library
user: "Zod đang throw error này, không hiểu tại sao"
assistant: "Để Librarian research Zod source code để hiểu error handling"
<commentary>
Third-party error → Librarian có thể trace source
</commentary>
</example>

<example id="librarian-compare">
Context: User cần so sánh implementations
user: "Next.js và Remix handle routing khác nhau thế nào?"
assistant: "Tôi sẽ dùng Librarian để phân tích cả 2 frameworks"
<commentary>
Multi-repo comparison → Librarian's strength
</commentary>
</example>
```

---

## 🔍 SEARCH SUBAGENT (Auto-activated)

```yaml
triggers:
  always_on:
    - codebase_query: true
    - file_location_needed: true
    - implementation_lookup: true
    - "where is X defined"
    - "find all usages of Y"
    - "locate the Z component"
```

---

## ⚡ PROACTIVE ACTIVATION TRIGGERS

### After-Action Triggers

```yaml
proactive_triggers:
  oracle:
    - event: "test_failed_repeatedly"
      count: 3
      action: "Suggest Oracle for deep debugging"
      
    - event: "lint_errors_complex"
      count: 10
      action: "Suggest Oracle for refactoring strategy"
      
    - event: "circular_import_detected"
      action: "Trigger Oracle for architecture review"
      
    - event: "security_scan_findings"
      severity: "high"
      action: "Mandatory Oracle security review"
      
  librarian:
    - event: "external_package_error"
      action: "Suggest Librarian for source investigation"
      
    - event: "deprecation_warning"
      action: "Suggest Librarian for migration guide lookup"
      
    - event: "version_conflict"
      action: "Trigger Librarian for compatibility research"
```

### Pre-emptive Triggers

```yaml
preemptive_triggers:
  oracle:
    - condition: "PR size > 500 LOC"
      action: "Recommend Oracle review before merge"
      
    - condition: "New architectural pattern introduced"
      action: "Suggest Oracle for pattern validation"
      
  librarian:
    - condition: "New dependency added"
      action: "Suggest Librarian for dependency analysis"
      
    - condition: "Major version upgrade"
      action: "Recommend Librarian for breaking changes review"
```
