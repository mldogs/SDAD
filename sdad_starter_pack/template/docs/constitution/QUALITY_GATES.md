# Quality Gates (immutable)

Это “судья” для агента: команды и бюджеты, по которым принимаем работу.

Owner: человек‑арбитр.

---

## Required commands

Заполни реальные команды проекта и ожидаемое поведение.

### Format

    <format-command>

### Lint

    <lint-command>

### Typecheck (optional)

    <typecheck-command>

### Tests

    <test-command>

---

## Acceptance checks

Минимум:
- unit/integration tests зелёные
- линтер зелёный
- performance budget соблюдён (если задан)

Опционально:
- security/static analysis
- coverage threshold

