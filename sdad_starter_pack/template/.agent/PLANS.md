# PLANS.md — Канонический шаблон

> Этот файл размещается в `.agent/PLANS.md` и определяет формат ExecPlan
> Источники:
> - [OpenAI Cookbook — codex_exec_plans](https://cookbook.openai.com/articles/codex_exec_plans)
> - [openai/openai-agents-js PLANS.md](https://github.com/openai/openai-agents-js/blob/main/PLANS.md)
> - [openai/codex plan mode template](https://github.com/openai/codex/blob/main/codex-rs/core/templates/collaboration_mode/plan.md)
> - [openai/skills create-plan](https://github.com/openai/skills/blob/main/skills/.experimental/create-plan/SKILL.md)

---

## Что такое ExecPlan

**ExecPlan** (Execution Plan) — проектный документ, который агент следует для реализации функции или системного изменения.

Ключевое свойство: план должен быть написан так, чтобы **полный новичок** (без знания репозитория) мог выполнить задачу от начала до конца.

---

## Три фазы создания плана

> Из [codex plan mode template](https://github.com/openai/codex/blob/main/codex-rs/core/templates/collaboration_mode/plan.md)

### Phase 1 — Ground in Environment

Сначала исследуй, потом спрашивай. Устраняй неизвестное через discovery.

```
- Просмотри README.md, docs/, ARCHITECTURE.md
- Изучи релевантные source files
- Определи constraints: язык, фреймворки, CI, deployment
```

### Phase 2 — Intent Chat

Установи, что пользователь действительно хочет: цель, критерии успеха, scope, ограничения.

### Phase 3 — Implementation Chat

Детализируй подход: interfaces, data flow, edge cases, testing, rollout.

**Результат:** План готов к немедленной реализации без дополнительных решений.

---

## Два типа неизвестного

| Тип | Действие |
|-----|----------|
| **Discoverable Facts** | Исследуй репозиторий/систему прежде чем спрашивать |
| **Preferences/Tradeoffs** | Спроси с 2-4 взаимоисключающими вариантами |

---

## 5 требований к ExecPlan (Non-Negotiable)

| Требование | Оригинал | Описание |
|------------|----------|----------|
| **Самодостаточный** | Self-contained | Содержит ВСЮ информацию для новичка |
| **Живой документ** | Living document | Обновляется по мере работы |
| **Понятный новичку** | Novice-guiding | Можно выполнить без знания репозитория |
| **Демонстрируемо рабочий** | Demonstrably working | Результат — наблюдаемое поведение |
| **Простой язык** | Plain language | Каждый термин объясняется сразу |

---

## 4 обязательные секции (Must Update)

Эти секции **обязательно** обновляются по ходу работы:

### 1. Progress (Прогресс)

```markdown
## Progress
- [x] (2025-01-15 10:00Z) Изучить существующую структуру
- [x] (2025-01-15 10:30Z) Создать handler
- [ ] Написать тесты
- [ ] (частично: 2/5 тестов готовы) Покрыть edge cases
```

### 2. Surprises & Discoveries (Неожиданности)

```markdown
## Surprises & Discoveries
- Observation: API возвращает null вместо throwing
  Evidence: `userRepo.findById(999) → null`
  Impact: Нужна явная проверка и 404
```

### 3. Decision Log (Журнал решений)

```markdown
## Decision Log
- Decision: Использовать существующий UserRepository
  Rationale: Уже реализован и покрыт тестами
  Date/Author: 2025-01-15 / @developer
```

### 4. Outcomes & Retrospective (Итоги)

```markdown
## Outcomes & Retrospective
Goal: Добавить endpoint GET /api/users/:id
Result: Работает, тесты проходят, время отклика <50ms
Lessons: Стоило раньше проверить error middleware
```

---

## Структура плана

### Scope (In/Out)

> Из [create-plan SKILL](https://github.com/openai/skills/blob/main/skills/.experimental/create-plan/SKILL.md)

```markdown
## Scope

**In:**
- Endpoint GET /api/users/:id
- Валидация ID
- Тесты: success + not found

**Out:**
- Pagination
- Кеширование
- Авторизация (будет отдельной задачей)
```

### Action Items (6-10, verb-first)

```markdown
## Plan of Work

1. Add handler `getUserById` in `src/api/users.ts`
2. Register route in `src/routes/index.ts`
3. Verify error handling with existing middleware
4. Write unit test for success case
5. Write unit test for not-found case
6. Test manually with curl
7. Update OpenAPI spec
```

Каждый item:
- Начинается с глагола: Add, Refactor, Verify, Ship
- Атомарный и упорядоченный: discovery → changes → tests → rollout
- Минимум один validation item
- Минимум один edge case / risk item

---

## Validation: Observable Behavior

> "HTTP 200 at endpoint" (behavioral) > "added HealthCheck struct" (internal)

```markdown
## Validation and Acceptance

### Criterion 1: Success case
Input: `GET /api/users/1` (user exists)
Output: HTTP 200, `{"id": "1", "name": "...", "email": "..."}`

### Criterion 2: Not found
Input: `GET /api/users/nonexistent`
Output: HTTP 404, `{"error": "User not found"}`

### How to verify:
    $ curl http://localhost:3000/api/users/1
    {"id":"1","name":"John","email":"john@example.com"}
```

---

## Milestone Storytelling

> Из [codex_exec_plans](https://github.com/openai/openai-cookbook/blob/main/articles/codex_exec_plans.md)

Каждая веха следует narrative arc:

```
Goal → Work → Result → Proof
```

```markdown
### Milestone 1: Handler created

**Goal:** Создать handler для получения пользователя по ID

**Work:** Добавлен `getUserById` в `src/api/users.ts`:
- Извлекает ID из params
- Вызывает repository
- Возвращает 404 или 200

**Result:** Handler компилируется и экспортируется

**Proof:**
    $ grep -n "getUserById" src/api/users.ts
    45:export async function getUserById(req, res, next) {
```

---

## Anti-patterns (чего избегать)

| Anti-pattern | Почему плохо | Как правильно |
|--------------|--------------|---------------|
| **Undefined jargon** | "Добавить middleware" — какой? где? | "Добавить `authMiddleware` из `src/middleware/auth.ts`" |
| **Narrow implementation** | "Код компилируется" | "Endpoint возвращает HTTP 200 с данными" |
| **Outsourcing decisions** | "Выбери подходящую библиотеку" | "Использовать `zod` для валидации (уже в проекте)" |
| **"As defined previously"** | Ссылка на prior plan | Повтори определение, даже если redundant |
| **Vague language** | "handle backend" | "Add `POST /api/orders` endpoint" |

---

## Правила форматирования

| Правило | Описание |
|---------|----------|
| **Один code block** | ExecPlan — один fenced block с меткой `md` |
| **Без вложенных блоков** | Используй indented blocks (4 пробела) |
| **Prose-first** | Предпочитай предложения спискам |
| **Checklists только в Progress** | Остальное — prose |
| **Два newline после заголовков** | Для читаемости |

---

## Open Questions (опционально, max 3)

```markdown
## Open Questions
1. Нужна ли rate limiting для этого endpoint?
2. Какой формат ошибок предпочтителен: RFC 7807 или custom?
```

---

## Финализация

План готов когда:
- [ ] Можно начать реализацию **немедленно** без дополнительных решений
- [ ] Scope чётко определён (In/Out)
- [ ] Validation criteria — observable behavior
- [ ] Нет undefined jargon
- [ ] Каждое решение обосновано

**Не спрашивай "should I proceed?"** — план должен быть self-sufficient.
