---
globs:
  - '**/*.ts'
  - '**/*.tsx'
---

# TypeScript Conventions

## ✅ Language Rules
- **MANDATORY**: Respond in Vietnamese.
- **WITH EXPLANATION**: `**[English Term]** (Vietnamese description)`

## Quy Tắc TypeScript

### Strict Mode
- Luôn enable `strict: true` trong tsconfig.json
- Không dùng `any` - sử dụng `unknown` với type guards

### Type Definitions
- **Interfaces** (giao diện) cho object shapes
- **Type aliases** (bí danh kiểu) cho unions, intersections, utility types
- **Const assertions** (`as const`) cho immutable values
- **Readonly modifiers** cho properties không thay đổi

### Advanced Types
- **Discriminated unions** (union phân biệt) cho exhaustive checking
- **Generic constraints** (`<T extends Base>`) cho type safety
- **Mapped types** cho transformations
- **Template literal types** cho string patterns

### Best Practices
```typescript
// ✅ Đúng: Interface cho object shape
interface User {
  readonly id: string;
  name: string;
  email: string;
}

// ✅ Đúng: Type guard
function isUser(value: unknown): value is User {
  return typeof value === 'object' && value !== null && 'id' in value;
}

// ✅ Đúng: Const assertion
const STATUS = {
  ACTIVE: 'active',
  INACTIVE: 'inactive',
} as const;

// ❌ Sai: any type
function bad(data: any) { ... }

// ✅ Đúng: unknown với guard
function good(data: unknown) {
  if (isUser(data)) {
    console.log(data.name);
  }
}
```

### Imports
- **Type-only imports** (`import type { X }`) cho tree-shaking
- Organize imports: external → internal → types

### Documentation
- JSDoc comments cho public APIs
- `@param`, `@returns`, `@throws` annotations
