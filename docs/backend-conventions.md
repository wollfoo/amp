---
globs:
  - 'server/**'
  - 'api/**'
---

# Quy ước Backend

- Mọi **handler API** (xử lý request) phải validate input trước khi dùng.
- Tất cả truy vấn DB phải dùng **parameterized queries** (truy vấn có tham số) để tránh SQL injection.
- Không log **secrets** (bí mật) như token, password, private key.
- Dùng **structured logging** (log có cấu trúc JSON) với `level`, `service`, `request_id`.
- Viết test cho **critical paths** (đường đi quan trọng) của API: happy path + error path.
- Khi thêm endpoint mới, cập nhật tài liệu ở `docs/api/*.md` (nếu có).
