---
globs:
  - '**/auth/**'
  - '**/security/**'
  - '**/login/**'
  - '**/password/**'
  - '**/jwt/**'
  - '**/session/**'
  - '**/oauth/**'
---

# Security Rules

## ✅ Language Rules
- **MANDATORY**: Respond in Vietnamese.
- **WITH EXPLANATION**: `**[English Term]** (Vietnamese description)`

## Quy Tắc Bảo Mật

### Authentication (Xác thực)

#### Password Handling
- **bcrypt** với rounds ≥12 cho password hashing
- KHÔNG lưu plaintext passwords
- Implement **rate limiting** cho login attempts

```python
# ✅ Đúng: bcrypt với salt rounds phù hợp
import bcrypt
password_hash = bcrypt.hashpw(password.encode(), bcrypt.gensalt(rounds=12))
```

#### JWT Best Practices
- **Short expiration** (15-30 phút cho access tokens)
- **Refresh token rotation** 
- Validate **issuer**, **audience**, **expiration**
- Store secrets trong environment variables

### Authorization (Phân quyền)
- **RBAC** (Role-Based Access Control) cho permissions
- **Principle of Least Privilege** (quyền tối thiểu)
- Check authorization ở **server-side**

### Input Validation
- **Validate ALL user input** (server-side)
- **Parameterized queries** - KHÔNG concatenate SQL
- **Sanitize output** để prevent XSS

```typescript
// ❌ Sai: SQL injection risk
const query = `SELECT * FROM users WHERE id = '${userId}'`;

// ✅ Đúng: Parameterized query
const query = 'SELECT * FROM users WHERE id = $1';
await db.query(query, [userId]);
```

### Secrets Management
- KHÔNG hardcode secrets trong code
- Sử dụng **environment variables**
- KHÔNG commit `.env` files

### HTTPS
- Enforce **HTTPS** trong production
- Proper **TLS** configuration
- HSTS headers enabled

### Logging
- KHÔNG log sensitive data (passwords, tokens, PII)
- Log security events (failed logins, permission denials)
- Implement log rotation

### Checklist Khi Review Security Code
- [ ] Passwords hashed với bcrypt ≥12 rounds?
- [ ] JWT tokens có expiration ngắn?
- [ ] Input validated server-side?
- [ ] Queries parameterized?
- [ ] Secrets trong env vars?
- [ ] HTTPS enforced?
- [ ] Rate limiting implemented?
