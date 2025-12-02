---
globs:
  - '**/components/**'
  - '**/*.tsx'
  - '**/*.jsx'
  - '**/*.css'
  - '**/*.scss'
  - '**/styles/**'
  - '**/pages/**'
  - '**/views/**'
---

# Frontend Rules

## ✅ Language Rules
- **MANDATORY**: Respond in Vietnamese.
- **WITH EXPLANATION**: `**[English Term]** (Vietnamese description)`

## Quy Tắc Frontend

### Component Architecture
- **Functional components** với hooks
- **Single Responsibility** - mỗi component một nhiệm vụ
- **Composition over inheritance**

### Component Structure
```tsx
// ✅ Cấu trúc component chuẩn
interface ButtonProps {
  variant: 'primary' | 'secondary';
  children: React.ReactNode;
  onClick?: () => void;
  disabled?: boolean;
}

export function Button({ 
  variant, 
  children, 
  onClick, 
  disabled = false 
}: ButtonProps) {
  return (
    <button
      className={cn(styles.button, styles[variant])}
      onClick={onClick}
      disabled={disabled}
    >
      {children}
    </button>
  );
}
```

### State Management
- **Local state** cho component-specific
- **Context** cho shared state (theme, auth)
- **External store** (Zustand, Redux) cho complex state

### Performance
- **React.memo** cho expensive components
- **useMemo/useCallback** khi cần thiết
- **Lazy loading** cho routes và large components
- **Code splitting** để giảm bundle size

### Accessibility (A11y)
- **Semantic HTML** (`<button>`, `<nav>`, `<main>`)
- **ARIA labels** cho interactive elements
- **Keyboard navigation** support
- **Color contrast** ≥4.5:1

```tsx
// ✅ Accessible button
<button
  aria-label="Đóng modal"
  onClick={onClose}
>
  <CloseIcon aria-hidden="true" />
</button>
```

### Styling
- **TailwindCSS** hoặc **CSS Modules**
- **Design tokens** cho consistency
- **Mobile-first** responsive design

### File Organization
```
components/
├── ui/              # Reusable UI components
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.test.tsx
│   │   └── index.ts
├── features/        # Feature-specific components
└── layouts/         # Layout components
```

### Checklist Component
- [ ] Props typed với interface?
- [ ] Default props defined?
- [ ] Accessible (ARIA, keyboard)?
- [ ] Responsive design?
- [ ] Error states handled?
- [ ] Loading states?
