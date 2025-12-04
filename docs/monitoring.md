# 📊 METRICS & MONITORING

## Key Performance Indicators (KPIs)

```yaml
metrics:
  activation_rate:
    oracle:
      target: ">= 80% when complexity >= 7"
      
    librarian:
      target: ">= 90% when external code referenced"
      
  success_rate:
    oracle:
      target: ">= 85% task completion"
      
    librarian:
      target: ">= 90% information found"
      
  latency:
    oracle:
      p50: "< 30s"
      p99: "< 90s"
      
    librarian:
      p50: "< 15s"
      p99: "< 45s"
      
  cost_efficiency:
    oracle_calls_per_session: "track"
    librarian_calls_per_session: "track"
    unnecessary_calls: "minimize"
```

---

## Logging Schema

```typescript
interface SubagentActivationLog {
  // Identity
  session_id: string;
  thread_id: string;
  timestamp: string;
  
  // Activation details
  subagent: "oracle" | "librarian" | "search";
  trigger_type: "explicit" | "implicit" | "proactive";
  trigger_phrase?: string;
  complexity_score: number;
  confidence: number;
  
  // Context
  user_query: string;
  files_involved: string[];
  task_type: string;
  
  // Result
  status: "success" | "failed" | "timeout" | "fallback";
  duration_ms: number;
  fallback_used: boolean;
  fallback_reason?: string;
  
  // Quality
  user_feedback?: 1 | 2 | 3 | 4 | 5;
  task_completed: boolean;
}
```

---

## Alert Rules

```yaml
alerts:
  critical:
    - name: "oracle_timeout_spike"
      condition: "oracle_timeout_rate > 10% for 5 minutes"
      action: "PagerDuty + auto-fallback"
      
    - name: "librarian_error_spike"
      condition: "librarian_error_rate > 15% for 5 minutes"
      action: "PagerDuty + circuit-breaker"
      
  warning:
    - name: "low_oracle_activation"
      condition: "oracle_activation_rate < 50% when complexity >= 7"
      action: "Slack notification + log review"
      
    - name: "unnecessary_subagent_calls"
      condition: "unnecessary_call_rate > 20%"
      action: "Slack notification + threshold review"
      
  info:
    - name: "daily_cost_report"
      schedule: "0 9 * * *"
      action: "Email summary to team"
```

---

## Dashboard Panels

```yaml
dashboard:
  panels:
    - name: "Activation Rates"
      metrics: [oracle_activation_rate, librarian_activation_rate]
      visualization: "time_series"
      
    - name: "Success Rates"
      metrics: [oracle_success_rate, librarian_success_rate]
      visualization: "gauge"
      
    - name: "Latency Distribution"
      metrics: [oracle_latency_p50, oracle_latency_p99]
      visualization: "histogram"
      
    - name: "Cost Tracking"
      metrics: [daily_oracle_cost, daily_librarian_cost]
      visualization: "bar_chart"
```
