---
globs:
  - '**/*.py'
---

# Python Conventions

## ✅ Language Rules
- **MANDATORY**: Respond in Vietnamese.
- **WITH EXPLANATION**: `**[English Term]** (Vietnamese description)`

## Quy Tắc Python

### Code Style
- Tuân thủ **PEP 8** (style guide)
- Sử dụng **Black** formatter
- **Type hints** (gợi ý kiểu) cho tất cả functions

### Type Hints
```python
# ✅ Đúng: Type hints đầy đủ
from typing import Optional, List, Dict

def get_user(user_id: str) -> Optional[User]:
    """Lấy thông tin user theo ID.
    
    Args:
        user_id: ID của user cần tìm.
        
    Returns:
        User object nếu tìm thấy, None nếu không.
    """
    ...

# ✅ Đúng: Generic types
def process_items(items: List[T]) -> Dict[str, T]:
    ...
```

### Best Practices
- **Composition over inheritance** (ưu tiên composition)
- **Generators** cho memory efficiency với large datasets
- **Context managers** (`with` statement) cho resource handling
- **Custom exceptions** thay vì generic `Exception`

### Error Handling
```python
# ✅ Đúng: Custom exception
class UserNotFoundError(Exception):
    """Lỗi khi không tìm thấy user."""
    pass

# ✅ Đúng: Specific exception handling
try:
    user = get_user(user_id)
except UserNotFoundError as e:
    logger.error(f"User not found: {e}")
    raise
```

### Testing
- **pytest** cho unit tests
- **Fixtures** cho test setup
- Coverage target: **≥90%**

### Documentation
- **Docstrings** (Google style) cho modules, classes, functions
- Tiếng Việt cho internal docs
- Bilingual cho public APIs
