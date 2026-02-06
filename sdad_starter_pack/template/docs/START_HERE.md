# START HERE (for fresh agents)

Этот файл оптимизирован для агента с пустым контекстом.

Оператору (человеку): режимы запуска Codex см. `docs/RUNBOOK_CODEX.md`. Git‑протокол (автокоммиты) см. `docs/RUNBOOK_GIT.md`.

---

## Source of truth (order)

1) `docs/constitution/PURPOSE.md` — зачем проект и что считается успехом  
2) `docs/constitution/CONSTRAINTS.md` — жёсткие ограничения (immutable)  
3) `docs/constitution/ARCHITECTURE.md` — ключевые границы/контракты  
4) `docs/constitution/QUALITY_GATES.md` — команды, которые подтверждают “готово”  
5) `docs/execplans/pilot_execplan.md` — текущий план (mutable; living doc)  
6) `.agent/AGENTS.md` / `CLAUDE.md` — правила работы агента (Always/Ask/Never)

---

## How to work

Следуй ExecPlan итеративно:

1) возьми один атомарный шаг из `Progress`  
2) внеси изменения в код  
3) запусти проверки (по `QUALITY_GATES.md`)  
4) обнови ExecPlan (Progress + evidence)  
5) сделай локальный commit (если проект использует git; не пушь без Ask‑first)  
6) повтори

Если упёрся:
- зафиксируй “Blocker” в ExecPlan (evidence + варианты)  
- задай максимум 1–3 вопроса (multiple choice)
