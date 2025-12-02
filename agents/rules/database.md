---
globs:
  - '**/*.sql'
  - '**/migrations/**'
  - '**/db/**'
  - '**/database/**'
  - '**/models/**'
  - '**/schema/**'
  - '**/prisma/**'
  - '**/drizzle/**'
---

# Database Rules

## ✅ Language Rules
- **MANDATORY**: Respond in Vietnamese.
- **WITH EXPLANATION**: `**[English Term]** (Vietnamese description)`

## Quy Tắc Database

### Query Safety
- **ALWAYS parameterized queries** - KHÔNG concatenate
- **Prepared statements** cho repeated queries

```sql
-- ❌ Sai: SQL injection risk
SELECT * FROM users WHERE email = '${email}';

-- ✅ Đúng: Parameterized
SELECT * FROM users WHERE email = $1;
```

### Performance
- **Indexing strategy** - index columns thường query
- **EXPLAIN ANALYZE** trước khi deploy
- **Avoid N+1 queries** - sử dụng JOINs hoặc batch loading
- **Pagination** cho large datasets

### Migrations
- **Đặt tên descriptive**: `YYYYMMDD_HHMMSS_add_users_table.sql`
- **Reversible migrations** - luôn có rollback
- **Test migrations** trước khi apply production

```sql
-- Migration: 20250601_120000_add_user_status.sql

-- Up
ALTER TABLE users ADD COLUMN status VARCHAR(20) DEFAULT 'active';
CREATE INDEX idx_users_status ON users(status);

-- Down
DROP INDEX idx_users_status;
ALTER TABLE users DROP COLUMN status;
```

### Schema Design
- **Normalization** cho data integrity
- **Denormalize** chỉ khi có performance need rõ ràng
- **Foreign keys** với proper cascading
- **Timestamps** (`created_at`, `updated_at`) cho tất cả tables

### Naming Conventions
| Object | Convention | Example |
|--------|------------|---------|
| Tables | snake_case, plural | `users`, `order_items` |
| Columns | snake_case | `first_name`, `created_at` |
| Primary keys | `id` hoặc `table_id` | `id`, `user_id` |
| Foreign keys | `referenced_table_id` | `user_id`, `order_id` |
| Indexes | `idx_table_column` | `idx_users_email` |

### Connection Security
- **SSL/TLS** cho production connections
- **Connection pooling** để manage resources
- **Least privilege** cho database users

### Backup & Recovery
- Regular **automated backups**
- Test **restore procedures**
- **Point-in-time recovery** cho production

### Checklist Database Changes
- [ ] Queries parameterized?
- [ ] Indexes cho thường-queried columns?
- [ ] Migration có rollback?
- [ ] EXPLAIN ANALYZE chạy?
- [ ] Foreign keys có cascading đúng?
