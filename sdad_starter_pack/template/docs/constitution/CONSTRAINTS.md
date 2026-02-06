# Constraints (immutable)

Owner: человек‑арбитр. Агент не меняет без Ask‑first + Decision Log.

---

## Non‑negotiable constraints

- Offline / network:
- Security / privacy:
- Dependency policy:
- Licensing policy:
- Performance budgets:
- Platform/runtime constraints:

---

## Agent boundaries

- Ask first: новые зависимости, DB/schema, CI/CD, секреты, breaking API.
- Never: отключать тесты/линт; коммитить секреты; “магические” изменения без валидации.

