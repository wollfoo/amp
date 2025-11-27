---
globs:
  - '**/*.ts'
  - '**/*.tsx'
---

# Quy ước TypeScript

- Luôn bật **strict mode** (chế độ nghiêm ngặt) trong `tsconfig.json`.
- Không dùng **any** (kiểu bất kỳ) trừ khi bất khả kháng; ưu tiên **unknown** + type guard.
- Dùng **interfaces** (mô tả cấu trúc đối tượng) cho shape dữ liệu public.
- Ưu tiên **readonly** (chỉ đọc) cho field/prop không thay đổi.
- Hàm nên là **pure functions** (hàm thuần) khi có thể; tránh side-effect khó theo dõi.
- Đặt tên kiểu với hậu tố **Props**, **Options**, **Result** để rõ vai trò.
