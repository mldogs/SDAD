# Project Brief (входной документ)

Этот документ — единственный обязательный “вход” для генерации первичного пакета SDAD‑документации.
Пиши конкретно. Если чего‑то не знаешь — так и напиши (раздел “Open questions”).

---

## 1) One‑liner

Опиши проект в одном предложении: кто пользователь и какую проблему решаем.

---

## 2) Goals (цели)

- Goal 1:
- Goal 2:

---

## 3) Non‑goals (явно НЕ делаем)

- Non‑goal 1:
- Non‑goal 2:

---

## 4) Acceptance criteria (как понять, что “готово”)

Опиши критерии так, чтобы их можно было проверить командами/тестами.

### Functional
- …

### Quality / Metrics
- Performance budget: …
- Coverage target (если применимо): …
- Accuracy target (если применимо): …

### Validation harness (как проверять)
- Primary: `<command>` (пример: `pytest -q`)
- Secondary: `<command>` (пример: `npm test`)

---

## 5) Constraints (жёсткие ограничения)

- Security / privacy:
- Network (можно ли в интернет?):
- Offline‑first (если да — что запрещено):
- Allowed dependencies / stacks:
- Deployment / runtime constraints:

---

## 6) Users & scenarios (2–5 сценариев использования)

1. …
2. …

---

## 7) Current state (если уже есть код/система)

- Repo / modules:
- Known pain points:
- Existing tests / CI:

Если кода пока нет — так и напиши: “greenfield”.

---

## 8) First pilot (bounded work package)

Опиши первый “пилот” так, чтобы он был ограниченным и проверяемым.

- In scope:
- Out of scope:
- Why this pilot:

---

## 9) Open questions (max 3)

1) …
2) …
3) …

