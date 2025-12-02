---
globs:
  - '**/*.test.*'
  - '**/*.spec.*'
  - '**/__tests__/**'
  - '**/test/**'
  - '**/tests/**'
---

# Testing Rules

## ✅ Language Rules
- **MANDATORY**: Respond in Vietnamese.
- **WITH EXPLANATION**: `**[English Term]** (Vietnamese description)`

## Quy Tắc Testing

### Coverage Targets
| Loại | Target |
|------|--------|
| Unit tests | ≥80% |
| Integration tests | ≥70% |
| Critical paths | 100% |

### Test Structure (AAA Pattern)
```typescript
describe('UserService', () => {
  describe('createUser', () => {
    it('should create user with valid data', async () => {
      // Arrange (Chuẩn bị)
      const userData = { name: 'Test', email: 'test@example.com' };
      
      // Act (Thực hiện)
      const result = await userService.createUser(userData);
      
      // Assert (Kiểm tra)
      expect(result.id).toBeDefined();
      expect(result.name).toBe('Test');
    });
  });
});
```

### Naming Convention
- `should [action] when [condition]`
- `should throw [error] when [invalid condition]`

### Best Practices

#### Test Isolation
- Mỗi test **độc lập** - không phụ thuộc test khác
- **Reset state** giữa các tests
- Sử dụng **mocks/stubs** cho external dependencies

#### Edge Cases
Luôn test:
- Empty/null inputs
- Boundary values
- Error conditions
- Concurrent operations

#### Test Types
```
Unit Tests (nhanh, isolated)
    ↓
Integration Tests (APIs, DB)
    ↓
E2E Tests (user flows)
```

### Anti-patterns (Tránh)
- ❌ Test implementation details
- ❌ Flaky tests (intermittent failures)
- ❌ Tests phụ thuộc thứ tự
- ❌ Hard-coded dates/times
- ❌ Shared mutable state

### Tools by Language
| Language | Framework |
|----------|-----------|
| JavaScript/TypeScript | Jest, Vitest |
| Python | pytest |
| Go | testing package |
| Rust | cargo test |

### Mocking Guidelines
- Mock external services, databases
- KHÔNG mock internal implementation
- Use factories cho test data
