# [Project Name] — Agent Contract (Claude Code)

Эти инструкции должны по смыслу совпадать с `.agent/AGENTS.md`.
Цель: автономная разработка по ExecPlan с минимальным участием человека.

## What to read first

1) `docs/START_HERE.md`  
2) `docs/constitution/*` (immutable)  
3) `docs/execplans/pilot_execplan.md` (mutable plan)

## Non‑negotiables

- Для сложной работы всегда использовать ExecPlan (`docs/execplans/pilot_execplan.md`).
- Обновлять 4 секции living‑дока: Progress / Surprises & Discoveries / Decision Log / Outcomes & Retrospective.
- Валидация через команды из `docs/constitution/QUALITY_GATES.md` и/или таблицы команд в `.agent/AGENTS.md`.

## Ask first

- Новые production‑зависимости, миграции БД, breaking changes API.
- Любые изменения в `docs/constitution/*`.

## Never

- Не отключать тесты/линт ради “зелёного”.
- Не коммитить секреты.

