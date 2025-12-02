---
globs:
  - '**/*.go'
  - '**/go.mod'
  - '**/go.sum'
---

# Go Conventions

## ✅ Language Rules
- **MANDATORY**: Respond in Vietnamese.
- **WITH EXPLANATION**: `**[English Term]** (Vietnamese description)`

## Quy Tắc Go

### Code Style
- **Effective Go** principles
- `gofmt` / `goimports` cho formatting
- `golint` / `staticcheck` cho linting

### Error Handling
- **Explicit error handling** - không ignore errors
- **Wrap errors** với context

```go
// ✅ Đúng: Error wrapping với context
if err != nil {
    return fmt.Errorf("failed to create user: %w", err)
}

// ❌ Sai: Ignore error
result, _ := someFunction()
```

### Naming Conventions
- **Exported**: PascalCase (`UserService`, `GetUser`)
- **Unexported**: camelCase (`userRepo`, `getByID`)
- **Acronyms**: viết hoa (`HTTP`, `URL`, `ID`)

### Interfaces
- **Accept interfaces, return structs**
- **Small interfaces** (1-3 methods)
- **Interface naming**: `-er` suffix (`Reader`, `Writer`)

```go
// ✅ Đúng: Small interface
type UserRepository interface {
    GetByID(ctx context.Context, id string) (*User, error)
    Save(ctx context.Context, user *User) error
}
```

### Concurrency
- **Goroutines** cho concurrent operations
- **Channels** cho communication
- **sync.WaitGroup** cho coordination
- **Context** cho cancellation/timeout

```go
// ✅ Đúng: Context với timeout
ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
defer cancel()

result, err := service.Process(ctx, data)
```

### Testing
- **Table-driven tests**
- **Benchmarks** cho performance-critical code
- `go test -race` để detect race conditions

```go
func TestAdd(t *testing.T) {
    tests := []struct {
        name     string
        a, b     int
        expected int
    }{
        {"positive", 1, 2, 3},
        {"negative", -1, -2, -3},
        {"zero", 0, 0, 0},
    }
    
    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            result := Add(tt.a, tt.b)
            if result != tt.expected {
                t.Errorf("got %d, want %d", result, tt.expected)
            }
        })
    }
}
```

### Dependencies
- **Minimal dependencies** - prefer stdlib
- `go mod tidy` để clean unused deps
