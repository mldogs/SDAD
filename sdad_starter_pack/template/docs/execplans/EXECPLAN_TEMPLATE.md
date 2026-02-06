```md
# [Initiative] ExecPlan

Этот ExecPlan — живой документ. Секции `Progress`, `Surprises & Discoveries`,
`Decision Log` и `Outcomes & Retrospective` должны обновляться по мере работы.
Соответствует `.agent/PLANS.md`.

## Purpose / Big Picture

Опиши, что получит пользователь и как это проверить (observable behavior).

## Scope

**In:**
- …

**Out:**
- …

## Progress

- [ ] (YYYY-MM-DD HH:MMZ) Ground: подтвердить текущие факты в репозитории
- [ ] (YYYY-MM-DD HH:MMZ) Implement: минимальный thin-slice
- [ ] (YYYY-MM-DD HH:MMZ) Validate: тесты/линт + ручной smoke
- [ ] (YYYY-MM-DD HH:MMZ) Iterate: закрыть edge cases и обновить документы

## Surprises & Discoveries

- Observation: …
  Evidence: …
  Impact: …

## Decision Log

- Decision: …
  Rationale: …
  Date/Author: YYYY-MM-DD / @name

## Outcomes & Retrospective

Goal: …
Result: …
Proof: …
Lessons: …

## Context and Orientation

Опиши текущее состояние так, как будто читатель ничего не знает:
- ключевые файлы (полными путями)
- термины
- ограничения

## Plan of Work

Прозой: какие изменения будут сделаны, в каких файлах, какие тесты/валидации.

## Concrete Steps

Точные команды, рабочие директории, короткий ожидаемый вывод.
Используй indented blocks (не вставляй вложенные ```).

## Validation and Acceptance

Критерии приёмки как поведение + входы/выходы:
- Success case:
- Not found / negative case:
- Performance budget:

## Idempotence and Recovery

Что безопасно повторять, как откатываться, как не ломать окружение.

## Artifacts and Notes

Короткие транскрипты команд/выводов как доказательства.

## Interfaces and Dependencies

Какие интерфейсы/типы/эндпоинты/модули должны существовать в конце.
Какие зависимости использовать и почему.
```
